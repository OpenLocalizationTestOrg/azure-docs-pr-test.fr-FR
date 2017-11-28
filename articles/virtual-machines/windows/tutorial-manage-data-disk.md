---
title: aaaManage Azure disques avec hello Azure PowerShell | Documents Microsoft
description: "Didacticiel - gérer les disques Azure avec hello Azure PowerShell"
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
ms.openlocfilehash: 2f61ad18bc94bab527d7ae593da603c6073adc89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-disks-with-powershell"></a><span data-ttu-id="077bb-103">Gestion des disques Azure avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="077bb-103">Manage Azure disks with PowerShell</span></span>

<span data-ttu-id="077bb-104">Machines virtuelles Azure utilisent le système d’exploitation de disques toostore hello machines virtuelles, des applications et des données.</span><span class="sxs-lookup"><span data-stu-id="077bb-104">Azure virtual machines use disks toostore hello VMs operating system, applications, and data.</span></span> <span data-ttu-id="077bb-105">Lorsque vous créez une machine virtuelle, il est important toochoose une taille de disque et la charge de travail de configuration approprié toohello attendu.</span><span class="sxs-lookup"><span data-stu-id="077bb-105">When creating a VM it is important toochoose a disk size and configuration appropriate toohello expected workload.</span></span> <span data-ttu-id="077bb-106">Ce didacticiel décrit le déploiement et la gestion des disques de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="077bb-106">This tutorial covers deploying and managing VM disks.</span></span> <span data-ttu-id="077bb-107">Vous en apprendrez davantage sur les points suivants :</span><span class="sxs-lookup"><span data-stu-id="077bb-107">You learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="077bb-108">Disques de système d’exploitation et disques temporaires</span><span class="sxs-lookup"><span data-stu-id="077bb-108">OS disks and temporary disks</span></span>
> * <span data-ttu-id="077bb-109">Disques de données</span><span class="sxs-lookup"><span data-stu-id="077bb-109">Data disks</span></span>
> * <span data-ttu-id="077bb-110">Disques Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="077bb-110">Standard and Premium disks</span></span>
> * <span data-ttu-id="077bb-111">Performances des disques</span><span class="sxs-lookup"><span data-stu-id="077bb-111">Disk performance</span></span>
> * <span data-ttu-id="077bb-112">Attachement et préparation des disques de données</span><span class="sxs-lookup"><span data-stu-id="077bb-112">Attaching and preparing data disks</span></span>

<span data-ttu-id="077bb-113">Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module.</span><span class="sxs-lookup"><span data-stu-id="077bb-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="077bb-114">Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="077bb-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="077bb-115">Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="077bb-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="default-azure-disks"></a><span data-ttu-id="077bb-116">Disques Azure par défaut</span><span class="sxs-lookup"><span data-stu-id="077bb-116">Default Azure disks</span></span>

<span data-ttu-id="077bb-117">Création d’une machine virtuelle Azure, deux disques sont automatiquement attaché toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="077bb-117">When an Azure virtual machine is created, two disks are automatically attached toohello virtual machine.</span></span> 

<span data-ttu-id="077bb-118">**Disque de système d’exploitation** - disques de système d’exploitation peuvent être dimensionnés des téraoctets de too1 et hôtes hello de système d’exploitation de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="077bb-118">**Operating system disk** - Operating system disks can be sized up too1 terabyte, and hosts hello VMs operating system.</span></span>  <span data-ttu-id="077bb-119">disque de Hello du système d’exploitation est attribué à une lettre de lecteur de *c:* par défaut.</span><span class="sxs-lookup"><span data-stu-id="077bb-119">hello OS disk is assigned a drive letter of *c:* by default.</span></span> <span data-ttu-id="077bb-120">disque Hello mise en cache de la configuration du disque du système d’exploitation hello est optimisé pour les performances du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="077bb-120">hello disk caching configuration of hello OS disk is optimized for OS performance.</span></span> <span data-ttu-id="077bb-121">disque de Hello du système d’exploitation **ne doivent pas** héberger des applications ou des données.</span><span class="sxs-lookup"><span data-stu-id="077bb-121">hello OS disk **should not** host applications or data.</span></span> <span data-ttu-id="077bb-122">Pour héberger ce type de contenu, utilisez plutôt un disque de données, qui est décrit plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="077bb-122">For applications and data, use a data disk, which is detailed later in this article.</span></span>

