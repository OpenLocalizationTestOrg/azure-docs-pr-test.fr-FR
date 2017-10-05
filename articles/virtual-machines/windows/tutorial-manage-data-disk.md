---
title: Gestion des disques Azure avec Azure PowerShell | Microsoft Docs
description: Didacticiel - Gestion des disques Azure avec Azure PowerShell
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 6f1bc9361745adc211f22416a7ba8ac1b8dc614e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="107e9-103">Gestion des disques Azure avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="107e9-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="107e9-104">Les machines virtuelles utilisent des disques pour stocker leur système d’exploitation, leurs applications et leurs données.</span><span class="sxs-lookup"><span data-stu-id="107e9-104">Azure virtual machines use disks to store the VMs operating system, applications, and data.</span></span> <span data-ttu-id="107e9-105">Lorsque vous créez une machine virtuelle, il est important de choisir une taille de disque et une configuration appropriées à la charge de travail prévue.</span><span class="sxs-lookup"><span data-stu-id="107e9-105">When creating a VM it is important to choose a disk size and configuration appropriate to the expected workload.</span></span> <span data-ttu-id="107e9-106">Ce didacticiel décrit le déploiement et la gestion des disques de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="107e9-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="107e9-107">Vous en apprendrez davantage sur les points suivants :</span><span class="sxs-lookup"><span data-stu-id="107e9-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="107e9-108">Disques de système d’exploitation et disques temporaires</span><span class="sxs-lookup"><span data-stu-id="107e9-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="107e9-109">Disques de données</span><span class="sxs-lookup"><span data-stu-id="107e9-109">Data disks</span></span>
> * <span data-ttu-id="107e9-110">Disques Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="107e9-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="107e9-111">Performances des disques</span><span class="sxs-lookup"><span data-stu-id="107e9-111">Disk performance</span></span>
> * <span data-ttu-id="107e9-112">Attachement et préparation des disques de données</span><span class="sxs-lookup"><span data-stu-id="107e9-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="107e9-113">Ce didacticiel requiert le module Azure PowerShell version 3.6 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="107e9-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="107e9-114">Exécutez ` Get-Module -ListAvailable AzureRM` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="107e9-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="107e9-115">Si vous devez effectuer une mise à niveau, consultez [Installer le module Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="107e9-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="107e9-116">Disques Azure par défaut</span><span class="sxs-lookup"><span data-stu-id="107e9-116">Default Azure disks</span></span>

<span data-ttu-id="107e9-117">Lorsqu’une machine virtuelle Azure est créée, deux disques sont automatiquement attachés à celle-ci.</span><span class="sxs-lookup"><span data-stu-id="107e9-117">When an Azure virtual machine is created, two disks are automatically attached to the virtual machine.</span></span> 

<span data-ttu-id="107e9-118">**Disque de système d’exploitation** : la taille des disques de système d’exploitation peut atteindre 1 To ; ces disques hébergent le système d’exploitation des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="107e9-118">**Operating system disk** - Operating system disks can be sized up to 1 terabyte, and hosts the VMs operating system.</span></span>  <span data-ttu-id="107e9-119">Le disque de système d’exploitation se voit attribuer la lettre de lecteur *c:* par défaut.</span><span class="sxs-lookup"><span data-stu-id="107e9-119">The OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="107e9-120">La configuration de la mise en cache de disque de système d’exploitation est optimisée pour les performances du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="107e9-120">The disk caching configuration of the OS disk is optimized for OS performance.</span></span> <span data-ttu-id="107e9-121">Le disque de système d’exploitation **ne doit pas** héberger d’applications ou de données.</span><span class="sxs-lookup"><span data-stu-id="107e9-121">The OS disk **should not** host applications or data.</span></span> <span data-ttu-id="107e9-122">Pour héberger ce type de contenu, utilisez plutôt un disque de données, qui est décrit plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="107e9-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="107e9-123">**Disque temporaire** : les disques temporaires utilisent un disque SSD qui se trouve sur le même hôte Azure que la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="107e9-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on the same Azure host as the VM.</span></span> <span data-ttu-id="107e9-124">Les disques temporaires sont extrêmement performants et peuvent être utilisés pour des opérations telles que le traitement de données temporaires.</span><span class="sxs-lookup"><span data-stu-id="107e9-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="107e9-125">Toutefois, si la machine virtuelle est déplacée vers un nouvel hôte, toutes les données stockées sur un disque temporaire sont supprimées.</span><span class="sxs-lookup"><span data-stu-id="107e9-125">However, if the VM is moved to a new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="107e9-126">La taille du disque temporaire est déterminée par la taille de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="107e9-126">The size of the temporary disk is determined by the VM size.</span></span> <span data-ttu-id="107e9-127">Les disques temporaires se voient attribuer la lettre de lecteur *d:* par défaut.</span><span class="sxs-lookup"><span data-stu-id="107e9-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="107e9-128">Tailles du disque temporaire</span><span class="sxs-lookup"><span data-stu-id="107e9-128">Temporary disk sizes</span></span>

