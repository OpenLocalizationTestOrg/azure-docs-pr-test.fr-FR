---
title: "Gestion des disques Azure avec l’interface de ligne de commande Azure | Microsoft Docs"
description: "Didacticiel - Gestion des disques Azure avec l’interface de ligne de commande Azure"
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
ms.openlocfilehash: d77dd2b44dca8cee6fa2e93e79cda76c80ccfe1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-the-azure-cli"></a><span data-ttu-id="fb160-103">Gestion des disques Azure avec l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="fb160-103">Manage Azure disks with the Azure CLI</span></span>

<span data-ttu-id="fb160-104">Les machines virtuelles utilisent des disques pour stocker leur système d’exploitation, leurs applications et leurs données.</span><span class="sxs-lookup"><span data-stu-id="fb160-104">Azure virtual machines use disks to store the VMs operating system, applications, and data.</span></span> <span data-ttu-id="fb160-105">Lorsque vous créez une machine virtuelle, il est important de choisir une taille de disque et une configuration appropriées à la charge de travail prévue.</span><span class="sxs-lookup"><span data-stu-id="fb160-105">When creating a VM it is important to choose a disk size and configuration appropriate to the expected workload.</span></span> <span data-ttu-id="fb160-106">Ce didacticiel décrit le déploiement et la gestion des disques de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fb160-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="fb160-107">Vous en apprendrez davantage sur les points suivants :</span><span class="sxs-lookup"><span data-stu-id="fb160-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fb160-108">Disques de système d’exploitation et disques temporaires</span><span class="sxs-lookup"><span data-stu-id="fb160-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="fb160-109">Disques de données</span><span class="sxs-lookup"><span data-stu-id="fb160-109">Data disks</span></span>
> * <span data-ttu-id="fb160-110">Disques Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="fb160-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="fb160-111">Performances des disques</span><span class="sxs-lookup"><span data-stu-id="fb160-111">Disk performance</span></span>
> * <span data-ttu-id="fb160-112">Attachement et préparation des disques de données</span><span class="sxs-lookup"><span data-stu-id="fb160-112">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="fb160-113">Redimensionnement des disques</span><span class="sxs-lookup"><span data-stu-id="fb160-113">Resizing disks</span></span>
> * <span data-ttu-id="fb160-114">Captures instantanées de disque</span><span class="sxs-lookup"><span data-stu-id="fb160-114">Disk snapshots</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fb160-115">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter l’interface de ligne de commande Azure version 2.0.4 ou une version ultérieure pour poursuivre la procédure décrite dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="fb160-115">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="fb160-116">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="fb160-116">Run `az --version` to find the version.</span></span> <span data-ttu-id="fb160-117">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fb160-117">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="default-azure-disks"></a><span data-ttu-id="fb160-118">Disques Azure par défaut</span><span class="sxs-lookup"><span data-stu-id="fb160-118">Default Azure disks</span></span>

<span data-ttu-id="fb160-119">Lorsqu’une machine virtuelle Azure est créée, deux disques sont automatiquement attachés à celle-ci.</span><span class="sxs-lookup"><span data-stu-id="fb160-119">When an Azure virtual machine is created, two disks are automatically attached to the virtual machine.</span></span> 

<span data-ttu-id="fb160-120">**Disque de système d’exploitation** : la taille des disques de système d’exploitation peut atteindre 1 To ; ces disques hébergent le système d’exploitation des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="fb160-120">**Operating system disk** - Operating system disks can be sized up to 1 terabyte, and hosts the VMs operating system.</span></span> <span data-ttu-id="fb160-121">Le disque de système d’exploitation est nommé */dev/sda* par défaut.</span><span class="sxs-lookup"><span data-stu-id="fb160-121">The OS disk is labeled */dev/sda* by default.</span></span> <span data-ttu-id="fb160-122">La configuration de la mise en cache de disque de système d’exploitation est optimisée pour les performances du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="fb160-122">The disk caching configuration of the OS disk is optimized for OS performance.</span></span> <span data-ttu-id="fb160-123">En raison de cette configuration, le disque de système d’exploitation **ne doit pas** héberger d’applications ou de données.</span><span class="sxs-lookup"><span data-stu-id="fb160-123">Because of this configuration, the OS disk **should not** host applications or data.</span></span> <span data-ttu-id="fb160-124">Pour héberger ce type de contenu, utilisez plutôt des disques de données, qui sont décrits plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="fb160-124">For applications and data, use data disks, which are detailed later in this article.</span></span> 

