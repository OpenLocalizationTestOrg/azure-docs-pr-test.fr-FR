---
title: "aaaManage Azure disques avec hello CLI d’Azure | Documents Microsoft"
description: "Didacticiel - gérer les disques Azure avec hello CLI d’Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ad29cfbec5f9738f47705b19d0450c9a2f555492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-hello-azure-cli"></a><span data-ttu-id="1e060-103">Gérer les disques Azure avec hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="1e060-103">Manage Azure disks with hello Azure CLI</span></span>

<span data-ttu-id="1e060-104">Machines virtuelles Azure utilisent le système d’exploitation de disques toostore hello machines virtuelles, des applications et des données.</span><span class="sxs-lookup"><span data-stu-id="1e060-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="1e060-105">Lorsque vous créez une machine virtuelle, il est important toochoose une taille de disque et la charge de travail de configuration approprié toohello attendu.</span><span class="sxs-lookup"><span data-stu-id="1e060-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="1e060-106">Ce didacticiel décrit le déploiement et la gestion des disques de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1e060-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="1e060-107">Vous en apprendrez davantage sur les points suivants :</span><span class="sxs-lookup"><span data-stu-id="1e060-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1e060-108">Disques de système d’exploitation et disques temporaires</span><span class="sxs-lookup"><span data-stu-id="1e060-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="1e060-109">Disques de données</span><span class="sxs-lookup"><span data-stu-id="1e060-109">Data disks</span></span>
> * <span data-ttu-id="1e060-110">Disques Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="1e060-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="1e060-111">Performances des disques</span><span class="sxs-lookup"><span data-stu-id="1e060-111">Disk performance</span></span>
> * <span data-ttu-id="1e060-112">Attachement et préparation des disques de données</span><span class="sxs-lookup"><span data-stu-id="1e060-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="1e060-113">Redimensionnement des disques</span><span class="sxs-lookup"><span data-stu-id="1e060-113">Resizing disks</span></span>
> * <span data-ttu-id="1e060-114">Captures instantanées de disque</span><span class="sxs-lookup"><span data-stu-id="1e060-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1e060-115">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1e060-115">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="1e060-116">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="1e060-116">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1e060-117">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1e060-117">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="1e060-118">Disques Azure par défaut</span><span class="sxs-lookup"><span data-stu-id="1e060-118">Default Azure disks</span></span>

<span data-ttu-id="1e060-119">Création d’une machine virtuelle Azure, deux disques sont automatiquement attaché toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1e060-119">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="1e060-120">**Disque de système d’exploitation** - disques de système d’exploitation peuvent être dimensionnés des téraoctets de too1 et hôtes hello de système d’exploitation de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="1e060-120">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span> <span data-ttu-id="1e060-121">disque de Hello du système d’exploitation est étiqueté */dev/sda* par défaut.</span><span class="sxs-lookup"><span data-stu-id="1e060-121">hello OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="1e060-122">disque Hello mise en cache de la configuration du disque du système d’exploitation hello est optimisé pour les performances du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="1e060-122">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="1e060-123">En raison de cette configuration, hello disque de système d’exploitation **ne doivent pas** héberger des applications ou des données.</span><span class="sxs-lookup"><span data-stu-id="1e060-123">Because of this configuration, hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="1e060-124">Pour héberger ce type de contenu, utilisez plutôt des disques de données, qui sont décrits plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="1e060-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="1e060-125">**Disque temporaire** -les disques temporaires utilisent un disque SSD qui se trouve sur hello même hôte Azure en tant que machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="1e060-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="1e060-126">Les disques temporaires sont extrêmement performants et peuvent être utilisés pour des opérations telles que le traitement de données temporaires.</span><span class="sxs-lookup"><span data-stu-id="1e060-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="1e060-127">Toutefois, si hello machine virtuelle est déplacée tooa nouvel hôte, toutes les données stockées sur un disque temporaire sont supprimées.</span><span class="sxs-lookup"><span data-stu-id="1e060-127">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="1e060-128">taille de Hello du disque temporaire de hello est déterminé par hello taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1e060-128">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="1e060-129">Les disques temporaires sont nommés */dev/sdb* et ont un point de montage */mnt*.</span><span class="sxs-lookup"><span data-stu-id="1e060-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="1e060-130">Tailles du disque temporaire</span><span class="sxs-lookup"><span data-stu-id="1e060-130">Temporary disk sizes</span></span>

