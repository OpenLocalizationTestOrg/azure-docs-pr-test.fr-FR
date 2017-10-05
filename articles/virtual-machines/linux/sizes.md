---
title: Tailles des machines virtuelles Linux dans Azure | Microsoft Docs
description: "Répertorie les différentes tailles disponibles pour les machines virtuelles Linux dans Azure."
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
ms.openlocfilehash: fe7a92901ae25aa99ef71f09c416e6c6ad30d39b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="sizes-for-linux-virtual-machines-in-azure"></a><span data-ttu-id="2e1b7-103">Tailles des machines virtuelles Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="2e1b7-103">Sizes for Linux virtual machines in Azure</span></span>
<span data-ttu-id="2e1b7-104">Cet article décrit les tailles et options disponibles pour les machines virtuelles Azure que vous pouvez utiliser pour exécuter vos applications et charges de travail Linux.</span><span class="sxs-lookup"><span data-stu-id="2e1b7-104">This article describes the available sizes and options for the Azure virtual machines you can use to run your Linux apps and workloads.</span></span> <span data-ttu-id="2e1b7-105">Il expose également les points à prendre en considération pour le déploiement quand vous planifiez l’utilisation de ces ressources.</span><span class="sxs-lookup"><span data-stu-id="2e1b7-105">It also provides deployment considerations to be aware of when you're planning to use these resources.</span></span> <span data-ttu-id="2e1b7-106">Cet article est également disponible pour les [machines virtuelles Windows](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e1b7-106">This article is also available for [Windows virtual machines](../windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


| <span data-ttu-id="2e1b7-107">Type</span><span class="sxs-lookup"><span data-stu-id="2e1b7-107">Type</span></span>                     | <span data-ttu-id="2e1b7-108">Tailles</span><span class="sxs-lookup"><span data-stu-id="2e1b7-108">Sizes</span></span>           |    <span data-ttu-id="2e1b7-109">Description</span><span class="sxs-lookup"><span data-stu-id="2e1b7-109">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="2e1b7-110">Usage général</span><span class="sxs-lookup"><span data-stu-id="2e1b7-110">General purpose</span></span>](sizes-general.md)          | <span data-ttu-id="2e1b7-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="2e1b7-111">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7,</span></span>  | <span data-ttu-id="2e1b7-112">Ratio processeur/mémoire équilibré.</span><span class="sxs-lookup"><span data-stu-id="2e1b7-112">Balanced CPU-to-memory ratio.</span></span> <span data-ttu-id="2e1b7-113">Idéal pour le test et le développement, les bases de données petites à moyennes et les serveurs web au trafic faible à moyen.</span><span class="sxs-lookup"><span data-stu-id="2e1b7-113">Ideal for testing and development, small to medium databases, and low to medium traffic web servers.</span></span> |
| [<span data-ttu-id="2e1b7-114">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="2e1b7-114">Compute optimized</span></span>](sizes-compute.md)        | <span data-ttu-id="2e1b7-115">Fs, F</span><span class="sxs-lookup"><span data-stu-id="2e1b7-115">Fs, F</span></span>             | <span data-ttu-id="2e1b7-116">Ratio processeur/mémoire élevé.</span><span class="sxs-lookup"><span data-stu-id="2e1b7-116">High CPU-to-memory ratio.</span></span> <span data-ttu-id="2e1b7-117">Convient pour les serveurs web au trafic moyen, les appareils réseau, les processus de traitement par lots et les serveurs d’application.</span><span class="sxs-lookup"><span data-stu-id="2e1b7-117">Good for medium traffic web servers, network appliances, bath processes, and application servers.</span></span>        |
| [<span data-ttu-id="2e1b7-118">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="2e1b7-118">Memory optimized</span></span>](sizes-memory.md)         | <span data-ttu-id="2e1b7-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="2e1b7-119">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="2e1b7-120">Ratio mémoire/processeur élevé.</span><span class="sxs-lookup"><span data-stu-id="2e1b7-120">High memory-to-CPU ratio.</span></span> <span data-ttu-id="2e1b7-121">Idéal pour les serveurs de base de données relationnelle, les caches moyens à grands et l’analytique en mémoire.</span><span class="sxs-lookup"><span data-stu-id="2e1b7-121">Great for relational database servers, medium to large caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="2e1b7-122">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="2e1b7-122">Storage optimized</span></span>](sizes-storage.md)        | <span data-ttu-id="2e1b7-123">Ls</span><span class="sxs-lookup"><span data-stu-id="2e1b7-123">Ls</span></span>                | <span data-ttu-id="2e1b7-124">Débit de disque et E/S élevés.</span><span class="sxs-lookup"><span data-stu-id="2e1b7-124">High disk throughput and IO.</span></span> <span data-ttu-id="2e1b7-125">Idéale pour les bases de données NoSQL, SQL et Big Data.</span><span class="sxs-lookup"><span data-stu-id="2e1b7-125">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="2e1b7-126">GPU</span><span class="sxs-lookup"><span data-stu-id="2e1b7-126">GPU</span></span>](sizes-gpu.md)            | <span data-ttu-id="2e1b7-127">NV, NC</span><span class="sxs-lookup"><span data-stu-id="2e1b7-127">NV, NC</span></span>            | <span data-ttu-id="2e1b7-128">Machines virtuelles spécialisées conçues pour les opérations graphiques lourdes et la retouche vidéo.</span><span class="sxs-lookup"><span data-stu-id="2e1b7-128">Specialized virtual machines targeted for heavy graphic rendering and video editing.</span></span> <span data-ttu-id="2e1b7-129">Disponible avec un ou plusieurs GPU.</span><span class="sxs-lookup"><span data-stu-id="2e1b7-129">Available with single or multiple GPUs.</span></span>       |
| [<span data-ttu-id="2e1b7-130">Calcul haute performance</span><span class="sxs-lookup"><span data-stu-id="2e1b7-130">High performance compute</span></span>](sizes-hpc.md) | <span data-ttu-id="2e1b7-131">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="2e1b7-131">H, A8-11</span></span>          | <span data-ttu-id="2e1b7-132">Nos machines virtuelles les plus rapides et dotées des processeurs les plus puissants avec interfaces réseau haut débit en option (RDMA).</span><span class="sxs-lookup"><span data-stu-id="2e1b7-132">Our fastest and most powerful CPU virtual machines with optional high-throughput network interfaces (RDMA).</span></span> 