<span data-ttu-id="fb160-125">**Disque temporaire** : les disques temporaires utilisent un disque SSD qui se trouve sur le même hôte Azure que la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fb160-125">**Temporary disk** - Temporary disks use a solid-state drive that is located on the same Azure host as the VM.</span></span> <span data-ttu-id="fb160-126">Les disques temporaires sont extrêmement performants et peuvent être utilisés pour des opérations telles que le traitement de données temporaires.</span><span class="sxs-lookup"><span data-stu-id="fb160-126">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="fb160-127">Toutefois, si la machine virtuelle est déplacée vers un nouvel hôte, toutes les données stockées sur un disque temporaire sont supprimées.</span><span class="sxs-lookup"><span data-stu-id="fb160-127">However, if the VM is moved to a new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="fb160-128">La taille du disque temporaire est déterminée par la taille de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fb160-128">The size of the temporary disk is determined by the VM size.</span></span> <span data-ttu-id="fb160-129">Les disques temporaires sont nommés */dev/sdb* et ont un point de montage */mnt*.</span><span class="sxs-lookup"><span data-stu-id="fb160-129">Temporary disks are labeled */dev/sdb* and have a mountpoint of */mnt*.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="fb160-130">Tailles du disque temporaire</span><span class="sxs-lookup"><span data-stu-id="fb160-130">Temporary disk sizes</span></span>

