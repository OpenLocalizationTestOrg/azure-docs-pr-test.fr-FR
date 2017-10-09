---
title: aaaUsing hello administrateur et utilisateur les portails dans Azure pile | Documents Microsoft
description: "Découvrez les différences de hello entre les portails de hello administrateur et utilisateur dans la pile de Azure."
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
ms.openlocfilehash: 5e940749917e4aade26483a79bcc238346bf94f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-administrator-and-user-portals-in-azure-stack"></a><span data-ttu-id="c470f-103">À l’aide des portails d’administrateur et utilisateur hello dans la pile de Azure</span><span class="sxs-lookup"><span data-stu-id="c470f-103">Using hello administrator and user portals in Azure Stack</span></span>

<span data-ttu-id="c470f-104">Il existe deux portails dans la pile de Azure ; Hello du portail de l’administrateur et le portail de l’utilisateur hello (également appelée tooas hello *client* portail).</span><span class="sxs-lookup"><span data-stu-id="c470f-104">There are two portals in Azure Stack; hello administrator portal and hello user portal (also referred tooas hello *tenant* portal).</span></span> <span data-ttu-id="c470f-105">les portails Hello sont soutenues par des instances distinctes du Gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="c470f-105">hello portals are backed by separate instances of Azure Resource Manager.</span></span>

<span data-ttu-id="c470f-106">tableau Hello suivant montre comment tooconnect toohello portails et des points de terminaison tooResource Manager dans un environnement du Kit de développement de pile Azure.</span><span class="sxs-lookup"><span data-stu-id="c470f-106">hello following table shows how tooconnect toohello portals and tooResource Manager endpoints in an Azure Stack Development Kit environment.</span></span>

|  <span data-ttu-id="c470f-107">Portail</span><span class="sxs-lookup"><span data-stu-id="c470f-107">Portal</span></span> | <span data-ttu-id="c470f-108">URL du portail</span><span class="sxs-lookup"><span data-stu-id="c470f-108">Portal URL</span></span> | <span data-ttu-id="c470f-109">URL de point de terminaison Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c470f-109">Resource Manager endpoint URL</span></span> |   
| -------- | ------------- | ------- |  
| <span data-ttu-id="c470f-110">Administrateur</span><span class="sxs-lookup"><span data-stu-id="c470f-110">Administrator</span></span> | <span data-ttu-id="c470f-111">https://adminportal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="c470f-111">https://adminportal.local.azurestack.external</span></span>  | <span data-ttu-id="c470f-112">https://adminmanagement.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="c470f-112">https://adminmanagement.local.azurestack.external</span></span>  |  
| <span data-ttu-id="c470f-113">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="c470f-113">User</span></span> | <span data-ttu-id="c470f-114">https://portal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="c470f-114">https://portal.local.azurestack.external</span></span> | <span data-ttu-id="c470f-115">https://management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="c470f-115">https://management.local.azurestack.external</span></span>  |
| | |

## <a name="hello-administrator-portal"></a><span data-ttu-id="c470f-116">portail d’administration Hello</span><span class="sxs-lookup"><span data-stu-id="c470f-116">hello administrator portal</span></span>

<span data-ttu-id="c470f-117">portail d’administration Hello permet à un cloud opérateur tooperform tâches d’administration et opérationnel.</span><span class="sxs-lookup"><span data-stu-id="c470f-117">hello administrator portal enables a cloud operator tooperform administrative and operational tasks.</span></span> <span data-ttu-id="c470f-118">Un opérateur cloud peut effectuer des opérations telles que :</span><span class="sxs-lookup"><span data-stu-id="c470f-118">A cloud operator can do things such as:</span></span>
* <span data-ttu-id="c470f-119">Surveiller l’intégrité et les alertes</span><span class="sxs-lookup"><span data-stu-id="c470f-119">monitor health and alerts</span></span>
* <span data-ttu-id="c470f-120">Gérer la capacité</span><span class="sxs-lookup"><span data-stu-id="c470f-120">manage capacity</span></span>
* <span data-ttu-id="c470f-121">remplir le marketplace de hello</span><span class="sxs-lookup"><span data-stu-id="c470f-121">populate hello marketplace</span></span>
* <span data-ttu-id="c470f-122">Créer des plans et des offres</span><span class="sxs-lookup"><span data-stu-id="c470f-122">create plans and offers</span></span>
* <span data-ttu-id="c470f-123">Créer des abonnements pour les locataires</span><span class="sxs-lookup"><span data-stu-id="c470f-123">create subscriptions for tenants</span></span>