| <span data-ttu-id="107e9-129">Type</span><span class="sxs-lookup"><span data-stu-id="107e9-129">Type</span></span> | <span data-ttu-id="107e9-130">Taille de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="107e9-130">VM Size</span></span> | <span data-ttu-id="107e9-131">Taille maximale du disque temporaire (Go)</span><span class="sxs-lookup"><span data-stu-id="107e9-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="107e9-132">Usage général</span><span class="sxs-lookup"><span data-stu-id="107e9-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="107e9-133">Séries A et D</span><span class="sxs-lookup"><span data-stu-id="107e9-133">A and D series</span></span> | <span data-ttu-id="107e9-134">800</span><span class="sxs-lookup"><span data-stu-id="107e9-134">800</span></span> |
| [<span data-ttu-id="107e9-135">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="107e9-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="107e9-136">Série F</span><span class="sxs-lookup"><span data-stu-id="107e9-136">F series</span></span> | <span data-ttu-id="107e9-137">800</span><span class="sxs-lookup"><span data-stu-id="107e9-137">800</span></span> |
| [<span data-ttu-id="107e9-138">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="107e9-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="107e9-139">Séries D et G</span><span class="sxs-lookup"><span data-stu-id="107e9-139">D and G series</span></span> | <span data-ttu-id="107e9-140">6144</span><span class="sxs-lookup"><span data-stu-id="107e9-140">6144</span></span> |
| [<span data-ttu-id="107e9-141">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="107e9-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="107e9-142">Série L</span><span class="sxs-lookup"><span data-stu-id="107e9-142">L series</span></span> | <span data-ttu-id="107e9-143">5630</span><span class="sxs-lookup"><span data-stu-id="107e9-143">5630</span></span> |
| [<span data-ttu-id="107e9-144">GPU</span><span class="sxs-lookup"><span data-stu-id="107e9-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="107e9-145">Série N</span><span class="sxs-lookup"><span data-stu-id="107e9-145">N series</span></span> | <span data-ttu-id="107e9-146">1 440</span><span class="sxs-lookup"><span data-stu-id="107e9-146">1440</span></span> |
| [<span data-ttu-id="107e9-147">Hautes performances</span><span class="sxs-lookup"><span data-stu-id="107e9-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="107e9-148">Séries A et H</span><span class="sxs-lookup"><span data-stu-id="107e9-148">A and H series</span></span> | <span data-ttu-id="107e9-149">2000</span><span class="sxs-lookup"><span data-stu-id="107e9-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="107e9-150">Disques de données Azure</span><span class="sxs-lookup"><span data-stu-id="107e9-150">Azure data disks</span></span>

<span data-ttu-id="107e9-151">Des disques de données supplémentaires peuvent être ajoutés pour installer des applications et stocker des données.</span><span class="sxs-lookup"><span data-stu-id="107e9-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="107e9-152">Les disques de données doivent être utilisés dans les cas où un stockage des données durable et réactif est souhaité.</span><span class="sxs-lookup"><span data-stu-id="107e9-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="107e9-153">Chaque disque de données possède une capacité maximale de 1 To.</span><span class="sxs-lookup"><span data-stu-id="107e9-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="107e9-154">La taille de la machine virtuelle détermine le nombre de disques de données pouvant être attachés à cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="107e9-154">The size of the virtual machine determines how many data disks can be attached to a VM.</span></span> <span data-ttu-id="107e9-155">Pour chaque cœur de la machine virtuelle, deux disques de données peuvent être attachés.</span><span class="sxs-lookup"><span data-stu-id="107e9-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="107e9-156">Disques de données max. par machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="107e9-156">Max data disks per VM</span></span>

| <span data-ttu-id="107e9-157">Type</span><span class="sxs-lookup"><span data-stu-id="107e9-157">Type</span></span> | <span data-ttu-id="107e9-158">Taille de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="107e9-158">VM Size</span></span> | <span data-ttu-id="107e9-159">Disques de données max. par machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="107e9-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="107e9-160">Usage général</span><span class="sxs-lookup"><span data-stu-id="107e9-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="107e9-161">Séries A et D</span><span class="sxs-lookup"><span data-stu-id="107e9-161">A and D series</span></span> | <span data-ttu-id="107e9-162">32</span><span class="sxs-lookup"><span data-stu-id="107e9-162">32</span></span> |
| [<span data-ttu-id="107e9-163">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="107e9-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="107e9-164">Série F</span><span class="sxs-lookup"><span data-stu-id="107e9-164">F series</span></span> | <span data-ttu-id="107e9-165">32</span><span class="sxs-lookup"><span data-stu-id="107e9-165">32</span></span> |
| [<span data-ttu-id="107e9-166">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="107e9-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="107e9-167">Séries D et G</span><span class="sxs-lookup"><span data-stu-id="107e9-167">D and G series</span></span> | <span data-ttu-id="107e9-168">64</span><span class="sxs-lookup"><span data-stu-id="107e9-168">64</span></span> |
| [<span data-ttu-id="107e9-169">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="107e9-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="107e9-170">Série L</span><span class="sxs-lookup"><span data-stu-id="107e9-170">L series</span></span> | <span data-ttu-id="107e9-171">64</span><span class="sxs-lookup"><span data-stu-id="107e9-171">64</span></span> |
| [<span data-ttu-id="107e9-172">GPU</span><span class="sxs-lookup"><span data-stu-id="107e9-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="107e9-173">Série N</span><span class="sxs-lookup"><span data-stu-id="107e9-173">N series</span></span> | <span data-ttu-id="107e9-174">48</span><span class="sxs-lookup"><span data-stu-id="107e9-174">48</span></span> |
| [<span data-ttu-id="107e9-175">Hautes performances</span><span class="sxs-lookup"><span data-stu-id="107e9-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="107e9-176">Séries A et H</span><span class="sxs-lookup"><span data-stu-id="107e9-176">A and H series</span></span> | <span data-ttu-id="107e9-177">32</span><span class="sxs-lookup"><span data-stu-id="107e9-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="107e9-178">Type de disque de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="107e9-178">VM disk types</span></span>

<span data-ttu-id="107e9-179">Azure propose deux types de disque.</span><span class="sxs-lookup"><span data-stu-id="107e9-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="107e9-180">Disque Standard</span><span class="sxs-lookup"><span data-stu-id="107e9-180">Standard disk</span></span>

<span data-ttu-id="107e9-181">Le stockage Standard s’appuie sur des disques durs et offre un stockage économique qui n’en est pas moins performant.</span><span class="sxs-lookup"><span data-stu-id="107e9-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="107e9-182">Les disques Standard constituent la solution idéale pour une charge de travail de développement et de test économique.</span><span class="sxs-lookup"><span data-stu-id="107e9-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="107e9-183">Disque Premium</span><span class="sxs-lookup"><span data-stu-id="107e9-183">Premium disk</span></span>

<span data-ttu-id="107e9-184">Les disques Premium reposent sur un disque SSD à faible latence et hautes performances.</span><span class="sxs-lookup"><span data-stu-id="107e9-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="107e9-185">Ils conviennent parfaitement aux machines virtuelles exécutant une charge de travail en production.</span><span class="sxs-lookup"><span data-stu-id="107e9-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="107e9-186">Le stockage Premium prend en charge les machines virtuelles des séries DS, DSv2, GS et FS.</span><span class="sxs-lookup"><span data-stu-id="107e9-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="107e9-187">Les disques Premium sont de trois types (P10, P20, P30), la taille du disque détermine le type de disque.</span><span class="sxs-lookup"><span data-stu-id="107e9-187">Premium disks come in three types (P10, P20, P30), the size of the disk determines the disk type.</span></span> <span data-ttu-id="107e9-188">Lorsque vous sélectionnez une taille de disque, la valeur est arrondie au type suivant.</span><span class="sxs-lookup"><span data-stu-id="107e9-188">When selecting, a disk size the value is rounded up to the next type.</span></span> <span data-ttu-id="107e9-189">Par exemple, si la taille est inférieure à 128 Go le type de disque sera P10, entre 129 Go et 512 Go, le type de disque sera P20, et au-delà de 512 Go, le type de disque sera P30.</span><span class="sxs-lookup"><span data-stu-id="107e9-189">For example, if the size is below 128 GB the disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="107e9-190">Performances du disque Premium</span><span class="sxs-lookup"><span data-stu-id="107e9-190">Premium disk performance</span></span>

|<span data-ttu-id="107e9-191">Type de disque de stockage Premium</span><span class="sxs-lookup"><span data-stu-id="107e9-191">Premium storage disk type</span></span> | <span data-ttu-id="107e9-192">P10</span><span class="sxs-lookup"><span data-stu-id="107e9-192">P10</span></span> | <span data-ttu-id="107e9-193">P20</span><span class="sxs-lookup"><span data-stu-id="107e9-193">P20</span></span> | <span data-ttu-id="107e9-194">P30</span><span class="sxs-lookup"><span data-stu-id="107e9-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="107e9-195">Taille du disque (arrondie)</span><span class="sxs-lookup"><span data-stu-id="107e9-195">Disk size (round up)</span></span> | <span data-ttu-id="107e9-196">128 Go</span><span class="sxs-lookup"><span data-stu-id="107e9-196">128 GB</span></span> | <span data-ttu-id="107e9-197">512 Go</span><span class="sxs-lookup"><span data-stu-id="107e9-197">512 GB</span></span> | <span data-ttu-id="107e9-198">1 024 Go (1 To)</span><span class="sxs-lookup"><span data-stu-id="107e9-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="107e9-199">IOPS par disque</span><span class="sxs-lookup"><span data-stu-id="107e9-199">IOPS per disk</span></span> | <span data-ttu-id="107e9-200">500</span><span class="sxs-lookup"><span data-stu-id="107e9-200">500</span></span> | <span data-ttu-id="107e9-201">2 300</span><span class="sxs-lookup"><span data-stu-id="107e9-201">2,300</span></span> | <span data-ttu-id="107e9-202">5 000</span><span class="sxs-lookup"><span data-stu-id="107e9-202">5,000</span></span> |
<span data-ttu-id="107e9-203">Débit par disque</span><span class="sxs-lookup"><span data-stu-id="107e9-203">Throughput per disk</span></span> | <span data-ttu-id="107e9-204">100 Mo/s</span><span class="sxs-lookup"><span data-stu-id="107e9-204">100 MB/s</span></span> | <span data-ttu-id="107e9-205">150 Mo/s</span><span class="sxs-lookup"><span data-stu-id="107e9-205">150 MB/s</span></span> | <span data-ttu-id="107e9-206">200 Mo/s</span><span class="sxs-lookup"><span data-stu-id="107e9-206">200 MB/s</span></span> |

<span data-ttu-id="107e9-207">Bien que le tableau ci-dessus identifie le nombre max. d’E/S par seconde par disque, un niveau de performances plus élevé est possible en entrelaçant plusieurs disques de données.</span><span class="sxs-lookup"><span data-stu-id="107e9-207">While the above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="107e9-208">Par exemple, 64 disques de données peuvent être attachés à la machine virtuelle Standard_GS5.</span><span class="sxs-lookup"><span data-stu-id="107e9-208">For instance, 64 data disks can be attached to Standard_GS5 VM.</span></span> <span data-ttu-id="107e9-209">Si chacun de ces disques est de type P30, vous pouvez atteindre un nombre maximum d’E/S par seconde de 80 000.</span><span class="sxs-lookup"><span data-stu-id="107e9-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="107e9-210">Pour plus d’informations sur le nombre max. d’E/S par seconde par machine virtuelle, consultez [Tailles des machines virtuelles Linux dans Azure](./sizes.md).</span><span class="sxs-lookup"><span data-stu-id="107e9-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="107e9-211">Créer et attacher des disques</span><span class="sxs-lookup"><span data-stu-id="107e9-211">Create and attach disks</span></span>

<span data-ttu-id="107e9-212">Pour exécuter l’exemple dans ce didacticiel, vous devez disposer d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="107e9-212">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="107e9-213">Si nécessaire, cet [exemple de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) peut en créer une pour vous.</span><span class="sxs-lookup"><span data-stu-id="107e9-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="107e9-214">Au cours du didacticiel, remplacez les noms du groupe de ressources et de la machine virtuelle si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="107e9-214">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

<span data-ttu-id="107e9-215">Créez la configuration initiale avec [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span><span class="sxs-lookup"><span data-stu-id="107e9-215">Create the initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="107e9-216">L’exemple suivant configure un disque d’une taille de 128 Go.</span><span class="sxs-lookup"><span data-stu-id="107e9-216">The following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="107e9-217">Créez le disque de données avec la commande [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="107e9-217">Create the data disk with the [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="107e9-218">Obtenez la machine virtuelle que vous souhaitez ajouter au disque de données avec la commande [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="107e9-218">Get the virtual machine that you want to add the data disk to with the [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="107e9-219">Ajoutez le disque de données à la configuration de la machine virtuelle avec la commande [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="107e9-219">Add the data disk to the virtual machine configuration with the [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="107e9-220">Mettez à jour la machine virtuelle avec la commande [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk).</span><span class="sxs-lookup"><span data-stu-id="107e9-220">Update the virtual machine with the [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="107e9-221">Préparer les disques de données</span><span class="sxs-lookup"><span data-stu-id="107e9-221">Prepare data disks</span></span>

<span data-ttu-id="107e9-222">Une fois qu’un disque a été attaché à la machine virtuelle, le système d’exploitation doit être configuré pour utiliser le disque.</span><span class="sxs-lookup"><span data-stu-id="107e9-222">Once a disk has been attached to the virtual machine, the operating system needs to be configured to use the disk.</span></span> <span data-ttu-id="107e9-223">L’exemple suivant montre comment configurer manuellement le premier disque ajouté à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="107e9-223">The following example shows how to manually configure the first disk added to the VM.</span></span> <span data-ttu-id="107e9-224">Ce processus peut également être automatisé à l’aide de [l’extension de script personnalisé](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="107e9-224">This process can also be automated using the [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="107e9-225">Configuration manuelle</span><span class="sxs-lookup"><span data-stu-id="107e9-225">Manual configuration</span></span>

<span data-ttu-id="107e9-226">Créez une connexion RDP avec la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="107e9-226">Create an RDP connection with the virtual machine.</span></span> <span data-ttu-id="107e9-227">Ouvrez PowerShell et exécutez ce script.</span><span class="sxs-lookup"><span data-stu-id="107e9-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="107e9-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="107e9-228">Next steps</span></span>

<span data-ttu-id="107e9-229">Ce didacticiel vous a apporté des connaissances concernant les disques de machine virtuelle, notamment concernant les points suivants :</span><span class="sxs-lookup"><span data-stu-id="107e9-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="107e9-230">Disques de système d’exploitation et disques temporaires</span><span class="sxs-lookup"><span data-stu-id="107e9-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="107e9-231">Disques de données</span><span class="sxs-lookup"><span data-stu-id="107e9-231">Data disks</span></span>
> * <span data-ttu-id="107e9-232">Disques Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="107e9-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="107e9-233">Performances des disques</span><span class="sxs-lookup"><span data-stu-id="107e9-233">Disk performance</span></span>
> * <span data-ttu-id="107e9-234">Attachement et préparation des disques de données</span><span class="sxs-lookup"><span data-stu-id="107e9-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="107e9-235">Passez au didacticiel suivant pour en apprendre davantage sur l’automatisation de la configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="107e9-235">Advance to the next tutorial to learn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="107e9-236">[How to customize a Linux virtual machine on first boot](./tutorial-automate-vm-deployment.md) (Comment personnaliser une machine virtuelle Linux au premier démarrage)</span><span class="sxs-lookup"><span data-stu-id="107e9-236">[Automate VM configuration](./tutorial-automate-vm-deployment.md)</span></span>
