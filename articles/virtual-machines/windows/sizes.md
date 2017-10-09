---
title: "tailles d’aaaWindows machine virtuelle dans Azure | Documents Microsoft"
description: "Répertorie les tailles disponibles pour les machines virtuelles Windows Azure hello différentes."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: aabf0d30-04eb-4d34-b44a-69f8bfb84f22
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 80bd8241b134031c41b56224e841c7557c4845cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="4e3d2-103">Tailles des machines virtuelles Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="4e3d2-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="4e3d2-104">Cet article décrit les tailles disponibles hello et des options pour hello des machines virtuelles Azure, vous pouvez utiliser toorun vos applications Windows et les charges de travail.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-104">This article describes hello available sizes and options for hello Azure virtual machines you can use toorun your Windows apps and workloads.</span></span> <span data-ttu-id="4e3d2-105">Il fournit également des toobe de considérations de déploiement prenant en charge de lorsque vous planifiez toouse ces ressources.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-105">It also provides deployment considerations toobe aware of when you're planning toouse these resources.</span></span>  <span data-ttu-id="4e3d2-106">Cet article est également disponible pour les [machines virtuelles Linux](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4e3d2-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


| <span data-ttu-id="4e3d2-107">Type</span><span class="sxs-lookup"><span data-stu-id="4e3d2-107">Type</span></span>                     | <span data-ttu-id="4e3d2-108">Tailles</span><span class="sxs-lookup"><span data-stu-id="4e3d2-108">Sizes</span></span>           |    <span data-ttu-id="4e3d2-109">Description</span><span class="sxs-lookup"><span data-stu-id="4e3d2-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="4e3d2-110">Usage général</span><span class="sxs-lookup"><span data-stu-id="4e3d2-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="4e3d2-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="4e3d2-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="4e3d2-112">Ratio processeur/mémoire équilibré.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="4e3d2-113">Idéal pour le test et développement toomedium petites bases de données et des serveurs web toomedium faible trafic.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-113">Ideal for testing and development, small toomedium databases, and low toomedium traffic web servers.</span></span> |
| [<span data-ttu-id="4e3d2-114">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="4e3d2-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="4e3d2-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="4e3d2-115">Fs, F</span></span>             | <span data-ttu-id="4e3d2-116">Ratio processeur/mémoire élevé.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="4e3d2-117">Convient pour les serveurs web au trafic moyen, les appareils réseau, les processus de traitement par lots et les serveurs d’application.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="4e3d2-118">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="4e3d2-118">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="4e3d2-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="4e3d2-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="4e3d2-120">Ratio mémoire/processeur élevé.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="4e3d2-121">Idéal pour les serveurs de base de données relationnelle, toolarge moyennes caches et en mémoire analytique.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-121">Great for relational database servers, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="4e3d2-122">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="4e3d2-122">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="4e3d2-123">Ls</span><span class="sxs-lookup"><span data-stu-id="4e3d2-123">Ls</span></span>                | <span data-ttu-id="4e3d2-124">Débit de disque et E/S élevés.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-124">High disk throughput and IO.</span></span> <span data-ttu-id="4e3d2-125">Idéale pour les bases de données NoSQL, SQL et Big Data.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="4e3d2-126">GPU</span><span class="sxs-lookup"><span data-stu-id="4e3d2-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="4e3d2-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="4e3d2-127">NV, NC</span></span>            | <span data-ttu-id="4e3d2-128">Machines virtuelles spécialisées conçues pour les opérations graphiques lourdes et la retouche vidéo.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="4e3d2-129">Disponible avec un ou plusieurs GPU.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="4e3d2-130">Calcul haute performance</span><span class="sxs-lookup"><span data-stu-id="4e3d2-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="4e3d2-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="4e3d2-131">H, A8-11</span></span>          | <span data-ttu-id="4e3d2-132">Nos machines virtuelles les plus rapides et dotées des processeurs les plus puissants avec interfaces réseau haut débit en option (RDMA).</span><span class="sxs-lookup"><span data-stu-id="4e3d2-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br> 

- <span data-ttu-id="4e3d2-133">Pour plus d’informations sur la tarification de hello de différentes tailles, consultez [tarification des Machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span><span class="sxs-lookup"><span data-stu-id="4e3d2-133">For information about pricing of hello various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
- <span data-ttu-id="4e3d2-134">limites de toosee général sur des machines virtuelles Azure, consultez [abonnement Azure et limites de service, quotas et contraintes](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="4e3d2-134">toosee general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="4e3d2-135">Les coûts de stockage sont calculés séparément en fonction des pages utilisées dans le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-135">Storage costs are calculated separately based on used pages in hello storage account.</span></span> <span data-ttu-id="4e3d2-136">Pour plus d’informations, consultez [Prix appliqués à Azure Storage](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="4e3d2-136">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
- <span data-ttu-id="4e3d2-137">Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-137">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>



## <a name="rest-api"></a><span data-ttu-id="4e3d2-138">API REST</span><span class="sxs-lookup"><span data-stu-id="4e3d2-138">Rest API</span></span>

<span data-ttu-id="4e3d2-139">Pour des informations sur l’utilisation de tooquery d’API REST hello pour les tailles de machine virtuelle, voir hello :</span><span class="sxs-lookup"><span data-stu-id="4e3d2-139">For information on using hello REST API tooquery for VM sizes, see hello following:</span></span>

- [<span data-ttu-id="4e3d2-140">Répertorier les tailles disponibles des machines virtuelles pour le redimensionnement</span><span class="sxs-lookup"><span data-stu-id="4e3d2-140">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="4e3d2-141">Répertorier les tailles disponibles des machines virtuelles pour un abonnement</span><span class="sxs-lookup"><span data-stu-id="4e3d2-141">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="4e3d2-142">Répertorier les tailles de machine virtuelle disponibles dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="4e3d2-142">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="4e3d2-143">ACU</span><span class="sxs-lookup"><span data-stu-id="4e3d2-143">ACU</span></span>

<span data-ttu-id="4e3d2-144">Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.</span><span class="sxs-lookup"><span data-stu-id="4e3d2-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e3d2-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e3d2-145">Next steps</span></span>

<span data-ttu-id="4e3d2-146">En savoir plus sur hello différentes tailles de machine virtuelle qui sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="4e3d2-146">Learn more about hello different VM sizes that are available:</span></span>
- [<span data-ttu-id="4e3d2-147">Usage général</span><span class="sxs-lookup"><span data-stu-id="4e3d2-147">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="4e3d2-148">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="4e3d2-148">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="4e3d2-149">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="4e3d2-149">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="4e3d2-150">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="4e3d2-150">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="4e3d2-151">Optimisé pour le GPU</span><span class="sxs-lookup"><span data-stu-id="4e3d2-151">GPU optimized</span></span>](sizes-gpu.md)
- [<span data-ttu-id="4e3d2-152">Calcul haute performance</span><span class="sxs-lookup"><span data-stu-id="4e3d2-152">High performance compute</span></span>](sizes-hpc.md)



