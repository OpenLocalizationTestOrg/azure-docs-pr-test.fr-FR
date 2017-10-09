---
title: "aaaMicrosoft architecture du Kit de développement de pile Azure | Documents Microsoft"
description: "Hello vue architecture du Kit de développement Microsoft Azure pile."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a7e61ea4-be2f-4e55-9beb-7a079f348e05
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: helaw
ms.openlocfilehash: 32a19ced7ddd57b97ba796679c116132090402e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-stack-development-kit-architecture"></a><span data-ttu-id="e5e02-103">Architecture du Kit de développement Microsoft Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e5e02-103">Microsoft Azure Stack Development Kit architecture</span></span>
<span data-ttu-id="e5e02-104">Hello Kit de développement de pile Azure est un déploiement à un seul nœud de pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="e5e02-104">hello Azure Stack Development Kit is a single-node deployment of Azure Stack.</span></span> <span data-ttu-id="e5e02-105">Tous les composants de hello sont installés sur des machines virtuelles en cours d’exécution sur un ordinateur hôte unique.</span><span class="sxs-lookup"><span data-stu-id="e5e02-105">All hello components are installed in virtual machines running on a single host machine.</span></span> 

## <a name="logical-architecture-diagram"></a><span data-ttu-id="e5e02-106">Schéma de l’architecture logique</span><span class="sxs-lookup"><span data-stu-id="e5e02-106">Logical architecture diagram</span></span>
<span data-ttu-id="e5e02-107">Hello diagramme suivant illustre architecture logique de hello du kit de développement Azure pile hello et ses composants.</span><span class="sxs-lookup"><span data-stu-id="e5e02-107">hello following diagram illustrates hello logical architecture of hello Azure Stack development kit and its components.</span></span>

![](media/azure-stack-architecture/image1.png)

## <a name="virtual-machine-roles"></a><span data-ttu-id="e5e02-108">Rôles de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e5e02-108">Virtual machine roles</span></span>
<span data-ttu-id="e5e02-109">Hello kit de développement de pile de Azure offre des services à l’aide de hello suivant des ordinateurs virtuels sur l’ordinateur hôte de hello :</span><span class="sxs-lookup"><span data-stu-id="e5e02-109">hello Azure Stack development kit offers services using hello following VMs on hello host:</span></span>