<br>

- <span data-ttu-id="2e1b7-133">Pour plus d'informations sur la tarification des différentes tailles, consultez [Tarification des machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="2e1b7-133">For information about pricing of the various sizes, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span> 
- <span data-ttu-id="2e1b7-134">Pour la disponibilité des tailles de machine virtuelle dans les régions Azure, consultez [Disponibilité des produits par région](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="2e1b7-134">For availability of VM sizes in Azure regions, see [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
- <span data-ttu-id="2e1b7-135">Pour connaître les limites générales des machines virtuelles Azure, consultez [Abonnement Azure et limites, quotas et contraintes du service](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="2e1b7-135">To see general limits on Azure VMs, see [Azure subscription and service limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span>
- <span data-ttu-id="2e1b7-136">Lisez-en davantage sur les [Unités de calcul Azure (ACU)](../windows/acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.</span><span class="sxs-lookup"><span data-stu-id="2e1b7-136">Learn more about how [Azure compute units (ACU)](../windows/acu.md) can help you compare compute performance across Azure SKUs.</span></span>


## <a name="rest-api"></a><span data-ttu-id="2e1b7-137">API REST</span><span class="sxs-lookup"><span data-stu-id="2e1b7-137">Rest API</span></span>

<span data-ttu-id="2e1b7-138">Pour plus d’informations sur l’utilisation de l’API REST pour demander la taille des machines virtuelles, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="2e1b7-138">For information on using the REST API to query for VM sizes, see the following:</span></span>

- [<span data-ttu-id="2e1b7-139">Répertorier les tailles disponibles des machines virtuelles pour le redimensionnement</span><span class="sxs-lookup"><span data-stu-id="2e1b7-139">List available virtual machine sizes for resizing</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-for-resizing)
- [<span data-ttu-id="2e1b7-140">Répertorier les tailles disponibles des machines virtuelles pour un abonnement</span><span class="sxs-lookup"><span data-stu-id="2e1b7-140">List available virtual machine sizes for a subscription</span></span>](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)
- [<span data-ttu-id="2e1b7-141">Répertorier les tailles de machine virtuelle disponibles dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="2e1b7-141">List available virtual machine sizes in an availability set</span></span>](
https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-list-sizes-availability-set)

## <a name="acu"></a><span data-ttu-id="2e1b7-142">ACU</span><span class="sxs-lookup"><span data-stu-id="2e1b7-142">ACU</span></span>

<span data-ttu-id="2e1b7-143">Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.</span><span class="sxs-lookup"><span data-stu-id="2e1b7-143">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e1b7-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e1b7-144">Next steps</span></span>

<span data-ttu-id="2e1b7-145">En savoir plus sur les différentes tailles de machines virtuelles qui sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="2e1b7-145">Learn more about the different VM sizes that are available:</span></span>
- [<span data-ttu-id="2e1b7-146">Usage général</span><span class="sxs-lookup"><span data-stu-id="2e1b7-146">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="2e1b7-147">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="2e1b7-147">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="2e1b7-148">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="2e1b7-148">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="2e1b7-149">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="2e1b7-149">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="2e1b7-150">GPU</span><span class="sxs-lookup"><span data-stu-id="2e1b7-150">GPU</span></span>](sizes-gpu.md)
- [<span data-ttu-id="2e1b7-151">Calcul haute performance</span><span class="sxs-lookup"><span data-stu-id="2e1b7-151">High performance compute</span></span>](sizes-hpc.md)