| <span data-ttu-id="1e060-131">Type</span><span class="sxs-lookup"><span data-stu-id="1e060-131">Type</span></span> | <span data-ttu-id="1e060-132">Taille de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1e060-132">VM Size</span></span> | <span data-ttu-id="1e060-133">Taille maximale du disque temporaire (Go)</span><span class="sxs-lookup"><span data-stu-id="1e060-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="1e060-134">Usage général</span><span class="sxs-lookup"><span data-stu-id="1e060-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="1e060-135">Séries A et D</span><span class="sxs-lookup"><span data-stu-id="1e060-135">A and D series</span></span> | <span data-ttu-id="1e060-136">800</span><span class="sxs-lookup"><span data-stu-id="1e060-136">800</span></span> |
| [<span data-ttu-id="1e060-137">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="1e060-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="1e060-138">Série F</span><span class="sxs-lookup"><span data-stu-id="1e060-138">F series</span></span> | <span data-ttu-id="1e060-139">800</span><span class="sxs-lookup"><span data-stu-id="1e060-139">800</span></span> |
| [<span data-ttu-id="1e060-140">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="1e060-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="1e060-141">Séries D et G</span><span class="sxs-lookup"><span data-stu-id="1e060-141">D and G series</span></span> | <span data-ttu-id="1e060-142">6144</span><span class="sxs-lookup"><span data-stu-id="1e060-142">6144</span></span> |
| [<span data-ttu-id="1e060-143">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="1e060-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="1e060-144">Série L</span><span class="sxs-lookup"><span data-stu-id="1e060-144">L series</span></span> | <span data-ttu-id="1e060-145">5630</span><span class="sxs-lookup"><span data-stu-id="1e060-145">5630</span></span> |
| [<span data-ttu-id="1e060-146">GPU</span><span class="sxs-lookup"><span data-stu-id="1e060-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="1e060-147">Série N</span><span class="sxs-lookup"><span data-stu-id="1e060-147">N series</span></span> | <span data-ttu-id="1e060-148">1 440</span><span class="sxs-lookup"><span data-stu-id="1e060-148">1440</span></span> |
| [<span data-ttu-id="1e060-149">Hautes performances</span><span class="sxs-lookup"><span data-stu-id="1e060-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="1e060-150">Séries A et H</span><span class="sxs-lookup"><span data-stu-id="1e060-150">A and H series</span></span> | <span data-ttu-id="1e060-151">2000</span><span class="sxs-lookup"><span data-stu-id="1e060-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="1e060-152">Disques de données Azure</span><span class="sxs-lookup"><span data-stu-id="1e060-152">Azure data disks</span></span>

<span data-ttu-id="1e060-153">Des disques de données supplémentaires peuvent être ajoutés pour installer des applications et stocker des données.</span><span class="sxs-lookup"><span data-stu-id="1e060-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="1e060-154">Les disques de données doivent être utilisés dans les cas où un stockage des données durable et réactif est souhaité.</span><span class="sxs-lookup"><span data-stu-id="1e060-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="1e060-155">Chaque disque de données possède une capacité maximale de 1 To.</span><span class="sxs-lookup"><span data-stu-id="1e060-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="1e060-156">taille de Hello de machine virtuelle de hello détermine le nombre de disques de données peut être attaché tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1e060-156">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="1e060-157">Pour chaque cœur de la machine virtuelle, deux disques de données peuvent être attachés.</span><span class="sxs-lookup"><span data-stu-id="1e060-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="1e060-158">Disques de données max. par machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1e060-158">Max data disks per VM</span></span>

| <span data-ttu-id="1e060-159">Type</span><span class="sxs-lookup"><span data-stu-id="1e060-159">Type</span></span> | <span data-ttu-id="1e060-160">Taille de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1e060-160">VM Size</span></span> | <span data-ttu-id="1e060-161">Disques de données max. par machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1e060-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="1e060-162">Usage général</span><span class="sxs-lookup"><span data-stu-id="1e060-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="1e060-163">Séries A et D</span><span class="sxs-lookup"><span data-stu-id="1e060-163">A and D series</span></span> | <span data-ttu-id="1e060-164">32</span><span class="sxs-lookup"><span data-stu-id="1e060-164">32</span></span> |
| [<span data-ttu-id="1e060-165">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="1e060-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="1e060-166">Série F</span><span class="sxs-lookup"><span data-stu-id="1e060-166">F series</span></span> | <span data-ttu-id="1e060-167">32</span><span class="sxs-lookup"><span data-stu-id="1e060-167">32</span></span> |
| [<span data-ttu-id="1e060-168">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="1e060-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="1e060-169">Séries D et G</span><span class="sxs-lookup"><span data-stu-id="1e060-169">D and G series</span></span> | <span data-ttu-id="1e060-170">64</span><span class="sxs-lookup"><span data-stu-id="1e060-170">64</span></span> |
| [<span data-ttu-id="1e060-171">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="1e060-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="1e060-172">Série L</span><span class="sxs-lookup"><span data-stu-id="1e060-172">L series</span></span> | <span data-ttu-id="1e060-173">64</span><span class="sxs-lookup"><span data-stu-id="1e060-173">64</span></span> |
| [<span data-ttu-id="1e060-174">GPU</span><span class="sxs-lookup"><span data-stu-id="1e060-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="1e060-175">Série N</span><span class="sxs-lookup"><span data-stu-id="1e060-175">N series</span></span> | <span data-ttu-id="1e060-176">48</span><span class="sxs-lookup"><span data-stu-id="1e060-176">48</span></span> |
| [<span data-ttu-id="1e060-177">Hautes performances</span><span class="sxs-lookup"><span data-stu-id="1e060-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="1e060-178">Séries A et H</span><span class="sxs-lookup"><span data-stu-id="1e060-178">A and H series</span></span> | <span data-ttu-id="1e060-179">32</span><span class="sxs-lookup"><span data-stu-id="1e060-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="1e060-180">Type de disque de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1e060-180">VM disk types</span></span>

<span data-ttu-id="1e060-181">Azure propose deux types de disque.</span><span class="sxs-lookup"><span data-stu-id="1e060-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="1e060-182">Disque Standard</span><span class="sxs-lookup"><span data-stu-id="1e060-182">Standard disk</span></span>

<span data-ttu-id="1e060-183">Le stockage Standard s’appuie sur des disques durs et offre un stockage économique qui n’en est pas moins performant.</span><span class="sxs-lookup"><span data-stu-id="1e060-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="1e060-184">Les disques Standard constituent la solution idéale pour une charge de travail de développement et de test économique.</span><span class="sxs-lookup"><span data-stu-id="1e060-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="1e060-185">Disque Premium</span><span class="sxs-lookup"><span data-stu-id="1e060-185">Premium disk</span></span>

<span data-ttu-id="1e060-186">Les disques Premium reposent sur un disque SSD à faible latence et hautes performances.</span><span class="sxs-lookup"><span data-stu-id="1e060-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="1e060-187">Ils conviennent parfaitement aux machines virtuelles exécutant une charge de travail en production.</span><span class="sxs-lookup"><span data-stu-id="1e060-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="1e060-188">Le stockage Premium prend en charge les machines virtuelles des séries DS, DSv2, GS et FS.</span><span class="sxs-lookup"><span data-stu-id="1e060-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="1e060-189">Les disques Premium sont fournis dans les trois types (P10, P20, P30), taille hello du disque de hello détermine le type de disque hello.</span><span class="sxs-lookup"><span data-stu-id="1e060-189">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="1e060-190">Lors de la sélection, une valeur de hello de taille de disque est arrondie toohello les type suivant.</span><span class="sxs-lookup"><span data-stu-id="1e060-190">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="1e060-191">Par exemple, si la taille du disque hello est inférieure à 128 Go, le type de disque hello est P10.</span><span class="sxs-lookup"><span data-stu-id="1e060-191">For example, if hello disk size is less than 128 GB, hello disk type is P10.</span></span> <span data-ttu-id="1e060-192">Si la taille du disque hello est comprise entre 129 et 512 Go, taille de hello est un P20.</span><span class="sxs-lookup"><span data-stu-id="1e060-192">If hello disk size is between 129 GB and 512 GB, hello size is a P20.</span></span> <span data-ttu-id="1e060-193">Tout élément plus de 512 Go, taille de hello est un P30.</span><span class="sxs-lookup"><span data-stu-id="1e060-193">Anything over 512 GB, hello size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="1e060-194">Performances du disque Premium</span><span class="sxs-lookup"><span data-stu-id="1e060-194">Premium disk performance</span></span>

|<span data-ttu-id="1e060-195">Type de disque de stockage Premium</span><span class="sxs-lookup"><span data-stu-id="1e060-195">Premium storage disk type</span></span> | <span data-ttu-id="1e060-196">P10</span><span class="sxs-lookup"><span data-stu-id="1e060-196">P10</span></span> | <span data-ttu-id="1e060-197">P20</span><span class="sxs-lookup"><span data-stu-id="1e060-197">P20</span></span> | <span data-ttu-id="1e060-198">P30</span><span class="sxs-lookup"><span data-stu-id="1e060-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1e060-199">Taille du disque (arrondie)</span><span class="sxs-lookup"><span data-stu-id="1e060-199">Disk size (round up)</span></span> | <span data-ttu-id="1e060-200">128 Go</span><span class="sxs-lookup"><span data-stu-id="1e060-200">128 GB</span></span> | <span data-ttu-id="1e060-201">512 Go</span><span class="sxs-lookup"><span data-stu-id="1e060-201">512 GB</span></span> | <span data-ttu-id="1e060-202">1 024 Go (1 To)</span><span class="sxs-lookup"><span data-stu-id="1e060-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="1e060-203">Nb max. d'E/S par seconde par disque</span><span class="sxs-lookup"><span data-stu-id="1e060-203">Max IOPS per disk</span></span> | <span data-ttu-id="1e060-204">500</span><span class="sxs-lookup"><span data-stu-id="1e060-204">500</span></span> | <span data-ttu-id="1e060-205">2 300</span><span class="sxs-lookup"><span data-stu-id="1e060-205">2,300</span></span> | <span data-ttu-id="1e060-206">5 000</span><span class="sxs-lookup"><span data-stu-id="1e060-206">5,000</span></span> |
<span data-ttu-id="1e060-207">Débit par disque</span><span class="sxs-lookup"><span data-stu-id="1e060-207">Throughput per disk</span></span> | <span data-ttu-id="1e060-208">100 Mo/s</span><span class="sxs-lookup"><span data-stu-id="1e060-208">100 MB/s</span></span> | <span data-ttu-id="1e060-209">150 Mo/s</span><span class="sxs-lookup"><span data-stu-id="1e060-209">150 MB/s</span></span> | <span data-ttu-id="1e060-210">200 Mo/s</span><span class="sxs-lookup"><span data-stu-id="1e060-210">200 MB/s</span></span> |

<span data-ttu-id="1e060-211">Tandis que hello au-dessus de table identifie max IOPS par disque, un niveau plus élevé de performances est possible par l’agrégation de plusieurs disques de données.</span><span class="sxs-lookup"><span data-stu-id="1e060-211">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="1e060-212">Par exemple, une machine virtuelle Standard_GS5 peut atteindre un nombre maximum d’E/S par seconde de 80 000.</span><span class="sxs-lookup"><span data-stu-id="1e060-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="1e060-213">Pour plus d’informations sur le nombre max. d’E/S par seconde par machine virtuelle, consultez [Tailles des machines virtuelles Linux dans Azure](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="1e060-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="1e060-214">Créer et attacher des disques</span><span class="sxs-lookup"><span data-stu-id="1e060-214">Create and attach disks</span></span>

<span data-ttu-id="1e060-215">Disques de données peuvent être créés et attachés au moment de la création de machine virtuelle ou tooan existant de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1e060-215">Data disks can be created and attached at VM creation time or tooan existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="1e060-216">Attacher le disque lors de la création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1e060-216">Attach disk at VM creation</span></span>

<span data-ttu-id="1e060-217">Créer un groupe de ressources avec hello [création de groupe de az](https://docs.microsoft.com/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="1e060-217">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="1e060-218">Créer une machine virtuelle à l’aide de hello [az vm créer]( /cli/azure/vm#create) commande.</span><span class="sxs-lookup"><span data-stu-id="1e060-218">Create a VM using hello [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="1e060-219">Hello `--datadisk-sizes-gb` argument est utilisé toospecify qu’un disque supplémentaire doit être créé et attaché toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1e060-219">hello `--datadisk-sizes-gb` argument is used toospecify that an additional disk should be created and attached toohello virtual machine.</span></span> <span data-ttu-id="1e060-220">toocreate et attacher plusieurs disques, utilisez une liste délimitée par l’espace de valeurs de taille de disque.</span><span class="sxs-lookup"><span data-stu-id="1e060-220">toocreate and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="1e060-221">Bonjour l’exemple suivant, un ordinateur virtuel est créé avec des disques de données de deux, les deux 128 Go.</span><span class="sxs-lookup"><span data-stu-id="1e060-221">In hello following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="1e060-222">Les tailles de disque hello étant 128 Go, ces disques sont tous deux configurés en tant que P10s, qui fournissent des 500 IOPS maximales par disque.</span><span class="sxs-lookup"><span data-stu-id="1e060-222">Because hello disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-tooexisting-vm"></a><span data-ttu-id="1e060-223">Attacher le disque tooexisting machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1e060-223">Attach disk tooexisting VM</span></span>

<span data-ttu-id="1e060-224">toocreate et attacher une disque tooan existant machine virtuelle, utilisez hello [attacher de disque de machine virtuelle az](/cli/azure/vm/disk#attach) commande.</span><span class="sxs-lookup"><span data-stu-id="1e060-224">toocreate and attach a new disk tooan existing virtual machine, use hello [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="1e060-225">Hello exemple suivant crée un disque premium, 128 Go de taille et l’attache toohello que machine virtuelle créée dans la dernière étape de hello.</span><span class="sxs-lookup"><span data-stu-id="1e060-225">hello following example creates a premium disk, 128 gigabytes in size, and attaches it toohello VM created in hello last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="1e060-226">Préparer les disques de données</span><span class="sxs-lookup"><span data-stu-id="1e060-226">Prepare data disks</span></span>

<span data-ttu-id="1e060-227">Une fois qu’un disque a été attaché toohello virtual machine, le système d’exploitation de hello doit toobe configuré toouse hello disque.</span><span class="sxs-lookup"><span data-stu-id="1e060-227">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="1e060-228">Bonjour à l’exemple suivant montre comment toomanually configurer un disque.</span><span class="sxs-lookup"><span data-stu-id="1e060-228">hello following example shows how toomanually configure a disk.</span></span> <span data-ttu-id="1e060-229">Ce processus peut également être automatisé à l’aide de cloud-init, qui est présenté dans un [prochain didacticiel](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="1e060-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="1e060-230">Configuration manuelle</span><span class="sxs-lookup"><span data-stu-id="1e060-230">Manual configuration</span></span>

<span data-ttu-id="1e060-231">Créer une connexion SSH avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="1e060-231">Create an SSH connection with hello virtual machine.</span></span> <span data-ttu-id="1e060-232">Remplacez l’exemple d’adresse IP hello avec l’adresse IP publique de l’ordinateur virtuel de hello hello.</span><span class="sxs-lookup"><span data-stu-id="1e060-232">Replace hello example IP address with hello public IP of hello virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="1e060-233">Partition de disque hello avec `fdisk`.</span><span class="sxs-lookup"><span data-stu-id="1e060-233">Partition hello disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="1e060-234">Écrire une partition toohello à l’aide de hello `mkfs` commande.</span><span class="sxs-lookup"><span data-stu-id="1e060-234">Write a file system toohello partition by using hello `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="1e060-235">Monter le disque de nouveau hello afin qu’il soit accessible dans le système d’exploitation de hello.</span><span class="sxs-lookup"><span data-stu-id="1e060-235">Mount hello new disk so that it is accessible in hello operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="1e060-236">disque de Hello sont maintenant accessibles via hello *datadrive* point de montage, ce qui peut être vérifié en exécutant hello `df -h` commande.</span><span class="sxs-lookup"><span data-stu-id="1e060-236">hello disk can now be accessed through hello *datadrive* mountpoint, which can be verified by running hello `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="1e060-237">sortie de Hello affiche hello nouveau lecteur monté sur */datadrive*.</span><span class="sxs-lookup"><span data-stu-id="1e060-237">hello output shows hello new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="1e060-238">tooensure qui hello lecteur est remontée après un redémarrage, il doit être ajouté toohello */etc/fstab* fichier.</span><span class="sxs-lookup"><span data-stu-id="1e060-238">tooensure that hello drive is remounted after a reboot, it must be added toohello */etc/fstab* file.</span></span> <span data-ttu-id="1e060-239">toodo par conséquent, obtenir hello UUID de disque de hello avec hello `blkid` utilitaire.</span><span class="sxs-lookup"><span data-stu-id="1e060-239">toodo so, get hello UUID of hello disk with hello `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="1e060-240">sortie de Hello affiche hello UUID du lecteur de hello `/dev/sdc1` dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="1e060-240">hello output displays hello UUID of hello drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="1e060-241">Ajouter un toohello similaire de ligne suivant toohello */etc/fstab* fichier.</span><span class="sxs-lookup"><span data-stu-id="1e060-241">Add a line similar toohello following toohello */etc/fstab* file.</span></span> <span data-ttu-id="1e060-242">Notez également que la fonctionnalité permettant d’écrire des barrières peut être désactivée à l’aide de *barrier=0*, cette configuration peut améliorer les performances de disque.</span><span class="sxs-lookup"><span data-stu-id="1e060-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="1e060-243">Maintenant que hello disque a été configuré, fermez la session SSH de hello.</span><span class="sxs-lookup"><span data-stu-id="1e060-243">Now that hello disk has been configured, close hello SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="1e060-244">Redimensionner le disque de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1e060-244">Resize VM disk</span></span>

<span data-ttu-id="1e060-245">Une fois qu’un ordinateur virtuel a été déployé, disque de système d’exploitation hello ou les disques de données attaché peuvent être augmentées la taille.</span><span class="sxs-lookup"><span data-stu-id="1e060-245">Once a VM has been deployed, hello operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="1e060-246">L’augmentation de taille hello d’un disque est utile lorsque vous avez besoin de davantage d’espace de stockage ou un niveau plus élevé de performances (P10, P20, P30).</span><span class="sxs-lookup"><span data-stu-id="1e060-246">Increasing hello size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="1e060-247">Notez que vous ne pouvez pas réduire la taille des disques.</span><span class="sxs-lookup"><span data-stu-id="1e060-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="1e060-248">Avant d’augmenter la taille du disque, hello Id ou nom du disque de hello est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1e060-248">Before increasing disk size, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="1e060-249">Hello d’utilisation [liste des disques az](/cli/azure/vm/disk#list) tooreturn commande tous les disques dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1e060-249">Use hello [az disk list](/cli/azure/vm/disk#list) command tooreturn all disks in a resource group.</span></span> <span data-ttu-id="1e060-250">Prenez note du nom du disque hello que vous aimeriez tooresize.</span><span class="sxs-lookup"><span data-stu-id="1e060-250">Take note of hello disk name that you would like tooresize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="1e060-251">Hello machine virtuelle doit également être libéré.</span><span class="sxs-lookup"><span data-stu-id="1e060-251">hello VM must also be deallocated.</span></span> <span data-ttu-id="1e060-252">Hello d’utilisation [az vm désallouer]( /cli/azure/vm#deallocate) commande toostop et désallouer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1e060-252">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="1e060-253">Hello d’utilisation [mise à jour du disque az](/cli/azure/vm/disk#update) disque de commande tooresize hello.</span><span class="sxs-lookup"><span data-stu-id="1e060-253">Use hello [az disk update](/cli/azure/vm/disk#update) command tooresize hello disk.</span></span> <span data-ttu-id="1e060-254">Cet exemple redimensionne un disque nommé *myDataDisk* too1 téraoctet.</span><span class="sxs-lookup"><span data-stu-id="1e060-254">This example resizes a disk named *myDataDisk* too1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="1e060-255">Une fois l’opération de redimensionnement hello terminée, démarrer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1e060-255">Once hello resize operation has completed, start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="1e060-256">Si vous avez redimensionné hello d’exploitation du disque système, partition de hello est automatiquement développé.</span><span class="sxs-lookup"><span data-stu-id="1e060-256">If you’ve resized hello operating system disk, hello partition is automatically be expanded.</span></span> <span data-ttu-id="1e060-257">Si vous avez redimensionné un disque de données, toutes les partitions en cours doivent toobe développée dans le système d’exploitation de machines virtuelles hello.</span><span class="sxs-lookup"><span data-stu-id="1e060-257">If you have resized a data disk, any current partitions need toobe expanded in hello VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="1e060-258">Prendre une capture instantanée des disques Azure</span><span class="sxs-lookup"><span data-stu-id="1e060-258">Snapshot Azure disks</span></span>

<span data-ttu-id="1e060-259">Un instantané de disque crée une copie uniquement, point-à-temps lecture du disque de hello.</span><span class="sxs-lookup"><span data-stu-id="1e060-259">Taking a disk snapshot creates a read only, point-in-time copy of hello disk.</span></span> <span data-ttu-id="1e060-260">Les instantanés de machine virtuelle Azure sont utiles pour rapidement enregistrer l’état de hello d’une machine virtuelle avant d’apporter des modifications de configuration.</span><span class="sxs-lookup"><span data-stu-id="1e060-260">Azure VM snapshots are useful for quickly saving hello state of a VM before making configuration changes.</span></span> <span data-ttu-id="1e060-261">En cas de hello hello modifications de configuration révèle toobe indésirables, état de la machine virtuelle peut être restaurée à l’aide de la capture instantanée de hello.</span><span class="sxs-lookup"><span data-stu-id="1e060-261">In hello event hello configuration changes prove toobe undesired, VM state can be restored using hello snapshot.</span></span> <span data-ttu-id="1e060-262">Lorsqu’un ordinateur virtuel possède plusieurs disques, un instantané de chaque disque indépendamment hello d’autres.</span><span class="sxs-lookup"><span data-stu-id="1e060-262">When a VM has more than one disk, a snapshot is taken of each disk independently of hello others.</span></span> <span data-ttu-id="1e060-263">Pour effectuer des sauvegardes cohérentes d’application, envisagez l’arrêt hello machine virtuelle avant d’effectuer des captures instantanées de disque.</span><span class="sxs-lookup"><span data-stu-id="1e060-263">For taking application consistent backups, consider stopping hello VM before taking disk snapshots.</span></span> <span data-ttu-id="1e060-264">Vous pouvez également utiliser hello [service Azure Backup](/azure/backup/), qui permet aux vous tooperform automatisée sauvegardes hello machine virtuelle est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1e060-264">Alternatively, use hello [Azure Backup service](/azure/backup/), which enables you tooperform automated backups while hello VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="1e060-265">Création d’un instantané</span><span class="sxs-lookup"><span data-stu-id="1e060-265">Create snapshot</span></span>

<span data-ttu-id="1e060-266">Avant de créer un instantané de disque de machine virtuelle, hello Id ou nom de disque de hello est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1e060-266">Before creating a virtual machine disk snapshot, hello Id or name of hello disk is needed.</span></span> <span data-ttu-id="1e060-267">Hello d’utilisation [afficher de machine virtuelle az](https://docs.microsoft.com/en-us/cli/azure/vm#show) id de commande tooreturn hello disque. Dans cet exemple, l’id du disque hello est stocké dans une variable afin qu’il peut être utilisé dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1e060-267">Use hello [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command tooreturn hello disk id. In this example, hello disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="1e060-268">Maintenant que vous avez id hello du disque de machine virtuelle hello, hello commande suivante crée un instantané du disque de hello.</span><span class="sxs-lookup"><span data-stu-id="1e060-268">Now that you have hello id of hello virtual machine disk, hello following command creates a snapshot of hello disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="1e060-269">Création d’un disque à partir d’une capture instantanée</span><span class="sxs-lookup"><span data-stu-id="1e060-269">Create disk from snapshot</span></span>

<span data-ttu-id="1e060-270">Cet instantané peut ensuite être converti en un disque, ce qui peut être utilisé toorecreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1e060-270">This snapshot can then be converted into a disk, which can be used toorecreate hello virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="1e060-271">Restauration de la machine virtuelle à partir de l’instantané</span><span class="sxs-lookup"><span data-stu-id="1e060-271">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="1e060-272">récupération de machine virtuelle toodemonstrate, ordinateur virtuel existant de suppression hello.</span><span class="sxs-lookup"><span data-stu-id="1e060-272">toodemonstrate virtual machine recovery, delete hello existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="1e060-273">Créer un nouvel ordinateur virtuel à partir du disque de capture instantanée hello.</span><span class="sxs-lookup"><span data-stu-id="1e060-273">Create a new virtual machine from hello snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="1e060-274">Rattacher un disque de données</span><span class="sxs-lookup"><span data-stu-id="1e060-274">Reattach data disk</span></span>

<span data-ttu-id="1e060-275">Tous les disques de données doivent toobe rattaché toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1e060-275">All data disks need toobe reattached toohello virtual machine.</span></span>

<span data-ttu-id="1e060-276">Tout d’abord rechercher nom hello de disque de données à l’aide de hello [liste des disques az](https://docs.microsoft.com/cli/azure/disk#list) commande.</span><span class="sxs-lookup"><span data-stu-id="1e060-276">First find hello data disk name using hello [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="1e060-277">Cet exemple place hello nom du disque hello dans une variable nommée *datadisk*, qui est utilisé dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="1e060-277">This example places hello name of hello disk in a variable named *datadisk*, which is used in hello next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="1e060-278">Hello d’utilisation [attacher de disque de machine virtuelle az](https://docs.microsoft.com/cli/azure/vm/disk#attach) disque de commande tooattach hello.</span><span class="sxs-lookup"><span data-stu-id="1e060-278">Use hello [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command tooattach hello disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="1e060-279">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1e060-279">Next steps</span></span>

<span data-ttu-id="1e060-280">Ce didacticiel vous a apporté des connaissances concernant les disques de machine virtuelle, notamment concernant les points suivants :</span><span class="sxs-lookup"><span data-stu-id="1e060-280">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1e060-281">Disques de système d’exploitation et disques temporaires</span><span class="sxs-lookup"><span data-stu-id="1e060-281">OS disks and temporary disks</span></span>
> * <span data-ttu-id="1e060-282">Disques de données</span><span class="sxs-lookup"><span data-stu-id="1e060-282">Data disks</span></span>
> * <span data-ttu-id="1e060-283">Disques Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="1e060-283">Standard and Premium disks</span></span>
> * <span data-ttu-id="1e060-284">Performances des disques</span><span class="sxs-lookup"><span data-stu-id="1e060-284">Disk performance</span></span>
> * <span data-ttu-id="1e060-285">Attachement et préparation des disques de données</span><span class="sxs-lookup"><span data-stu-id="1e060-285">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="1e060-286">Redimensionnement des disques</span><span class="sxs-lookup"><span data-stu-id="1e060-286">Resizing disks</span></span>
> * <span data-ttu-id="1e060-287">Captures instantanées de disque</span><span class="sxs-lookup"><span data-stu-id="1e060-287">Disk snapshots</span></span>

<span data-ttu-id="1e060-288">Avance toohello toolearn de didacticiel suivant sur l’automatisation de configuration d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="1e060-288">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1e060-289">Automatiser la configuration de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1e060-289">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