<span data-ttu-id="077bb-123">**Disque temporaire** -les disques temporaires utilisent un disque SSD qui se trouve sur hello même hôte Azure en tant que machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="077bb-123">**Temporary disk** - Temporary disks use a solid-state drive that is located on hello same Azure host as hello VM.</span></span> <span data-ttu-id="077bb-124">Les disques temporaires sont extrêmement performants et peuvent être utilisés pour des opérations telles que le traitement de données temporaires.</span><span class="sxs-lookup"><span data-stu-id="077bb-124">Temp disks are highly performant and may be used for operations such as temporary data processing.</span></span> <span data-ttu-id="077bb-125">Toutefois, si hello machine virtuelle est déplacée tooa nouvel hôte, toutes les données stockées sur un disque temporaire sont supprimées.</span><span class="sxs-lookup"><span data-stu-id="077bb-125">However, if hello VM is moved tooa new host, any data stored on a temporary disk is removed.</span></span> <span data-ttu-id="077bb-126">taille de Hello du disque temporaire de hello est déterminé par hello taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="077bb-126">hello size of hello temporary disk is determined by hello VM size.</span></span> <span data-ttu-id="077bb-127">Les disques temporaires se voient attribuer la lettre de lecteur *d:* par défaut.</span><span class="sxs-lookup"><span data-stu-id="077bb-127">Temporary disks are assigned a drive letter of *d:* by default.</span></span>

### <a name="temporary-disk-sizes"></a><span data-ttu-id="077bb-128">Tailles du disque temporaire</span><span class="sxs-lookup"><span data-stu-id="077bb-128">Temporary disk sizes</span></span>

