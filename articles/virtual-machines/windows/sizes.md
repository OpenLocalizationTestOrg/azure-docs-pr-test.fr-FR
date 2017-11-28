---
title: Tailles des machines virtuelles Windows dans Azure | Microsoft Docs
description: "Répertorie les différentes tailles disponibles pour les machines virtuelles Windows dans Azure."
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
ms.openlocfilehash: b3a674137ed3dd47188d4af0bc845104eabc885e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="sizes-for-windows-virtual-machines-in-azure"></a><span data-ttu-id="3973a-103">Tailles des machines virtuelles Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="3973a-103">Sizes for Windows virtual machines in Azure</span></span>

<span data-ttu-id="3973a-104">Cet article décrit les tailles et options disponibles pour les machines virtuelles Azure que vous pouvez utiliser pour exécuter vos applications et charges de travail Windows.</span><span class="sxs-lookup"><span data-stu-id="3973a-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Windows apps and workloads.</span></span> <span data-ttu-id="3973a-105">Il expose également les points à prendre en considération pour le déploiement quand vous planifiez l’utilisation de ces ressources.</span><span class="sxs-lookup"><span data-stu-id="3973a-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span></span>  <span data-ttu-id="3973a-106">Cet article est également disponible pour les [machines virtuelles Linux](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3973a-106">This article is also available for [Linux virtual machines](../linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


| <span data-ttu-id="3973a-107">Type</span><span class="sxs-lookup"><span data-stu-id="3973a-107">Type</span></span>                     | <span data-ttu-id="3973a-108">Tailles</span><span class="sxs-lookup"><span data-stu-id="3973a-108">Sizes</span></span>           |    <span data-ttu-id="3973a-109">Description</span><span class="sxs-lookup"><span data-stu-id="3973a-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="3973a-110">Usage général</span><span class="sxs-lookup"><span data-stu-id="3973a-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="3973a-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="3973a-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span> | <span data-ttu-id="3973a-112">Ratio processeur/mémoire équilibré.</span><span class="sxs-lookup"><span data-stu-id="3973a-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="3973a-113">Idéal pour le test et le développement, les bases de données petites à moyennes et les serveurs web au trafic faible à moyen.</span><span class="sxs-lookup"><span data-stu-id="3973a-113">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span></span> |
| [<span data-ttu-id="3973a-114">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="3973a-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="3973a-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="3973a-115">Fs, F</span></span>             | <span data-ttu-id="3973a-116">Ratio processeur/mémoire élevé.</span><span class="sxs-lookup"><span data-stu-id="3973a-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="3973a-117">Convient pour les serveurs web au trafic moyen, les appareils réseau, les processus de traitement par lots et les serveurs d’application.</span><span class="sxs-lookup"><span data-stu-id="3973a-117">Good for medium traffic web servers, network appliances, batch processes, and application servers.</span></span>        |
| [<span data-ttu-id="3973a-118">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="3973a-118">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)         | <span data-ttu-id="3973a-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="3973a-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="3973a-120">Ratio mémoire/processeur élevé.</span><span class="sxs-lookup"><span data-stu-id="3973a-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="3973a-121">Idéal pour les serveurs de base de données relationnelle, les caches moyens à grands et l’analytique en mémoire.</span><span class="sxs-lookup"><span data-stu-id="3973a-121">Great for relational database servers, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="3973a-122">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="3973a-122">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)        | <span data-ttu-id="3973a-123">Ls</span><span class="sxs-lookup"><span data-stu-id="3973a-123">Ls</span></span>                | <span data-ttu-id="3973a-124">Débit de disque et E/S élevés.</span><span class="sxs-lookup"><span data-stu-id="3973a-124">High disk throughput and IO.</span></span> <span data-ttu-id="3973a-125">Idéale pour les bases de données NoSQL, SQL et Big Data.</span><span class="sxs-lookup"><span data-stu-id="3973a-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="3973a-126">GPU</span><span class="sxs-lookup"><span data-stu-id="3973a-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="3973a-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="3973a-127">NV, NC</span></span>            | <span data-ttu-id="3973a-128">Machines virtuelles spécialisées conçues pour les opérations graphiques lourdes et la retouche vidéo.</span><span class="sxs-lookup"><span data-stu-id="3973a-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="3973a-129">Disponible avec un ou plusieurs GPU.</span><span class="sxs-lookup"><span data-stu-id="3973a-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="3973a-130">Calcul haute performance</span><span class="sxs-lookup"><span data-stu-id="3973a-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="3973a-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="3973a-131">H, A8-11</span></span>          | <span data-ttu-id="3973a-132">Nos machines virtuelles les plus rapides et dotées des processeurs les plus puissants avec interfaces réseau haut débit en option (RDMA).</span><span class="sxs-lookup"><span data-stu-id="3973a-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br> 

- <span data-ttu-id="3973a-133">Pour plus d'informations sur la tarification des différentes tailles, consultez [Tarification des machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span><span class="sxs-lookup"><span data-stu-id="3973a-133">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows).</span></span> 
- <span data-ttu-id="3973a-134">Pour connaître les limites générales des machines virtuelles Azure, consultez [Abonnement Azure et limites, quotas et contraintes du service](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="3973a-134">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="3973a-135">Les coûts de stockage sont calculés séparément en fonction des pages utilisées dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3973a-135">Storage costs are calculated separately based on used pages in the storage account.</span></span> <span data-ttu-id="3973a-136">Pour plus d’informations, consultez [Prix appliqués à Azure Storage](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="3973a-136">For details, [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>
- <span data-ttu-id="3973a-137">Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.</span><span class="sxs-lookup"><span data-stu-id="3973a-137">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>



## <a name="rest-api"></a><span data-ttu-id="3973a-138">API REST</span><span class="sxs-lookup"><span data-stu-id="3973a-138">Rest API</span></span>

<span data-ttu-id="3973a-139">Pour plus d’informations sur l’utilisation de l’API REST pour demander la taille des machines virtuelles, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="3973a-139">For information on using the REST API to query for VM sizes, see the following:</span></span>

- [<span data-ttu-id="3973a-140">Répertorier les tailles disponibles des machines virtuelles pour le redimensionnement</span><span class="sxs-lookup"><span data-stu-id="3973a-140">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="3973a-141">Répertorier les tailles disponibles des machines virtuelles pour un abonnement</span><span class="sxs-lookup"><span data-stu-id="3973a-141">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="3973a-142">Répertorier les tailles de machine virtuelle disponibles dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="3973a-142">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="3973a-143">ACU</span><span class="sxs-lookup"><span data-stu-id="3973a-143">ACU</span></span>

<span data-ttu-id="3973a-144">Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.</span><span class="sxs-lookup"><span data-stu-id="3973a-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3973a-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3973a-145">Next steps</span></span>

<span data-ttu-id="3973a-146">En savoir plus sur les différentes tailles de machines virtuelles qui sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="3973a-146">Learn more about the different VM sizes that are available:</span></span>
- [<span data-ttu-id="3973a-147">Usage général</span><span class="sxs-lookup"><span data-stu-id="3973a-147">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="3973a-148">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="3973a-148">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="3973a-149">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="3973a-149">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="3973a-150">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="3973a-150">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="3973a-151">Optimisé pour le GPU</span><span class="sxs-lookup"><span data-stu-id="3973a-151">GPU optimized</span></span>](sizes-gpu.md)
- [<span data-ttu-id="3973a-152">Calcul haute performance</span><span class="sxs-lookup"><span data-stu-id="3973a-152">High performance compute</span></span>](sizes-hpc.md)