| <span data-ttu-id="fb160-131">Type</span><span class="sxs-lookup"><span data-stu-id="fb160-131">Type</span></span> | <span data-ttu-id="fb160-132">Taille de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="fb160-132">VM Size</span></span> | <span data-ttu-id="fb160-133">Taille maximale du disque temporaire (Go)</span><span class="sxs-lookup"><span data-stu-id="fb160-133">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="fb160-134">Usage général</span><span class="sxs-lookup"><span data-stu-id="fb160-134">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="fb160-135">Séries A et D</span><span class="sxs-lookup"><span data-stu-id="fb160-135">A and D series</span></span> | <span data-ttu-id="fb160-136">800</span><span class="sxs-lookup"><span data-stu-id="fb160-136">800</span></span> |
| [<span data-ttu-id="fb160-137">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="fb160-137">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="fb160-138">Série F</span><span class="sxs-lookup"><span data-stu-id="fb160-138">F series</span></span> | <span data-ttu-id="fb160-139">800</span><span class="sxs-lookup"><span data-stu-id="fb160-139">800</span></span> |
| [<span data-ttu-id="fb160-140">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="fb160-140">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="fb160-141">Séries D et G</span><span class="sxs-lookup"><span data-stu-id="fb160-141">D and G series</span></span> | <span data-ttu-id="fb160-142">6144</span><span class="sxs-lookup"><span data-stu-id="fb160-142">6144</span></span> |
| [<span data-ttu-id="fb160-143">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="fb160-143">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="fb160-144">Série L</span><span class="sxs-lookup"><span data-stu-id="fb160-144">L series</span></span> | <span data-ttu-id="fb160-145">5630</span><span class="sxs-lookup"><span data-stu-id="fb160-145">5630</span></span> |
| [<span data-ttu-id="fb160-146">GPU</span><span class="sxs-lookup"><span data-stu-id="fb160-146">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="fb160-147">Série N</span><span class="sxs-lookup"><span data-stu-id="fb160-147">N series</span></span> | <span data-ttu-id="fb160-148">1 440</span><span class="sxs-lookup"><span data-stu-id="fb160-148">1440</span></span> |
| [<span data-ttu-id="fb160-149">Hautes performances</span><span class="sxs-lookup"><span data-stu-id="fb160-149">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="fb160-150">Séries A et H</span><span class="sxs-lookup"><span data-stu-id="fb160-150">A and H series</span></span> | <span data-ttu-id="fb160-151">2000</span><span class="sxs-lookup"><span data-stu-id="fb160-151">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="fb160-152">Disques de données Azure</span><span class="sxs-lookup"><span data-stu-id="fb160-152">Azure data disks</span></span>

<span data-ttu-id="fb160-153">Des disques de données supplémentaires peuvent être ajoutés pour installer des applications et stocker des données.</span><span class="sxs-lookup"><span data-stu-id="fb160-153">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="fb160-154">Les disques de données doivent être utilisés dans les cas où un stockage des données durable et réactif est souhaité.</span><span class="sxs-lookup"><span data-stu-id="fb160-154">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="fb160-155">Chaque disque de données possède une capacité maximale de 1 To.</span><span class="sxs-lookup"><span data-stu-id="fb160-155">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="fb160-156">La taille de la machine virtuelle détermine le nombre de disques de données pouvant être attachés à cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fb160-156">The size of the virtual machine determines how many data disks can be attached to a VM.</span></span> <span data-ttu-id="fb160-157">Pour chaque cœur de la machine virtuelle, deux disques de données peuvent être attachés.</span><span class="sxs-lookup"><span data-stu-id="fb160-157">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="fb160-158">Disques de données max. par machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="fb160-158">Max data disks per VM</span></span>

| <span data-ttu-id="fb160-159">Type</span><span class="sxs-lookup"><span data-stu-id="fb160-159">Type</span></span> | <span data-ttu-id="fb160-160">Taille de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="fb160-160">VM Size</span></span> | <span data-ttu-id="fb160-161">Disques de données max. par machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="fb160-161">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="fb160-162">Usage général</span><span class="sxs-lookup"><span data-stu-id="fb160-162">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="fb160-163">Séries A et D</span><span class="sxs-lookup"><span data-stu-id="fb160-163">A and D series</span></span> | <span data-ttu-id="fb160-164">32</span><span class="sxs-lookup"><span data-stu-id="fb160-164">32</span></span> |
| [<span data-ttu-id="fb160-165">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="fb160-165">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="fb160-166">Série F</span><span class="sxs-lookup"><span data-stu-id="fb160-166">F series</span></span> | <span data-ttu-id="fb160-167">32</span><span class="sxs-lookup"><span data-stu-id="fb160-167">32</span></span> |
| [<span data-ttu-id="fb160-168">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="fb160-168">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="fb160-169">Séries D et G</span><span class="sxs-lookup"><span data-stu-id="fb160-169">D and G series</span></span> | <span data-ttu-id="fb160-170">64</span><span class="sxs-lookup"><span data-stu-id="fb160-170">64</span></span> |
| [<span data-ttu-id="fb160-171">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="fb160-171">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="fb160-172">Série L</span><span class="sxs-lookup"><span data-stu-id="fb160-172">L series</span></span> | <span data-ttu-id="fb160-173">64</span><span class="sxs-lookup"><span data-stu-id="fb160-173">64</span></span> |
| [<span data-ttu-id="fb160-174">GPU</span><span class="sxs-lookup"><span data-stu-id="fb160-174">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="fb160-175">Série N</span><span class="sxs-lookup"><span data-stu-id="fb160-175">N series</span></span> | <span data-ttu-id="fb160-176">48</span><span class="sxs-lookup"><span data-stu-id="fb160-176">48</span></span> |
| [<span data-ttu-id="fb160-177">Hautes performances</span><span class="sxs-lookup"><span data-stu-id="fb160-177">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="fb160-178">Séries A et H</span><span class="sxs-lookup"><span data-stu-id="fb160-178">A and H series</span></span> | <span data-ttu-id="fb160-179">32</span><span class="sxs-lookup"><span data-stu-id="fb160-179">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="fb160-180">Type de disque de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="fb160-180">VM disk types</span></span>

<span data-ttu-id="fb160-181">Azure propose deux types de disque.</span><span class="sxs-lookup"><span data-stu-id="fb160-181">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="fb160-182">Disque Standard</span><span class="sxs-lookup"><span data-stu-id="fb160-182">Standard disk</span></span>

<span data-ttu-id="fb160-183">Le stockage Standard s’appuie sur des disques durs et offre un stockage économique qui n’en est pas moins performant.</span><span class="sxs-lookup"><span data-stu-id="fb160-183">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="fb160-184">Les disques Standard constituent la solution idéale pour une charge de travail de développement et de test économique.</span><span class="sxs-lookup"><span data-stu-id="fb160-184">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="fb160-185">Disque Premium</span><span class="sxs-lookup"><span data-stu-id="fb160-185">Premium disk</span></span>

<span data-ttu-id="fb160-186">Les disques Premium reposent sur un disque SSD à faible latence et hautes performances.</span><span class="sxs-lookup"><span data-stu-id="fb160-186">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="fb160-187">Ils conviennent parfaitement aux machines virtuelles exécutant une charge de travail en production.</span><span class="sxs-lookup"><span data-stu-id="fb160-187">Perfect for VMs running production workload.</span></span> <span data-ttu-id="fb160-188">Le stockage Premium prend en charge les machines virtuelles des séries DS, DSv2, GS et FS.</span><span class="sxs-lookup"><span data-stu-id="fb160-188">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="fb160-189">Les disques Premium sont de trois types (P10, P20, P30), la taille du disque détermine le type de disque.</span><span class="sxs-lookup"><span data-stu-id="fb160-189">Premium disks come in three types (P10, P20, P30), the size of the disk determines the disk type.</span></span> <span data-ttu-id="fb160-190">Lorsque vous sélectionnez une taille de disque, la valeur est arrondie au type suivant.</span><span class="sxs-lookup"><span data-stu-id="fb160-190">When selecting, a disk size the value is rounded up to the next type.</span></span> <span data-ttu-id="fb160-191">Par exemple, si la taille du disque est inférieure à 128 Go, le type de disque est P10.</span><span class="sxs-lookup"><span data-stu-id="fb160-191">For example, if the disk size is less than 128 GB, the disk type is P10.</span></span> <span data-ttu-id="fb160-192">Si la taille du disque est entre 129 Go et 512 Go, le type de disque est P20.</span><span class="sxs-lookup"><span data-stu-id="fb160-192">If the disk size is between 129 GB and 512 GB, the size is a P20.</span></span> <span data-ttu-id="fb160-193">Pour toute taille de disque supérieure à 512 Go, le type de disques est P30.</span><span class="sxs-lookup"><span data-stu-id="fb160-193">Anything over 512 GB, the size is a P30.</span></span>

### <a name="premium-disk-performance"></a><span data-ttu-id="fb160-194">Performances du disque Premium</span><span class="sxs-lookup"><span data-stu-id="fb160-194">Premium disk performance</span></span>

|<span data-ttu-id="fb160-195">Type de disque de stockage Premium</span><span class="sxs-lookup"><span data-stu-id="fb160-195">Premium storage disk type</span></span> | <span data-ttu-id="fb160-196">P10</span><span class="sxs-lookup"><span data-stu-id="fb160-196">P10</span></span> | <span data-ttu-id="fb160-197">P20</span><span class="sxs-lookup"><span data-stu-id="fb160-197">P20</span></span> | <span data-ttu-id="fb160-198">P30</span><span class="sxs-lookup"><span data-stu-id="fb160-198">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fb160-199">Taille du disque (arrondie)</span><span class="sxs-lookup"><span data-stu-id="fb160-199">Disk size (round up)</span></span> | <span data-ttu-id="fb160-200">128 Go</span><span class="sxs-lookup"><span data-stu-id="fb160-200">128 GB</span></span> | <span data-ttu-id="fb160-201">512 Go</span><span class="sxs-lookup"><span data-stu-id="fb160-201">512 GB</span></span> | <span data-ttu-id="fb160-202">1 024 Go (1 To)</span><span class="sxs-lookup"><span data-stu-id="fb160-202">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="fb160-203">Nb max. d'E/S par seconde par disque</span><span class="sxs-lookup"><span data-stu-id="fb160-203">Max IOPS per disk</span></span> | <span data-ttu-id="fb160-204">500</span><span class="sxs-lookup"><span data-stu-id="fb160-204">500</span></span> | <span data-ttu-id="fb160-205">2 300</span><span class="sxs-lookup"><span data-stu-id="fb160-205">2,300</span></span> | <span data-ttu-id="fb160-206">5 000</span><span class="sxs-lookup"><span data-stu-id="fb160-206">5,000</span></span> |
<span data-ttu-id="fb160-207">Débit par disque</span><span class="sxs-lookup"><span data-stu-id="fb160-207">Throughput per disk</span></span> | <span data-ttu-id="fb160-208">100 Mo/s</span><span class="sxs-lookup"><span data-stu-id="fb160-208">100 MB/s</span></span> | <span data-ttu-id="fb160-209">150 Mo/s</span><span class="sxs-lookup"><span data-stu-id="fb160-209">150 MB/s</span></span> | <span data-ttu-id="fb160-210">200 Mo/s</span><span class="sxs-lookup"><span data-stu-id="fb160-210">200 MB/s</span></span> |

<span data-ttu-id="fb160-211">Bien que le tableau ci-dessus identifie le nombre max. d’E/S par seconde par disque, un niveau de performances plus élevé est possible en entrelaçant plusieurs disques de données.</span><span class="sxs-lookup"><span data-stu-id="fb160-211">While the above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="fb160-212">Par exemple, une machine virtuelle Standard_GS5 peut atteindre un nombre maximum d’E/S par seconde de 80 000.</span><span class="sxs-lookup"><span data-stu-id="fb160-212">For instance, a Standard_GS5 VM can achieve a maximum of 80,000 IOPS.</span></span> <span data-ttu-id="fb160-213">Pour plus d’informations sur le nombre max. d’E/S par seconde par machine virtuelle, consultez [Tailles des machines virtuelles Linux dans Azure](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="fb160-213">For detailed information on max IOPS per VM, see [Linux VM sizes](sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="fb160-214">Créer et attacher des disques</span><span class="sxs-lookup"><span data-stu-id="fb160-214">Create and attach disks</span></span>

<span data-ttu-id="fb160-215">Des disques de données peuvent être créés et attachés lors de la création d’une machine virtuelle, mais ils peuvent également être créés et attachés à une machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="fb160-215">Data disks can be created and attached at VM creation time or to an existing VM.</span></span>

### <a name="attach-disk-at-vm-creation"></a><span data-ttu-id="fb160-216">Attacher le disque lors de la création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="fb160-216">Attach disk at VM creation</span></span>

<span data-ttu-id="fb160-217">Créez un groupe de ressources avec la commande [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fb160-217">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupDisk --location eastus
```

<span data-ttu-id="fb160-218">Créez une machine virtuelle avec la commande [az vm create]( /cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="fb160-218">Create a VM using the [az vm create]( /cli/azure/vm#create) command.</span></span> <span data-ttu-id="fb160-219">L’argument `--datadisk-sizes-gb` est utilisé pour spécifier qu’un disque supplémentaire doit être créé et attaché à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fb160-219">The `--datadisk-sizes-gb` argument is used to specify that an additional disk should be created and attached to the virtual machine.</span></span> <span data-ttu-id="fb160-220">Pour créer et attacher plusieurs disques, utilisez une liste séparée par des espaces des valeurs de taille de disque.</span><span class="sxs-lookup"><span data-stu-id="fb160-220">To create and attach more than one disk, use a space-delimited list of disk size values.</span></span> <span data-ttu-id="fb160-221">Dans l’exemple suivant, une machine virtuelle est créée avec deux disques de données, tous deux de 128 Go.</span><span class="sxs-lookup"><span data-stu-id="fb160-221">In the following example, a VM is created with two data disks, both 128 GB.</span></span> <span data-ttu-id="fb160-222">La taille des disques étant de 128 Go, ces disques sont configurés en tant que disques P10, qui fournissent 500 E/S par seconde maximum par disque.</span><span class="sxs-lookup"><span data-stu-id="fb160-222">Because the disk sizes are 128 GB, these disks are both configured as P10s, which provide maximum 500 IOPS per disk.</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupDisk \
  --name myVM \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --data-disk-sizes-gb 128 128 \
  --generate-ssh-keys
```

### <a name="attach-disk-to-existing-vm"></a><span data-ttu-id="fb160-223">Attacher un disque à une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="fb160-223">Attach disk to existing VM</span></span>

<span data-ttu-id="fb160-224">Pour créer et attacher un nouveau disque à une machine virtuelle existante, utilisez la commande [az vm disk attach](/cli/azure/vm/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="fb160-224">To create and attach a new disk to an existing virtual machine, use the [az vm disk attach](/cli/azure/vm/disk#attach) command.</span></span> <span data-ttu-id="fb160-225">L’exemple suivant crée un disque Premium de 128 Go et l’attache à la machine virtuelle créée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="fb160-225">The following example creates a premium disk, 128 gigabytes in size, and attaches it to the VM created in the last step.</span></span>

```azurecli-interactive 
az vm disk attach --vm-name myVM --resource-group myResourceGroupDisk --disk myDataDisk --size-gb 128 --sku Premium_LRS --new 
```

## <a name="prepare-data-disks"></a><span data-ttu-id="fb160-226">Préparer les disques de données</span><span class="sxs-lookup"><span data-stu-id="fb160-226">Prepare data disks</span></span>

<span data-ttu-id="fb160-227">Une fois qu’un disque a été attaché à la machine virtuelle, le système d’exploitation doit être configuré pour utiliser le disque.</span><span class="sxs-lookup"><span data-stu-id="fb160-227">Once a disk has been attached to the virtual machine, the operating system needs to be configured to use the disk.</span></span> <span data-ttu-id="fb160-228">L’exemple suivant montre comment configurer manuellement un disque.</span><span class="sxs-lookup"><span data-stu-id="fb160-228">The following example shows how to manually configure a disk.</span></span> <span data-ttu-id="fb160-229">Ce processus peut également être automatisé à l’aide de cloud-init, qui est présenté dans un [prochain didacticiel](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="fb160-229">This process can also be automated using cloud-init, which is covered in a [later tutorial](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="fb160-230">Configuration manuelle</span><span class="sxs-lookup"><span data-stu-id="fb160-230">Manual configuration</span></span>

<span data-ttu-id="fb160-231">Créez une connexion SSH avec la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fb160-231">Create an SSH connection with the virtual machine.</span></span> <span data-ttu-id="fb160-232">Remplacez l’exemple d’adresse IP par l’adresse IP publique de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fb160-232">Replace the example IP address with the public IP of the virtual machine.</span></span>

```azurecli-interactive 
ssh 52.174.34.95
```

<span data-ttu-id="fb160-233">Partitionnez le disque avec `fdisk`.</span><span class="sxs-lookup"><span data-stu-id="fb160-233">Partition the disk with `fdisk`.</span></span>

```bash
(echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="fb160-234">Écrivez un système de fichiers dans la partition avec la commande `mkfs`.</span><span class="sxs-lookup"><span data-stu-id="fb160-234">Write a file system to the partition by using the `mkfs` command.</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="fb160-235">Montez le nouveau disque afin qu’il soit accessible dans le système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="fb160-235">Mount the new disk so that it is accessible in the operating system.</span></span>

```bash
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="fb160-236">Le disque est désormais accessible via le point de montage *datadrive*, qui peut être vérifié en exécutant la commande `df -h`.</span><span class="sxs-lookup"><span data-stu-id="fb160-236">The disk can now be accessed through the *datadrive* mountpoint, which can be verified by running the `df -h` command.</span></span> 

```bash
df -h
```

<span data-ttu-id="fb160-237">La sortie indique le nouveau lecteur monté sur */datadrive*.</span><span class="sxs-lookup"><span data-stu-id="fb160-237">The output shows the new drive mounted on */datadrive*.</span></span>

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   28G   5% /
/dev/sdb1       6.8G   16M  6.4G   1% /mnt
/dev/sdc1        50G   52M   47G   1% /datadrive
```

<span data-ttu-id="fb160-238">Pour vous assurer que le lecteur est remonté automatiquement après un redémarrage, vous devez l’ajouter au fichier */etc/fstab*.</span><span class="sxs-lookup"><span data-stu-id="fb160-238">To ensure that the drive is remounted after a reboot, it must be added to the */etc/fstab* file.</span></span> <span data-ttu-id="fb160-239">Pour ce faire, obtenez l’UUID du disque avec l’utilitaire `blkid`.</span><span class="sxs-lookup"><span data-stu-id="fb160-239">To do so, get the UUID of the disk with the `blkid` utility.</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="fb160-240">La sortie affiche l’UUID du lecteur, `/dev/sdc1` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="fb160-240">The output displays the UUID of the drive, `/dev/sdc1` in this case.</span></span>

```bash
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

<span data-ttu-id="fb160-241">Ajoutez une ligne semblable à ce qui suit au fichier */etc/fstab*.</span><span class="sxs-lookup"><span data-stu-id="fb160-241">Add a line similar to the following to the */etc/fstab* file.</span></span> <span data-ttu-id="fb160-242">Notez également que la fonctionnalité permettant d’écrire des barrières peut être désactivée à l’aide de *barrier=0*, cette configuration peut améliorer les performances de disque.</span><span class="sxs-lookup"><span data-stu-id="fb160-242">Also note that write barriers can be disabled using *barrier=0*, this configuration can improve disk performance.</span></span> 

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive  ext4    defaults,nofail,barrier=0   1  2
```

<span data-ttu-id="fb160-243">Maintenant que le disque a été configuré, fermez la session SSH.</span><span class="sxs-lookup"><span data-stu-id="fb160-243">Now that the disk has been configured, close the SSH session.</span></span>

```bash
exit
```

## <a name="resize-vm-disk"></a><span data-ttu-id="fb160-244">Redimensionner le disque de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="fb160-244">Resize VM disk</span></span>

<span data-ttu-id="fb160-245">Une fois qu’une machine virtuelle a été déployée, vous pouvez augmenter la taille du disque de système d’exploitation ou des disques de données attachés.</span><span class="sxs-lookup"><span data-stu-id="fb160-245">Once a VM has been deployed, the operating system disk or any attached data disks can be increased in size.</span></span> <span data-ttu-id="fb160-246">Augmenter la taille d’un disque peut être utile lorsque vous avez besoin de plus d’espace de stockage ou d’un niveau de performances plus élevé (P10, P20 et P30).</span><span class="sxs-lookup"><span data-stu-id="fb160-246">Increasing the size of a disk is beneficial when needing more storage space or a higher level of performance (P10, P20, P30).</span></span> <span data-ttu-id="fb160-247">Notez que vous ne pouvez pas réduire la taille des disques.</span><span class="sxs-lookup"><span data-stu-id="fb160-247">Note, disks cannot be decreased in size.</span></span>

<span data-ttu-id="fb160-248">Avant d’augmenter la taille du disque, l’ID ou le nom du disque est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="fb160-248">Before increasing disk size, the Id or name of the disk is needed.</span></span> <span data-ttu-id="fb160-249">Utilisez la commande [az disk list](/cli/azure/vm/disk#list) pour renvoyer tous les disques d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fb160-249">Use the [az disk list](/cli/azure/vm/disk#list) command to return all disks in a resource group.</span></span> <span data-ttu-id="fb160-250">Notez le nom du disque que vous souhaitez redimensionner.</span><span class="sxs-lookup"><span data-stu-id="fb160-250">Take note of the disk name that you would like to resize.</span></span>

```azurecli-interactive 
az disk list -g myResourceGroupDisk --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' --output table
```

<span data-ttu-id="fb160-251">La machine virtuelle doit également être libérée.</span><span class="sxs-lookup"><span data-stu-id="fb160-251">The VM must also be deallocated.</span></span> <span data-ttu-id="fb160-252">Utilisez la commande [az vm deallocate]( /cli/azure/vm#deallocate) pour arrêter la machine virtuelle et la libérer.</span><span class="sxs-lookup"><span data-stu-id="fb160-252">Use the [az vm deallocate]( /cli/azure/vm#deallocate) command to stop and deallocate the VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="fb160-253">Utilisez la commande [az disk update](/cli/azure/vm/disk#update) pour redimensionner le disque.</span><span class="sxs-lookup"><span data-stu-id="fb160-253">Use the [az disk update](/cli/azure/vm/disk#update) command to resize the disk.</span></span> <span data-ttu-id="fb160-254">Cet exemple redimensionne un disque nommé *myDataDisk* pour que sa taille soit de 1 To.</span><span class="sxs-lookup"><span data-stu-id="fb160-254">This example resizes a disk named *myDataDisk* to 1 terabyte.</span></span>

```azurecli-interactive 
az disk update --name myDataDisk --resource-group myResourceGroupDisk --size-gb 1023
```

<span data-ttu-id="fb160-255">Une fois l’opération de redimensionnement terminée, démarrez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fb160-255">Once the resize operation has completed, start the VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="fb160-256">Si vous avez redimensionné le disque de système d’exploitation, la partition est automatiquement étendue.</span><span class="sxs-lookup"><span data-stu-id="fb160-256">If you’ve resized the operating system disk, the partition is automatically be expanded.</span></span> <span data-ttu-id="fb160-257">Si vous avez redimensionné un disque de données, toutes les partitions en cours doivent être étendues dans le système d’exploitation des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="fb160-257">If you have resized a data disk, any current partitions need to be expanded in the VMs operating system.</span></span>

## <a name="snapshot-azure-disks"></a><span data-ttu-id="fb160-258">Prendre une capture instantanée des disques Azure</span><span class="sxs-lookup"><span data-stu-id="fb160-258">Snapshot Azure disks</span></span>

<span data-ttu-id="fb160-259">La capture instantanée du disque crée une copie en lecture seule à un moment donné du disque.</span><span class="sxs-lookup"><span data-stu-id="fb160-259">Taking a disk snapshot creates a read only, point-in-time copy of the disk.</span></span> <span data-ttu-id="fb160-260">Les captures instantanées de machine virtuelle Azure sont utiles pour enregistrer rapidement l’état d’une machine virtuelle avant d’apporter des modifications à la configuration.</span><span class="sxs-lookup"><span data-stu-id="fb160-260">Azure VM snapshots are useful for quickly saving the state of a VM before making configuration changes.</span></span> <span data-ttu-id="fb160-261">Si les modifications apportées à la configuration s’avèrent indésirables, l’état de la machine virtuelle peut être restauré à l’aide de la capture instantanée.</span><span class="sxs-lookup"><span data-stu-id="fb160-261">In the event the configuration changes prove to be undesired, VM state can be restored using the snapshot.</span></span> <span data-ttu-id="fb160-262">Lorsqu’une machine virtuelle a plusieurs disques, une capture instantanée de chaque disque est prise.</span><span class="sxs-lookup"><span data-stu-id="fb160-262">When a VM has more than one disk, a snapshot is taken of each disk independently of the others.</span></span> <span data-ttu-id="fb160-263">Pour les sauvegardes cohérentes des applications, pensez à arrêter la machine virtuelle avant de prendre des captures instantanées du disque.</span><span class="sxs-lookup"><span data-stu-id="fb160-263">For taking application consistent backups, consider stopping the VM before taking disk snapshots.</span></span> <span data-ttu-id="fb160-264">Vous pouvez également utiliser le [service Sauvegarde Azure](/azure/backup/), qui vous permet d’effectuer des sauvegardes automatisées alors que la machine virtuelle est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="fb160-264">Alternatively, use the [Azure Backup service](/azure/backup/), which enables you to perform automated backups while the VM is running.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="fb160-265">Création d’un instantané</span><span class="sxs-lookup"><span data-stu-id="fb160-265">Create snapshot</span></span>

<span data-ttu-id="fb160-266">Avant de créer une capture instantanée de disque de machine virtuelle, l’ID ou le nom du disque est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="fb160-266">Before creating a virtual machine disk snapshot, the Id or name of the disk is needed.</span></span> <span data-ttu-id="fb160-267">Utilisez la commande [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) pour renvoyer l’ID du disque.</span><span class="sxs-lookup"><span data-stu-id="fb160-267">Use the [az vm show](https://docs.microsoft.com/en-us/cli/azure/vm#show) command to return the disk id.</span></span> <span data-ttu-id="fb160-268">Dans cet exemple, l’ID du disque est stocké dans une variable pour qu’il puisse être utilisé dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="fb160-268">In this example, the disk id is stored in a variable so that it can be used in a later step.</span></span>

```azurecli-interactive 
osdiskid=$(az vm show -g myResourceGroupDisk -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="fb160-269">Maintenant que vous avez l’ID du disque de machine virtuelle, la commande suivante crée une capture instantanée du disque.</span><span class="sxs-lookup"><span data-stu-id="fb160-269">Now that you have the id of the virtual machine disk, the following command creates a snapshot of the disk.</span></span>

```azurcli
az snapshot create -g myResourceGroupDisk --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="fb160-270">Création d’un disque à partir d’une capture instantanée</span><span class="sxs-lookup"><span data-stu-id="fb160-270">Create disk from snapshot</span></span>

<span data-ttu-id="fb160-271">Cet instantané peut ensuite être converti en disque qui peut être utilisé pour recréer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fb160-271">This snapshot can then be converted into a disk, which can be used to recreate the virtual machine.</span></span>

```azurecli-interactive 
az disk create --resource-group myResourceGroupDisk --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="fb160-272">Restauration de la machine virtuelle à partir de l’instantané</span><span class="sxs-lookup"><span data-stu-id="fb160-272">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="fb160-273">Pour illustrer la récupération de machine virtuelle, supprimez la machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="fb160-273">To demonstrate virtual machine recovery, delete the existing virtual machine.</span></span> 

```azurecli-interactive 
az vm delete --resource-group myResourceGroupDisk --name myVM
```

<span data-ttu-id="fb160-274">Créez une nouvelle machine virtuelle à l’aide du disque d’instantané.</span><span class="sxs-lookup"><span data-stu-id="fb160-274">Create a new virtual machine from the snapshot disk.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupDisk --name myVM --attach-os-disk mySnapshotDisk --os-type linux
```

### <a name="reattach-data-disk"></a><span data-ttu-id="fb160-275">Rattacher un disque de données</span><span class="sxs-lookup"><span data-stu-id="fb160-275">Reattach data disk</span></span>

<span data-ttu-id="fb160-276">Tous les disques de données doivent être rattachés à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fb160-276">All data disks need to be reattached to the virtual machine.</span></span>

<span data-ttu-id="fb160-277">Trouvez d’abord le nom du disque de données à l’aide de la commande [az disk list](https://docs.microsoft.com/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="fb160-277">First find the data disk name using the [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="fb160-278">Cet exemple place le nom du disque dans une variable nommée *datadisk*, qui est utilisée à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="fb160-278">This example places the name of the disk in a variable named *datadisk*, which is used in the next step.</span></span>

```azurecli-interactive 
datadisk=$(az disk list -g myResourceGroupDisk --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="fb160-279">Utilisez la commande [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) pour attacher le disque.</span><span class="sxs-lookup"><span data-stu-id="fb160-279">Use the [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command to attach the disk.</span></span>

```azurecli-interactive 
az vm disk attach –g myResourceGroupDisk –-vm-name myVM –-disk $datadisk
```

## <a name="next-steps"></a><span data-ttu-id="fb160-280">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fb160-280">Next steps</span></span>

<span data-ttu-id="fb160-281">Ce didacticiel vous a apporté des connaissances concernant les disques de machine virtuelle, notamment concernant les points suivants :</span><span class="sxs-lookup"><span data-stu-id="fb160-281">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fb160-282">Disques de système d’exploitation et disques temporaires</span><span class="sxs-lookup"><span data-stu-id="fb160-282">OS disks and temporary disks</span></span>
> * <span data-ttu-id="fb160-283">Disques de données</span><span class="sxs-lookup"><span data-stu-id="fb160-283">Data disks</span></span>
> * <span data-ttu-id="fb160-284">Disques Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="fb160-284">Standard and Premium disks</span></span>
> * <span data-ttu-id="fb160-285">Performances des disques</span><span class="sxs-lookup"><span data-stu-id="fb160-285">Disk performance</span></span>
> * <span data-ttu-id="fb160-286">Attachement et préparation des disques de données</span><span class="sxs-lookup"><span data-stu-id="fb160-286">Attaching and preparing data disks</span></span>
> * <span data-ttu-id="fb160-287">Redimensionnement des disques</span><span class="sxs-lookup"><span data-stu-id="fb160-287">Resizing disks</span></span>
> * <span data-ttu-id="fb160-288">Captures instantanées de disque</span><span class="sxs-lookup"><span data-stu-id="fb160-288">Disk snapshots</span></span>

<span data-ttu-id="fb160-289">Passez au didacticiel suivant pour en apprendre davantage sur l’automatisation de la configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fb160-289">Advance to the next tutorial to learn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="fb160-290">[How to customize a Linux virtual machine on first boot](./tutorial-automate-vm-deployment.md) (Comment personnaliser une machine virtuelle Linux au premier démarrage)</span><span class="sxs-lookup"><span data-stu-id="fb160-290">[Automate VM configuration](./tutorial-automate-vm-deployment.md)</span></span>