| <span data-ttu-id="077bb-129">Type</span><span class="sxs-lookup"><span data-stu-id="077bb-129">Type</span></span> | <span data-ttu-id="077bb-130">Taille de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="077bb-130">VM Size</span></span> | <span data-ttu-id="077bb-131">Taille maximale du disque temporaire (Go)</span><span class="sxs-lookup"><span data-stu-id="077bb-131">Max temp disk size (GB)</span></span> |
|----|----|----|
| [<span data-ttu-id="077bb-132">Usage général</span><span class="sxs-lookup"><span data-stu-id="077bb-132">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="077bb-133">Séries A et D</span><span class="sxs-lookup"><span data-stu-id="077bb-133">A and D series</span></span> | <span data-ttu-id="077bb-134">800</span><span class="sxs-lookup"><span data-stu-id="077bb-134">800</span></span> |
| [<span data-ttu-id="077bb-135">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="077bb-135">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="077bb-136">Série F</span><span class="sxs-lookup"><span data-stu-id="077bb-136">F series</span></span> | <span data-ttu-id="077bb-137">800</span><span class="sxs-lookup"><span data-stu-id="077bb-137">800</span></span> |
| [<span data-ttu-id="077bb-138">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="077bb-138">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="077bb-139">Séries D et G</span><span class="sxs-lookup"><span data-stu-id="077bb-139">D and G series</span></span> | <span data-ttu-id="077bb-140">6144</span><span class="sxs-lookup"><span data-stu-id="077bb-140">6144</span></span> |
| [<span data-ttu-id="077bb-141">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="077bb-141">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="077bb-142">Série L</span><span class="sxs-lookup"><span data-stu-id="077bb-142">L series</span></span> | <span data-ttu-id="077bb-143">5630</span><span class="sxs-lookup"><span data-stu-id="077bb-143">5630</span></span> |
| [<span data-ttu-id="077bb-144">GPU</span><span class="sxs-lookup"><span data-stu-id="077bb-144">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="077bb-145">Série N</span><span class="sxs-lookup"><span data-stu-id="077bb-145">N series</span></span> | <span data-ttu-id="077bb-146">1 440</span><span class="sxs-lookup"><span data-stu-id="077bb-146">1440</span></span> |
| [<span data-ttu-id="077bb-147">Hautes performances</span><span class="sxs-lookup"><span data-stu-id="077bb-147">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="077bb-148">Séries A et H</span><span class="sxs-lookup"><span data-stu-id="077bb-148">A and H series</span></span> | <span data-ttu-id="077bb-149">2000</span><span class="sxs-lookup"><span data-stu-id="077bb-149">2000</span></span> |

## <a name="azure-data-disks"></a><span data-ttu-id="077bb-150">Disques de données Azure</span><span class="sxs-lookup"><span data-stu-id="077bb-150">Azure data disks</span></span>

<span data-ttu-id="077bb-151">Des disques de données supplémentaires peuvent être ajoutés pour installer des applications et stocker des données.</span><span class="sxs-lookup"><span data-stu-id="077bb-151">Additional data disks can be added for installing applications and storing data.</span></span> <span data-ttu-id="077bb-152">Les disques de données doivent être utilisés dans les cas où un stockage des données durable et réactif est souhaité.</span><span class="sxs-lookup"><span data-stu-id="077bb-152">Data disks should be used in any situation where durable and responsive data storage is desired.</span></span> <span data-ttu-id="077bb-153">Chaque disque de données possède une capacité maximale de 1 To.</span><span class="sxs-lookup"><span data-stu-id="077bb-153">Each data disk has a maximum capacity of 1 terabyte.</span></span> <span data-ttu-id="077bb-154">taille de Hello de machine virtuelle de hello détermine le nombre de disques de données peut être attaché tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="077bb-154">hello size of hello virtual machine determines how many data disks can be attached tooa VM.</span></span> <span data-ttu-id="077bb-155">Pour chaque cœur de la machine virtuelle, deux disques de données peuvent être attachés.</span><span class="sxs-lookup"><span data-stu-id="077bb-155">For each VM core, two data disks can be attached.</span></span> 

### <a name="max-data-disks-per-vm"></a><span data-ttu-id="077bb-156">Disques de données max. par machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="077bb-156">Max data disks per VM</span></span>

| <span data-ttu-id="077bb-157">Type</span><span class="sxs-lookup"><span data-stu-id="077bb-157">Type</span></span> | <span data-ttu-id="077bb-158">Taille de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="077bb-158">VM Size</span></span> | <span data-ttu-id="077bb-159">Disques de données max. par machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="077bb-159">Max data disks per VM</span></span> |
|----|----|----|
| [<span data-ttu-id="077bb-160">Usage général</span><span class="sxs-lookup"><span data-stu-id="077bb-160">General purpose</span></span>](sizes-general.md) | <span data-ttu-id="077bb-161">Séries A et D</span><span class="sxs-lookup"><span data-stu-id="077bb-161">A and D series</span></span> | <span data-ttu-id="077bb-162">32</span><span class="sxs-lookup"><span data-stu-id="077bb-162">32</span></span> |
| [<span data-ttu-id="077bb-163">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="077bb-163">Compute optimized</span></span>](sizes-compute.md) | <span data-ttu-id="077bb-164">Série F</span><span class="sxs-lookup"><span data-stu-id="077bb-164">F series</span></span> | <span data-ttu-id="077bb-165">32</span><span class="sxs-lookup"><span data-stu-id="077bb-165">32</span></span> |
| [<span data-ttu-id="077bb-166">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="077bb-166">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md) | <span data-ttu-id="077bb-167">Séries D et G</span><span class="sxs-lookup"><span data-stu-id="077bb-167">D and G series</span></span> | <span data-ttu-id="077bb-168">64</span><span class="sxs-lookup"><span data-stu-id="077bb-168">64</span></span> |
| [<span data-ttu-id="077bb-169">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="077bb-169">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md) | <span data-ttu-id="077bb-170">Série L</span><span class="sxs-lookup"><span data-stu-id="077bb-170">L series</span></span> | <span data-ttu-id="077bb-171">64</span><span class="sxs-lookup"><span data-stu-id="077bb-171">64</span></span> |
| [<span data-ttu-id="077bb-172">GPU</span><span class="sxs-lookup"><span data-stu-id="077bb-172">GPU</span></span>](sizes-gpu.md) | <span data-ttu-id="077bb-173">Série N</span><span class="sxs-lookup"><span data-stu-id="077bb-173">N series</span></span> | <span data-ttu-id="077bb-174">48</span><span class="sxs-lookup"><span data-stu-id="077bb-174">48</span></span> |
| [<span data-ttu-id="077bb-175">Hautes performances</span><span class="sxs-lookup"><span data-stu-id="077bb-175">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="077bb-176">Séries A et H</span><span class="sxs-lookup"><span data-stu-id="077bb-176">A and H series</span></span> | <span data-ttu-id="077bb-177">32</span><span class="sxs-lookup"><span data-stu-id="077bb-177">32</span></span> |

## <a name="vm-disk-types"></a><span data-ttu-id="077bb-178">Type de disque de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="077bb-178">VM disk types</span></span>

<span data-ttu-id="077bb-179">Azure propose deux types de disque.</span><span class="sxs-lookup"><span data-stu-id="077bb-179">Azure provides two types of disk.</span></span>

### <a name="standard-disk"></a><span data-ttu-id="077bb-180">Disque Standard</span><span class="sxs-lookup"><span data-stu-id="077bb-180">Standard disk</span></span>

<span data-ttu-id="077bb-181">Le stockage Standard s’appuie sur des disques durs et offre un stockage économique qui n’en est pas moins performant.</span><span class="sxs-lookup"><span data-stu-id="077bb-181">Standard Storage is backed by HDDs, and delivers cost-effective storage while still being performant.</span></span> <span data-ttu-id="077bb-182">Les disques Standard constituent la solution idéale pour une charge de travail de développement et de test économique.</span><span class="sxs-lookup"><span data-stu-id="077bb-182">Standard disks are ideal for a cost effective dev and test workload.</span></span>

### <a name="premium-disk"></a><span data-ttu-id="077bb-183">Disque Premium</span><span class="sxs-lookup"><span data-stu-id="077bb-183">Premium disk</span></span>

<span data-ttu-id="077bb-184">Les disques Premium reposent sur un disque SSD à faible latence et hautes performances.</span><span class="sxs-lookup"><span data-stu-id="077bb-184">Premium disks are backed by SSD-based high-performance, low-latency disk.</span></span> <span data-ttu-id="077bb-185">Ils conviennent parfaitement aux machines virtuelles exécutant une charge de travail en production.</span><span class="sxs-lookup"><span data-stu-id="077bb-185">Perfect for VMs running production workload.</span></span> <span data-ttu-id="077bb-186">Le stockage Premium prend en charge les machines virtuelles des séries DS, DSv2, GS et FS.</span><span class="sxs-lookup"><span data-stu-id="077bb-186">Premium Storage supports DS-series, DSv2-series, GS-series, and FS-series VMs.</span></span> <span data-ttu-id="077bb-187">Les disques Premium sont fournis dans les trois types (P10, P20, P30), taille hello du disque de hello détermine le type de disque hello.</span><span class="sxs-lookup"><span data-stu-id="077bb-187">Premium disks come in three types (P10, P20, P30), hello size of hello disk determines hello disk type.</span></span> <span data-ttu-id="077bb-188">Lors de la sélection, une valeur de hello de taille de disque est arrondie toohello les type suivant.</span><span class="sxs-lookup"><span data-stu-id="077bb-188">When selecting, a disk size hello value is rounded up toohello next type.</span></span> <span data-ttu-id="077bb-189">Par exemple, si la taille de hello est sous type de disque de 128 Go hello sera P10, entre 129 et 512 P20 dépasse 512 P30.</span><span class="sxs-lookup"><span data-stu-id="077bb-189">For example, if hello size is below 128 GB hello disk type will be P10, between 129 and 512 P20, and over 512 P30.</span></span> 

### <a name="premium-disk-performance"></a><span data-ttu-id="077bb-190">Performances du disque Premium</span><span class="sxs-lookup"><span data-stu-id="077bb-190">Premium disk performance</span></span>

|<span data-ttu-id="077bb-191">Type de disque de stockage Premium</span><span class="sxs-lookup"><span data-stu-id="077bb-191">Premium storage disk type</span></span> | <span data-ttu-id="077bb-192">P10</span><span class="sxs-lookup"><span data-stu-id="077bb-192">P10</span></span> | <span data-ttu-id="077bb-193">P20</span><span class="sxs-lookup"><span data-stu-id="077bb-193">P20</span></span> | <span data-ttu-id="077bb-194">P30</span><span class="sxs-lookup"><span data-stu-id="077bb-194">P30</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="077bb-195">Taille du disque (arrondie)</span><span class="sxs-lookup"><span data-stu-id="077bb-195">Disk size (round up)</span></span> | <span data-ttu-id="077bb-196">128 Go</span><span class="sxs-lookup"><span data-stu-id="077bb-196">128 GB</span></span> | <span data-ttu-id="077bb-197">512 Go</span><span class="sxs-lookup"><span data-stu-id="077bb-197">512 GB</span></span> | <span data-ttu-id="077bb-198">1 024 Go (1 To)</span><span class="sxs-lookup"><span data-stu-id="077bb-198">1,024 GB (1 TB)</span></span> |
| <span data-ttu-id="077bb-199">IOPS par disque</span><span class="sxs-lookup"><span data-stu-id="077bb-199">IOPS per disk</span></span> | <span data-ttu-id="077bb-200">500</span><span class="sxs-lookup"><span data-stu-id="077bb-200">500</span></span> | <span data-ttu-id="077bb-201">2 300</span><span class="sxs-lookup"><span data-stu-id="077bb-201">2,300</span></span> | <span data-ttu-id="077bb-202">5 000</span><span class="sxs-lookup"><span data-stu-id="077bb-202">5,000</span></span> |
<span data-ttu-id="077bb-203">Débit par disque</span><span class="sxs-lookup"><span data-stu-id="077bb-203">Throughput per disk</span></span> | <span data-ttu-id="077bb-204">100 Mo/s</span><span class="sxs-lookup"><span data-stu-id="077bb-204">100 MB/s</span></span> | <span data-ttu-id="077bb-205">150 Mo/s</span><span class="sxs-lookup"><span data-stu-id="077bb-205">150 MB/s</span></span> | <span data-ttu-id="077bb-206">200 Mo/s</span><span class="sxs-lookup"><span data-stu-id="077bb-206">200 MB/s</span></span> |

<span data-ttu-id="077bb-207">Tandis que hello au-dessus de table identifie max IOPS par disque, un niveau plus élevé de performances est possible par l’agrégation de plusieurs disques de données.</span><span class="sxs-lookup"><span data-stu-id="077bb-207">While hello above table identifies max IOPS per disk, a higher level of performance can be achieved by striping multiple data disks.</span></span> <span data-ttu-id="077bb-208">Par exemple, des 64 données disques peuvent être jointes tooStandard_GS5 VM.</span><span class="sxs-lookup"><span data-stu-id="077bb-208">For instance, 64 data disks can be attached tooStandard_GS5 VM.</span></span> <span data-ttu-id="077bb-209">Si chacun de ces disques est de type P30, vous pouvez atteindre un nombre maximum d’E/S par seconde de 80 000.</span><span class="sxs-lookup"><span data-stu-id="077bb-209">If each of these disks are sized as a P30, a maximum of 80,000 IOPS can be achieved.</span></span> <span data-ttu-id="077bb-210">Pour plus d’informations sur le nombre max. d’E/S par seconde par machine virtuelle, consultez [Tailles des machines virtuelles Linux dans Azure](./sizes.md).</span><span class="sxs-lookup"><span data-stu-id="077bb-210">For detailed information on max IOPS per VM, see [Linux VM sizes](./sizes.md).</span></span>

## <a name="create-and-attach-disks"></a><span data-ttu-id="077bb-211">Créer et attacher des disques</span><span class="sxs-lookup"><span data-stu-id="077bb-211">Create and attach disks</span></span>

<span data-ttu-id="077bb-212">exemple de hello toocomplete dans ce didacticiel, vous devez disposer d’un ordinateur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="077bb-212">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="077bb-213">Si nécessaire, cet [exemple de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) peut en créer une pour vous.</span><span class="sxs-lookup"><span data-stu-id="077bb-213">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="077bb-214">Lorsque le travail didacticiel de hello, remplacez machine virtuelle et groupe de ressources hello noms lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="077bb-214">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

<span data-ttu-id="077bb-215">Créer la configuration initiale hello avec [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span><span class="sxs-lookup"><span data-stu-id="077bb-215">Create hello initial configuration with [New-AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig).</span></span> <span data-ttu-id="077bb-216">Bonjour à l’exemple suivant configure un disque qui est la taille de 128 gigaoctets.</span><span class="sxs-lookup"><span data-stu-id="077bb-216">hello following example configures a disk that is 128 gigabytes in size.</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location EastUS -CreateOption Empty -DiskSizeGB 128
```

<span data-ttu-id="077bb-217">Créer un disque de données hello avec hello [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) commande.</span><span class="sxs-lookup"><span data-stu-id="077bb-217">Create hello data disk with hello [New-AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) command.</span></span>

```powershell
$dataDisk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myDataDisk -Disk $diskConfig
```

<span data-ttu-id="077bb-218">Ordinateur virtuel de Get hello que vous souhaitez tooadd Bonjour données disque toowith Bonjour [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) commande.</span><span class="sxs-lookup"><span data-stu-id="077bb-218">Get hello virtual machine that you want tooadd hello data disk toowith hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="077bb-219">Ajouter hello données disque toohello configuration d’ordinateur virtuel avec hello [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) commande.</span><span class="sxs-lookup"><span data-stu-id="077bb-219">Add hello data disk toohello virtual machine configuration with hello [Add-AzureRmVMDataDisk](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk -VM $vm -Name myDataDisk -CreateOption Attach -ManagedDiskId $dataDisk.Id -Lun 1
```

<span data-ttu-id="077bb-220">Mettre à jour de la machine virtuelle de hello avec hello [AzureRmVM de mise à jour](/powershell/module/azurerm.compute/add-azurermvmdatadisk) commande.</span><span class="sxs-lookup"><span data-stu-id="077bb-220">Update hello virtual machine with hello [Update-AzureRmVM](/powershell/module/azurerm.compute/add-azurermvmdatadisk) command.</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="prepare-data-disks"></a><span data-ttu-id="077bb-221">Préparer les disques de données</span><span class="sxs-lookup"><span data-stu-id="077bb-221">Prepare data disks</span></span>

<span data-ttu-id="077bb-222">Une fois qu’un disque a été attaché toohello virtual machine, le système d’exploitation de hello doit toobe configuré toouse hello disque.</span><span class="sxs-lookup"><span data-stu-id="077bb-222">Once a disk has been attached toohello virtual machine, hello operating system needs toobe configured toouse hello disk.</span></span> <span data-ttu-id="077bb-223">Hello suivant montre comment toomanually configurer hello premier disque ajouté toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="077bb-223">hello following example shows how toomanually configure hello first disk added toohello VM.</span></span> <span data-ttu-id="077bb-224">Ce processus peut également être automatisé à l’aide de hello [extension de script personnalisé](./tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="077bb-224">This process can also be automated using hello [custom script extension](./tutorial-automate-vm-deployment.md).</span></span>

### <a name="manual-configuration"></a><span data-ttu-id="077bb-225">Configuration manuelle</span><span class="sxs-lookup"><span data-stu-id="077bb-225">Manual configuration</span></span>

<span data-ttu-id="077bb-226">Créer une connexion RDP avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="077bb-226">Create an RDP connection with hello virtual machine.</span></span> <span data-ttu-id="077bb-227">Ouvrez PowerShell et exécutez ce script.</span><span class="sxs-lookup"><span data-stu-id="077bb-227">Open up PowerShell and run this script.</span></span>

```powershell
Get-Disk | Where partitionstyle -eq 'raw' | `
Initialize-Disk -PartitionStyle MBR -PassThru | `
New-Partition -AssignDriveLetter -UseMaximumSize | `
Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false
```

## <a name="next-steps"></a><span data-ttu-id="077bb-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="077bb-228">Next steps</span></span>

<span data-ttu-id="077bb-229">Ce didacticiel vous a apporté des connaissances concernant les disques de machine virtuelle, notamment concernant les points suivants :</span><span class="sxs-lookup"><span data-stu-id="077bb-229">In this tutorial, you learned about VM disks topics such as:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="077bb-230">Disques de système d’exploitation et disques temporaires</span><span class="sxs-lookup"><span data-stu-id="077bb-230">OS disks and temporary disks</span></span>
> * <span data-ttu-id="077bb-231">Disques de données</span><span class="sxs-lookup"><span data-stu-id="077bb-231">Data disks</span></span>
> * <span data-ttu-id="077bb-232">Disques Standard et Premium</span><span class="sxs-lookup"><span data-stu-id="077bb-232">Standard and Premium disks</span></span>
> * <span data-ttu-id="077bb-233">Performances des disques</span><span class="sxs-lookup"><span data-stu-id="077bb-233">Disk performance</span></span>
> * <span data-ttu-id="077bb-234">Attachement et préparation des disques de données</span><span class="sxs-lookup"><span data-stu-id="077bb-234">Attaching and preparing data disks</span></span>

<span data-ttu-id="077bb-235">Avance toohello toolearn de didacticiel suivant sur l’automatisation de configuration d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="077bb-235">Advance toohello next tutorial toolearn about automating VM configuration.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="077bb-236">Automatiser la configuration de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="077bb-236">Automate VM configuration</span></span>](./tutorial-automate-vm-deployment.md)
