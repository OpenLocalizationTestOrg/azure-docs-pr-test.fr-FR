---
title: "tailles d’aaaLinux machine virtuelle dans Azure | Documents Microsoft"
description: "Répertorie les tailles disponibles pour les ordinateurs virtuels Linux dans Azure hello différentes."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: da681171-f045-4c80-a5a9-d8bd47964673
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 56cbe0a0d7d34def07636edba74c4c699e336012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a><span data-ttu-id="18989-103">Tailles des machines virtuelles Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="18989-103">Sizes for Linux virtual machines in Azure</span></span>
<span data-ttu-id="18989-104">Cet article décrit les tailles disponibles hello et des options pour hello des machines virtuelles Azure, vous pouvez utiliser toorun vos applications de Linux et les charges de travail.</span><span class="sxs-lookup"><span data-stu-id="18989-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Linux apps and workloads.</span></span> <span data-ttu-id="18989-105">Il fournit également des toobe de considérations de déploiement prenant en charge de lorsque vous planifiez toouse ces ressources.</span><span class="sxs-lookup"><span data-stu-id="18989-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span> <span data-ttu-id="18989-106">Cet article est également disponible pour les [machines virtuelles Windows](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="18989-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


| <span data-ttu-id="18989-107">Type</span><span class="sxs-lookup"><span data-stu-id="18989-107">Type</span></span>                     | <span data-ttu-id="18989-108">Tailles</span><span class="sxs-lookup"><span data-stu-id="18989-108">Sizes</span></span>           |    <span data-ttu-id="18989-109">Description</span><span class="sxs-lookup"><span data-stu-id="18989-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="18989-110">Usage général</span><span class="sxs-lookup"><span data-stu-id="18989-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="18989-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="18989-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span></span>  | <span data-ttu-id="18989-112">Ratio processeur/mémoire équilibré.</span><span class="sxs-lookup"><span data-stu-id="18989-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="18989-113">Idéal pour le test et développement toomedium petites bases de données et des serveurs web toomedium faible trafic.</span><span class="sxs-lookup"><span data-stu-id="18989-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="18989-114">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="18989-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="18989-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="18989-115">Fs, F</span></span>             | <span data-ttu-id="18989-116">Ratio processeur/mémoire élevé.</span><span class="sxs-lookup"><span data-stu-id="18989-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="18989-117">Convient pour les serveurs web au trafic moyen, les appareils réseau, les processus de traitement par lots et les serveurs d’application.</span><span class="sxs-lookup"><span data-stu-id="18989-117">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span></span>        |
| [<span data-ttu-id="18989-118">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="18989-118">Memory optimized</span></span>](sizes-memory.md)         | <span data-ttu-id="18989-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="18989-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="18989-120">Ratio mémoire/processeur élevé.</span><span class="sxs-lookup"><span data-stu-id="18989-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="18989-121">Idéal pour les serveurs de base de données relationnelle, toolarge moyennes caches et en mémoire analytique.</span><span class="sxs-lookup"><span data-stu-id="18989-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="18989-122">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="18989-122">Storage optimized</span></span>](sizes-storage.md)        | <span data-ttu-id="18989-123">Ls</span><span class="sxs-lookup"><span data-stu-id="18989-123">Ls</span></span>                | <span data-ttu-id="18989-124">Débit de disque et E/S élevés.</span><span class="sxs-lookup"><span data-stu-id="18989-124">High disk throughput and IO.</span></span> <span data-ttu-id="18989-125">Idéale pour les bases de données NoSQL, SQL et Big Data.</span><span class="sxs-lookup"><span data-stu-id="18989-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="18989-126">GPU</span><span class="sxs-lookup"><span data-stu-id="18989-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="18989-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="18989-127">NV, NC</span></span>            | <span data-ttu-id="18989-128">Machines virtuelles spécialisées conçues pour les opérations graphiques lourdes et la retouche vidéo.</span><span class="sxs-lookup"><span data-stu-id="18989-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="18989-129">Disponible avec un ou plusieurs GPU.</span><span class="sxs-lookup"><span data-stu-id="18989-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="18989-130">Calcul haute performance</span><span class="sxs-lookup"><span data-stu-id="18989-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="18989-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="18989-131">H, A8-11</span></span>          | <span data-ttu-id="18989-132">Nos machines virtuelles les plus rapides et dotées des processeurs les plus puissants avec interfaces réseau haut débit en option (RDMA).</span><span class="sxs-lookup"><span data-stu-id="18989-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

- <span data-ttu-id="18989-133">Pour plus d’informations sur la tarification de hello de différentes tailles, consultez [tarification des Machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="18989-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span> 
- <span data-ttu-id="18989-134">Pour la disponibilité des tailles de machine virtuelle dans les régions Azure, consultez [Disponibilité des produits par région](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="18989-134">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
- <span data-ttu-id="18989-135">limites de toosee général sur des machines virtuelles Azure, consultez [abonnement Azure et limites de service, quotas et contraintes](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="18989-135">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="18989-136">Lisez-en davantage sur les [Unités de calcul Azure (ACU)](../windows/acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.</span><span class="sxs-lookup"><span data-stu-id="18989-136">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>


## <a name="rest-api"></a><span data-ttu-id="18989-137">API REST</span><span class="sxs-lookup"><span data-stu-id="18989-137">Rest API</span></span>

<span data-ttu-id="18989-138">Pour des informations sur l’utilisation de tooquery d’API REST hello pour les tailles de machine virtuelle, voir hello :</span><span class="sxs-lookup"><span data-stu-id="18989-138">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- [<span data-ttu-id="18989-139">Répertorier les tailles disponibles des machines virtuelles pour le redimensionnement</span><span class="sxs-lookup"><span data-stu-id="18989-139">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="18989-140">Répertorier les tailles disponibles des machines virtuelles pour un abonnement</span><span class="sxs-lookup"><span data-stu-id="18989-140">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="18989-141">Répertorier les tailles de machine virtuelle disponibles dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="18989-141">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="18989-142">ACU</span><span class="sxs-lookup"><span data-stu-id="18989-142">ACU</span></span>

<span data-ttu-id="18989-143">Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.</span><span class="sxs-lookup"><span data-stu-id="18989-143">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18989-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="18989-144">Next steps</span></span>

<span data-ttu-id="18989-145">En savoir plus sur hello différentes tailles de machine virtuelle qui sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="18989-145">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="18989-146">Usage général</span><span class="sxs-lookup"><span data-stu-id="18989-146">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="18989-147">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="18989-147">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="18989-148">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="18989-148">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="18989-149">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="18989-149">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="18989-150">GPU</span><span class="sxs-lookup"><span data-stu-id="18989-150">GPU</span></span>](sizes-gpu.md)
- [<span data-ttu-id="18989-151">Calcul haute performance</span><span class="sxs-lookup"><span data-stu-id="18989-151">High performance compute</span></span>](sizes-hpc.md)