| <span data-ttu-id="e5e02-110">Nom</span><span class="sxs-lookup"><span data-stu-id="e5e02-110">Name</span></span> | <span data-ttu-id="e5e02-111">Description</span><span class="sxs-lookup"><span data-stu-id="e5e02-111">Description</span></span> |
| ----- | ----- |
| <span data-ttu-id="e5e02-112">**AzS-ACS01**</span><span class="sxs-lookup"><span data-stu-id="e5e02-112">**AzS-ACS01**</span></span> | <span data-ttu-id="e5e02-113">Services de stockage Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e5e02-113">Azure Stack storage services.</span></span>|
| <span data-ttu-id="e5e02-114">**AzS-ADFS01**</span><span class="sxs-lookup"><span data-stu-id="e5e02-114">**AzS-ADFS01**</span></span> | <span data-ttu-id="e5e02-115">Services de fédération Active Directory (ADFS).</span><span class="sxs-lookup"><span data-stu-id="e5e02-115">Active Directory Federation Services (ADFS).</span></span>  |
| <span data-ttu-id="e5e02-116">**AzS-BGPNAT01**</span><span class="sxs-lookup"><span data-stu-id="e5e02-116">**AzS-BGPNAT01**</span></span> | <span data-ttu-id="e5e02-117">Routeur Edge et fournit des capacités NAT et VPN pour Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e5e02-117">Edge router and provides NAT and VPN capabilities for Azure Stack.</span></span> |
| <span data-ttu-id="e5e02-118">**AzS-CA01**</span><span class="sxs-lookup"><span data-stu-id="e5e02-118">**AzS-CA01**</span></span> | <span data-ttu-id="e5e02-119">Services d’autorité de certification pour les services de rôle Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e5e02-119">Certificate authority services for Azure Stack role services.</span></span>|
| <span data-ttu-id="e5e02-120">**AzS-DC01**</span><span class="sxs-lookup"><span data-stu-id="e5e02-120">**AzS-DC01**</span></span> | <span data-ttu-id="e5e02-121">Services Active Directory, DNS et DHCP pour Microsoft Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e5e02-121">Active Directory, DNS, and DHCP services for Microsoft Azure Stack.</span></span>|
| <span data-ttu-id="e5e02-122">**AzS-ERCS01**</span><span class="sxs-lookup"><span data-stu-id="e5e02-122">**AzS-ERCS01**</span></span> | <span data-ttu-id="e5e02-123">Machine virtuelle la console de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="e5e02-123">Emergency Recovery Console VM.</span></span> |
| <span data-ttu-id="e5e02-124">**AzS-GWY01**</span><span class="sxs-lookup"><span data-stu-id="e5e02-124">**AzS-GWY01**</span></span> | <span data-ttu-id="e5e02-125">Services de passerelle Edge, comme les connexions de site à site VPN pour les réseaux locataires.</span><span class="sxs-lookup"><span data-stu-id="e5e02-125">Edge gateway services such as VPN site-to-site connections for tenant networks.</span></span>|
| <span data-ttu-id="e5e02-126">**AzS-NC01**</span><span class="sxs-lookup"><span data-stu-id="e5e02-126">**AzS-NC01**</span></span> | <span data-ttu-id="e5e02-127">Contrôleur réseau qui gère les services réseau Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e5e02-127">Network Controller, which manages Azure Stack network services.</span></span>  |
| <span data-ttu-id="e5e02-128">**AzS-SLB01**</span><span class="sxs-lookup"><span data-stu-id="e5e02-128">**AzS-SLB01**</span></span> | <span data-ttu-id="e5e02-129">Services multiplexeur d’équilibrage de charge dans Azure Stack pour les clients et les services d’infrastructure Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e5e02-129">Load balancing multiplexer services in Azure Stack for both tenants and Azure Stack infrastructure services.</span></span>  |
| <span data-ttu-id="e5e02-130">**AzS-SQL01**</span><span class="sxs-lookup"><span data-stu-id="e5e02-130">**AzS-SQL01**</span></span> | <span data-ttu-id="e5e02-131">Magasin de données interne pour les rôles d’infrastructure Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="e5e02-131">Internal data store for Azure Stack infrastructure roles.</span></span>  |
| <span data-ttu-id="e5e02-132">**AzS-WAS01**</span><span class="sxs-lookup"><span data-stu-id="e5e02-132">**AzS-WAS01**</span></span> | <span data-ttu-id="e5e02-133">Portail d’administration Azure Stack et services Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e5e02-133">Azure Stack administrative portal and Azure Resource Manager services.</span></span>|
| <span data-ttu-id="e5e02-134">**AzS-WASP01**</span><span class="sxs-lookup"><span data-stu-id="e5e02-134">**AzS-WASP01**</span></span>| <span data-ttu-id="e5e02-135">Portail utilisateur (locataire) Azure Stack et services Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e5e02-135">Azure Stack user (tenant) portal and Azure Resource Manager services.</span></span>|
| <span data-ttu-id="e5e02-136">**AzS-XRP01**</span><span class="sxs-lookup"><span data-stu-id="e5e02-136">**AzS-XRP01**</span></span> | <span data-ttu-id="e5e02-137">Contrôleur de gestion d’infrastructure pour la pile Microsoft Azure, y compris les fournisseurs de ressources de calcul, réseau et stockage hello.</span><span class="sxs-lookup"><span data-stu-id="e5e02-137">Infrastructure management controller for Microsoft Azure Stack, including hello Compute, Network, and Storage resource providers.</span></span>|


## <a name="next-steps"></a><span data-ttu-id="e5e02-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e5e02-138">Next steps</span></span>
[<span data-ttu-id="e5e02-139">Déployer Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e5e02-139">Deploy Azure Stack</span></span>](azure-stack-deploy.md)

[<span data-ttu-id="e5e02-140">Première tootry de scénarios</span><span class="sxs-lookup"><span data-stu-id="e5e02-140">First scenarios tootry</span></span>](azure-stack-first-scenarios.md)