<span data-ttu-id="c470f-124">Un opérateur cloud peut aussi créer des ressources telles que des machines virtuelles, des réseaux virtuels et des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="c470f-124">A cloud operator can also create resources such as virtual machines, virtual networks, and storage accounts.</span></span>

 ![portail d’administration Hello](media/azure-stack-manage-portals/image1.png)

 ## <a name="hello-user-portal"></a><span data-ttu-id="c470f-126">portail de l’utilisateur Hello</span><span class="sxs-lookup"><span data-stu-id="c470f-126">hello user portal</span></span>

 <span data-ttu-id="c470f-127">portail de l’utilisateur Hello ne fournit pas de tooany accès hello administratifs ou opérationnels des fonctionnalités de portail d’administration hello.</span><span class="sxs-lookup"><span data-stu-id="c470f-127">hello user portal does not provide access tooany of hello administrative or operational capabilities of hello administrator portal.</span></span> <span data-ttu-id="c470f-128">Dans le portail de l’utilisateur hello, un utilisateur peut s’abonner à des offres toopublic et utiliser les services hello qui sont rendues disponibles par le biais des offres.</span><span class="sxs-lookup"><span data-stu-id="c470f-128">In hello user portal, a user can subscribe toopublic offers, and use hello services that are made available through those offers.</span></span>

  ![portail de l’utilisateur Hello](media/azure-stack-manage-portals/image2.png)
 
 ## <a name="subscription-behavior"></a><span data-ttu-id="c470f-130">Comportement de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="c470f-130">Subscription behavior</span></span>
 
 <span data-ttu-id="c470f-131">Assurez-vous que vous comprenez hello suivant des différences entre le comportement de l’abonnement dans les portails de hello deux.</span><span class="sxs-lookup"><span data-stu-id="c470f-131">Make sure that you understand hello following differences between subscription behavior in hello two portals.</span></span>

 <span data-ttu-id="c470f-132">Portail administrateur :</span><span class="sxs-lookup"><span data-stu-id="c470f-132">Administrator portal:</span></span>
* <span data-ttu-id="c470f-133">Il n'existe qu’un seul abonnement qui est disponible dans le portail d’administration hello.</span><span class="sxs-lookup"><span data-stu-id="c470f-133">There is only one subscription that is available in hello administrator portal.</span></span> <span data-ttu-id="c470f-134">Cet abonnement est hello *abonnement de fournisseur par défaut*.</span><span class="sxs-lookup"><span data-stu-id="c470f-134">This subscription is hello *Default Provider Subscription*.</span></span> <span data-ttu-id="c470f-135">Impossible d’ajouter tous les abonnements pour une utilisation dans le portail d’administration hello.</span><span class="sxs-lookup"><span data-stu-id="c470f-135">You can't add any other subscriptions for use in hello administrator portal.</span></span>
* <span data-ttu-id="c470f-136">Comme un opérateur cloud, vous pouvez ajouter des abonnements pour vos utilisateurs (y compris vous-même) à partir du portail d’administration hello.</span><span class="sxs-lookup"><span data-stu-id="c470f-136">As a cloud operator, you can add subscriptions for your users (including yourself) from hello administrator portal.</span></span> <span data-ttu-id="c470f-137">Les utilisateurs (y compris vous-même) peuvent accéder et utiliser ces abonnements à partir du portail de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="c470f-137">Users (including yourself) can access and use these subscriptions from hello user portal.</span></span>

  >[!NOTE]
  <span data-ttu-id="c470f-138">En raison de hello séparation du Gestionnaire de ressources Azure, les abonnements ne traversent pas portails.</span><span class="sxs-lookup"><span data-stu-id="c470f-138">Because of hello Azure Resource Manager separation, subscriptions do not cross portals.</span></span> <span data-ttu-id="c470f-139">Par exemple, si vous en tant qu’un opérateur cloud toohello portail de l’utilisateur se connecte, hello abonnement de fournisseur par défaut ne peut pas accéder à.</span><span class="sxs-lookup"><span data-stu-id="c470f-139">For example, if you as a cloud operator signs in toohello user portal, you can't access hello Default Provider Subscription.</span></span> <span data-ttu-id="c470f-140">Par conséquent, vous n’avez accès tooany les fonctions d’administration.</span><span class="sxs-lookup"><span data-stu-id="c470f-140">Therefore, you don't have access tooany administrative functions.</span></span> <span data-ttu-id="c470f-141">Vous pouvez créer des abonnements pour vous-même à partir d’offres publiques, mais vous êtes considéré comme un utilisateur de locataire.</span><span class="sxs-lookup"><span data-stu-id="c470f-141">You can create subscriptions for yourself from public offers, but you are considered a tenant user.</span></span>

<span data-ttu-id="c470f-142">Portail utilisateur :</span><span class="sxs-lookup"><span data-stu-id="c470f-142">User portal:</span></span>
* <span data-ttu-id="c470f-143">Dans le portail de l’utilisateur hello, un compte peut avoir plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="c470f-143">In hello user portal, an account can have multiple subscriptions.</span></span>

  >[!NOTE]
  <span data-ttu-id="c470f-144">Dans l’environnement de kit développement hello, si un utilisateur du client appartient toohello même répertoire en tant qu’opérateur de cloud hello, ils ne sont pas bloqués à partir de la signature dans le portail d’administration toohello.</span><span class="sxs-lookup"><span data-stu-id="c470f-144">In hello development kit environment, if a tenant user belongs toohello same directory as hello cloud operator, they are not blocked from signing in toohello administrator portal.</span></span> <span data-ttu-id="c470f-145">Toutefois, ils ne peut pas accéder aux fonctions administratives de hello.</span><span class="sxs-lookup"><span data-stu-id="c470f-145">However, they can't access any of hello administrative functions.</span></span> <span data-ttu-id="c470f-146">En outre, ils ne peuvent pas ajouter des abonnements ou l’accès offres effectuées toothem disponible dans le portail de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="c470f-146">Also, they can't add subscriptions or access offers that are made available toothem in hello user portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c470f-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c470f-147">Next steps</span></span>

[<span data-ttu-id="c470f-148">Se connecter tooAzure pile</span><span class="sxs-lookup"><span data-stu-id="c470f-148">Connect tooAzure Stack</span></span>](azure-stack-connect-azure-stack.md)

[<span data-ttu-id="c470f-149">Gestion des régions dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="c470f-149">Region management in Azure Stack</span></span>](azure-stack-region-management.md)
