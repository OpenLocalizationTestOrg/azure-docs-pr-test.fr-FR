---
title: "Migrer une machine virtuelle classique vers une machine virtuelle avec disque managé par ARM | Microsoft Docs"
description: "Migrez une machine virtuelle Azure unique à partir du modèle de déploiement Classic vers Managed Disks dans le modèle de déploiement Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 82389834d85981c0ed71bdcc891fbfdbe1377654
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manually-migrate-a-classic-vm-to-a-new-arm-managed-disk-vm-from-the-vhd"></a><span data-ttu-id="29fa7-103">Migrer manuellement une machine virtuelle classique vers une nouvelle machine virtuelle avec disque managé par ARM depuis le disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="29fa7-103">Manually migrate a Classic VM to a new ARM Managed Disk VM from the VHD</span></span> 


<span data-ttu-id="29fa7-104">Cette section vous aide à migrer vos machines virtuelles Azure existantes à partir du modèle de déploiement Classic vers [Managed Disks](managed-disks-overview.md) dans le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="29fa7-104">This section helps you to migrate your existing Azure VMs from the classic deployment model to [Managed Disks](managed-disks-overview.md) in the Resource Manager deployment model.</span></span>


## <a name="plan-for-the-migration-to-managed-disks"></a><span data-ttu-id="29fa7-105">Planification de la migration vers Managed Disks</span><span class="sxs-lookup"><span data-stu-id="29fa7-105">Plan for the migration to Managed Disks</span></span>

<span data-ttu-id="29fa7-106">Cette section vous aide à prendre la meilleure décision concernant les types de machines virtuelles et de disques.</span><span class="sxs-lookup"><span data-stu-id="29fa7-106">This section helps you to make the best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="29fa7-107">Emplacement</span><span class="sxs-lookup"><span data-stu-id="29fa7-107">Location</span></span>

<span data-ttu-id="29fa7-108">Choisissez un emplacement où Azure Managed Disks est disponible.</span><span class="sxs-lookup"><span data-stu-id="29fa7-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="29fa7-109">Si vous effectuez une migration vers des disques gérés Premium, assurez-vous également que le stockage Premium est disponible dans la région où vous prévoyez la migration.</span><span class="sxs-lookup"><span data-stu-id="29fa7-109">If you are migrating to Premium Managed Disks, also ensure that Premium storage is available in the region where you are planning to migrate to.</span></span> <span data-ttu-id="29fa7-110">Pour obtenir des informations à jour sur les emplacements disponibles, consultez [Services Azure par région](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="29fa7-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="29fa7-111">Tailles de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="29fa7-111">VM sizes</span></span>

<span data-ttu-id="29fa7-112">Si vous effectuez une migration vers des disques gérés Premium, vous devez mettre à jour la taille de la machine virtuelle par rapport à la capacité de stockage Premium disponible dans la région où se trouve la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="29fa7-112">If you are migrating to Premium Managed Disks, you have to update the size of the VM to Premium Storage capable size available in the region where VM is located.</span></span> <span data-ttu-id="29fa7-113">Passez en revue les tailles de machine virtuelle compatibles avec le stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="29fa7-113">Review the VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="29fa7-114">Les spécifications des tailles des machines virtuelles Azure sont répertoriées dans la section [Tailles des machines virtuelles](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="29fa7-114">The Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="29fa7-115">Passez en revue les caractéristiques de performances des machines virtuelles fonctionnant avec Premium Storage et choisissez la taille de machine virtuelle la mieux adaptée à votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="29fa7-115">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="29fa7-116">Assurez-vous que la bande passante disponible est suffisante sur votre machine virtuelle pour gérer le trafic du disque.</span><span class="sxs-lookup"><span data-stu-id="29fa7-116">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="29fa7-117">Tailles du disque</span><span class="sxs-lookup"><span data-stu-id="29fa7-117">Disk sizes</span></span>

<span data-ttu-id="29fa7-118">**Disques gérés Premium**</span><span class="sxs-lookup"><span data-stu-id="29fa7-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="29fa7-119">Il existe sept types de disques gérés Premium qui peuvent être utilisés avec votre machine virtuelle, chacun d’eux présentant des limites d’E/S par seconde et de débit spécifiques.</span><span class="sxs-lookup"><span data-stu-id="29fa7-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="29fa7-120">Prenez en compte ces limites lors de la sélection du type de disque Premium pour votre machine virtuelle en fonction des besoins en capacité, en performances, en extensibilité et en charges maximales de votre application.</span><span class="sxs-lookup"><span data-stu-id="29fa7-120">Consider these limits when choosing the Premium disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="29fa7-121">Type de disque Premium</span><span class="sxs-lookup"><span data-stu-id="29fa7-121">Premium Disks Type</span></span>  | <span data-ttu-id="29fa7-122">P4</span><span class="sxs-lookup"><span data-stu-id="29fa7-122">P4</span></span>    | <span data-ttu-id="29fa7-123">P6</span><span class="sxs-lookup"><span data-stu-id="29fa7-123">P6</span></span>    | <span data-ttu-id="29fa7-124">P10</span><span class="sxs-lookup"><span data-stu-id="29fa7-124">P10</span></span>   | <span data-ttu-id="29fa7-125">P20</span><span class="sxs-lookup"><span data-stu-id="29fa7-125">P20</span></span>   | <span data-ttu-id="29fa7-126">P30</span><span class="sxs-lookup"><span data-stu-id="29fa7-126">P30</span></span>   | <span data-ttu-id="29fa7-127">P40</span><span class="sxs-lookup"><span data-stu-id="29fa7-127">P40</span></span>   | <span data-ttu-id="29fa7-128">P50</span><span class="sxs-lookup"><span data-stu-id="29fa7-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="29fa7-129">Taille du disque</span><span class="sxs-lookup"><span data-stu-id="29fa7-129">Disk size</span></span>           | <span data-ttu-id="29fa7-130">128 Go</span><span class="sxs-lookup"><span data-stu-id="29fa7-130">128 GB</span></span>| <span data-ttu-id="29fa7-131">512 Go</span><span class="sxs-lookup"><span data-stu-id="29fa7-131">512 GB</span></span>| <span data-ttu-id="29fa7-132">128 Go</span><span class="sxs-lookup"><span data-stu-id="29fa7-132">128 GB</span></span>| <span data-ttu-id="29fa7-133">512 Go</span><span class="sxs-lookup"><span data-stu-id="29fa7-133">512 GB</span></span>            | <span data-ttu-id="29fa7-134">1024 Go (1 To)</span><span class="sxs-lookup"><span data-stu-id="29fa7-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="29fa7-135">2 048 Go (2 To)</span><span class="sxs-lookup"><span data-stu-id="29fa7-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="29fa7-136">4 095 Go (4 To)</span><span class="sxs-lookup"><span data-stu-id="29fa7-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="29fa7-137">IOPS par disque</span><span class="sxs-lookup"><span data-stu-id="29fa7-137">IOPS per disk</span></span>       | <span data-ttu-id="29fa7-138">120</span><span class="sxs-lookup"><span data-stu-id="29fa7-138">120</span></span>   | <span data-ttu-id="29fa7-139">240</span><span class="sxs-lookup"><span data-stu-id="29fa7-139">240</span></span>   | <span data-ttu-id="29fa7-140">500</span><span class="sxs-lookup"><span data-stu-id="29fa7-140">500</span></span>   | <span data-ttu-id="29fa7-141">2 300</span><span class="sxs-lookup"><span data-stu-id="29fa7-141">2300</span></span>              | <span data-ttu-id="29fa7-142">5 000</span><span class="sxs-lookup"><span data-stu-id="29fa7-142">5000</span></span>              | <span data-ttu-id="29fa7-143">7500</span><span class="sxs-lookup"><span data-stu-id="29fa7-143">7500</span></span>              | <span data-ttu-id="29fa7-144">7500</span><span class="sxs-lookup"><span data-stu-id="29fa7-144">7500</span></span>              | 
| <span data-ttu-id="29fa7-145">Débit par disque</span><span class="sxs-lookup"><span data-stu-id="29fa7-145">Throughput per disk</span></span> | <span data-ttu-id="29fa7-146">25 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="29fa7-146">25 MB per second</span></span>  | <span data-ttu-id="29fa7-147">50 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="29fa7-147">50 MB per second</span></span>  | <span data-ttu-id="29fa7-148">100 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="29fa7-148">100 MB per second</span></span> | <span data-ttu-id="29fa7-149">150 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="29fa7-149">150 MB per second</span></span> | <span data-ttu-id="29fa7-150">200 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="29fa7-150">200 MB per second</span></span> | <span data-ttu-id="29fa7-151">250 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="29fa7-151">250 MB per second</span></span> | <span data-ttu-id="29fa7-152">250 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="29fa7-152">250 MB per second</span></span> | 

<span data-ttu-id="29fa7-153">**Disques gérés Standard**</span><span class="sxs-lookup"><span data-stu-id="29fa7-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="29fa7-154">Il existe sept types de disques gérés Standard qui peuvent être utilisés avec votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="29fa7-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="29fa7-155">Chacun d’eux dispose d’une capacité différente, mais ils partagent les mêmes limites d’E/S par seconde et de débit.</span><span class="sxs-lookup"><span data-stu-id="29fa7-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="29fa7-156">Choisissez le type de disque géré Standard selon les besoins en capacité de votre application.</span><span class="sxs-lookup"><span data-stu-id="29fa7-156">Choose the type of Standard Managed disks based on the capacity needs of your application.</span></span>

| <span data-ttu-id="29fa7-157">Type de disque Standard</span><span class="sxs-lookup"><span data-stu-id="29fa7-157">Standard Disk Type</span></span>  | <span data-ttu-id="29fa7-158">S4</span><span class="sxs-lookup"><span data-stu-id="29fa7-158">S4</span></span>               | <span data-ttu-id="29fa7-159">S6</span><span class="sxs-lookup"><span data-stu-id="29fa7-159">S6</span></span>               | <span data-ttu-id="29fa7-160">S10</span><span class="sxs-lookup"><span data-stu-id="29fa7-160">S10</span></span>              | <span data-ttu-id="29fa7-161">S20</span><span class="sxs-lookup"><span data-stu-id="29fa7-161">S20</span></span>              | <span data-ttu-id="29fa7-162">S30</span><span class="sxs-lookup"><span data-stu-id="29fa7-162">S30</span></span>              | <span data-ttu-id="29fa7-163">S40</span><span class="sxs-lookup"><span data-stu-id="29fa7-163">S40</span></span>              | <span data-ttu-id="29fa7-164">S50</span><span class="sxs-lookup"><span data-stu-id="29fa7-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="29fa7-165">Taille du disque</span><span class="sxs-lookup"><span data-stu-id="29fa7-165">Disk size</span></span>           | <span data-ttu-id="29fa7-166">30 Go</span><span class="sxs-lookup"><span data-stu-id="29fa7-166">30 GB</span></span>            | <span data-ttu-id="29fa7-167">64 Go</span><span class="sxs-lookup"><span data-stu-id="29fa7-167">64 GB</span></span>            | <span data-ttu-id="29fa7-168">128 Go</span><span class="sxs-lookup"><span data-stu-id="29fa7-168">128 GB</span></span>           | <span data-ttu-id="29fa7-169">512 Go</span><span class="sxs-lookup"><span data-stu-id="29fa7-169">512 GB</span></span>           | <span data-ttu-id="29fa7-170">1024 Go (1 To)</span><span class="sxs-lookup"><span data-stu-id="29fa7-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="29fa7-171">2 048 Go (2 To)</span><span class="sxs-lookup"><span data-stu-id="29fa7-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="29fa7-172">4 095 Go (4 To)</span><span class="sxs-lookup"><span data-stu-id="29fa7-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="29fa7-173">IOPS par disque</span><span class="sxs-lookup"><span data-stu-id="29fa7-173">IOPS per disk</span></span>       | <span data-ttu-id="29fa7-174">500</span><span class="sxs-lookup"><span data-stu-id="29fa7-174">500</span></span>              | <span data-ttu-id="29fa7-175">500</span><span class="sxs-lookup"><span data-stu-id="29fa7-175">500</span></span>              | <span data-ttu-id="29fa7-176">500</span><span class="sxs-lookup"><span data-stu-id="29fa7-176">500</span></span>              | <span data-ttu-id="29fa7-177">500</span><span class="sxs-lookup"><span data-stu-id="29fa7-177">500</span></span>              | <span data-ttu-id="29fa7-178">500</span><span class="sxs-lookup"><span data-stu-id="29fa7-178">500</span></span>              | <span data-ttu-id="29fa7-179">500</span><span class="sxs-lookup"><span data-stu-id="29fa7-179">500</span></span>             | <span data-ttu-id="29fa7-180">500</span><span class="sxs-lookup"><span data-stu-id="29fa7-180">500</span></span>              | 
| <span data-ttu-id="29fa7-181">Débit par disque</span><span class="sxs-lookup"><span data-stu-id="29fa7-181">Throughput per disk</span></span> | <span data-ttu-id="29fa7-182">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="29fa7-182">60 MB per second</span></span> | <span data-ttu-id="29fa7-183">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="29fa7-183">60 MB per second</span></span> | <span data-ttu-id="29fa7-184">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="29fa7-184">60 MB per second</span></span> | <span data-ttu-id="29fa7-185">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="29fa7-185">60 MB per second</span></span> | <span data-ttu-id="29fa7-186">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="29fa7-186">60 MB per second</span></span> | <span data-ttu-id="29fa7-187">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="29fa7-187">60 MB per second</span></span> | <span data-ttu-id="29fa7-188">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="29fa7-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="29fa7-189">Stratégie de mise en cache du disque</span><span class="sxs-lookup"><span data-stu-id="29fa7-189">Disk caching policy</span></span> 

<span data-ttu-id="29fa7-190">**Disques gérés Premium**</span><span class="sxs-lookup"><span data-stu-id="29fa7-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="29fa7-191">Par défaut, la stratégie de mise en cache est *Lecture seule* pour tous les disques de données Premium et *Lecture-écriture* pour le disque du système d’exploitation Premium attaché à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="29fa7-191">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="29fa7-192">Ce paramètre de configuration est recommandé pour optimiser les performances des E/S de votre application.</span><span class="sxs-lookup"><span data-stu-id="29fa7-192">This configuration setting is recommended to achieve the optimal performance for your application’s IOs.</span></span> <span data-ttu-id="29fa7-193">Pour les disques de données en écriture seule ou avec d'importantes opérations d'écriture (par ex., les fichiers journaux de SQL Server), désactivez la mise en cache du disque pour de meilleures performances de l'application.</span><span class="sxs-lookup"><span data-stu-id="29fa7-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="29fa7-194">Tarification</span><span class="sxs-lookup"><span data-stu-id="29fa7-194">Pricing</span></span>

<span data-ttu-id="29fa7-195">Consultez la [tarification des disques gérés](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="29fa7-195">Review the [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="29fa7-196">La tarification des disques gérés Premium est identique à celle des disques non gérés Premium.</span><span class="sxs-lookup"><span data-stu-id="29fa7-196">Pricing of Premium Managed Disks is same as the Premium Unmanaged Disks.</span></span> <span data-ttu-id="29fa7-197">En revanche, la tarification des disques gérés Standard diffère de celle des disques Standard non gérés.</span><span class="sxs-lookup"><span data-stu-id="29fa7-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="29fa7-198">Liste de contrôle</span><span class="sxs-lookup"><span data-stu-id="29fa7-198">Checklist</span></span>

1.  <span data-ttu-id="29fa7-199">Si vous effectuez une migration vers des disques gérés Premium, assurez-vous qu’ils sont disponibles dans la région vers laquelle vous effectuez la migration.</span><span class="sxs-lookup"><span data-stu-id="29fa7-199">If you are migrating to Premium Managed Disks, make sure it is available in the region you are migrating to.</span></span>

2.  <span data-ttu-id="29fa7-200">Choisissez la nouvelle série de machines virtuelles que vous allez utiliser.</span><span class="sxs-lookup"><span data-stu-id="29fa7-200">Decide the new VM series you will be using.</span></span> <span data-ttu-id="29fa7-201">Elle doit être compatible avec le stockage Premium si vous migrez vers des disques gérés Premium.</span><span class="sxs-lookup"><span data-stu-id="29fa7-201">It should be a Premium Storage capable if you are migrating to Premium Managed Disks.</span></span>

3.  <span data-ttu-id="29fa7-202">Définissez la taille de machine virtuelle exacte que vous allez utiliser, disponible dans la région vers laquelle vous effectuez la migration.</span><span class="sxs-lookup"><span data-stu-id="29fa7-202">Decide the exact VM size you will use which are available in the region you are migrating to.</span></span> <span data-ttu-id="29fa7-203">La taille de machine virtuelle doit être suffisante pour prendre en charge le nombre de disques de données dont vous disposez.</span><span class="sxs-lookup"><span data-stu-id="29fa7-203">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="29fa7-204">Par exemple, si vous avez quatre disques de données, la machine virtuelle doit avoir au moins deux cœurs.</span><span class="sxs-lookup"><span data-stu-id="29fa7-204">For example, if you have four data disks, the VM must have two or more cores.</span></span> <span data-ttu-id="29fa7-205">Prenez également en considération les besoins en puissance, mémoire et bande passante réseau.</span><span class="sxs-lookup"><span data-stu-id="29fa7-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="29fa7-206">Gardez à portée de main les informations détaillées sur les machines virtuelles, notamment la liste des disques et des blobs de disques durs virtuels correspondants.</span><span class="sxs-lookup"><span data-stu-id="29fa7-206">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="29fa7-207">Préparez votre application pour les interruptions de service.</span><span class="sxs-lookup"><span data-stu-id="29fa7-207">Prepare your application for downtime.</span></span> <span data-ttu-id="29fa7-208">Pour effectuer une migration sans erreur, vous devez arrêter tous les processus en cours d’exécution dans le système actuel.</span><span class="sxs-lookup"><span data-stu-id="29fa7-208">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="29fa7-209">Ce n’est qu’à cette condition que le système présentera un état cohérent, permettant sa migration vers la nouvelle plateforme.</span><span class="sxs-lookup"><span data-stu-id="29fa7-209">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="29fa7-210">La durée de l’interruption de service dépend de la quantité de données dans les disques à migrer.</span><span class="sxs-lookup"><span data-stu-id="29fa7-210">Downtime duration depends on the amount of data in the disks to migrate.</span></span>


## <a name="migrate-the-vm"></a><span data-ttu-id="29fa7-211">Migrer la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="29fa7-211">Migrate the VM</span></span>

<span data-ttu-id="29fa7-212">Préparez votre application pour les interruptions de service.</span><span class="sxs-lookup"><span data-stu-id="29fa7-212">Prepare your application for downtime.</span></span> <span data-ttu-id="29fa7-213">Pour effectuer une migration sans erreur, vous devez arrêter tous les processus en cours d’exécution dans le système actuel.</span><span class="sxs-lookup"><span data-stu-id="29fa7-213">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="29fa7-214">Ce n’est qu’à cette condition que le système présentera un état cohérent, permettant sa migration vers la nouvelle plateforme.</span><span class="sxs-lookup"><span data-stu-id="29fa7-214">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="29fa7-215">La durée de l’interruption de service dépend de la quantité de données dans les disques à migrer.</span><span class="sxs-lookup"><span data-stu-id="29fa7-215">Downtime duration depends the amount of data in the disks to migrate.</span></span>


1.  <span data-ttu-id="29fa7-216">Tout d’abord, définissez les paramètres communs :</span><span class="sxs-lookup"><span data-stu-id="29fa7-216">First, set the common parameters:</span></span>

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  <span data-ttu-id="29fa7-217">Créez un disque de système d’exploitation géré à l’aide du disque dur virtuel de la machine virtuelle classique.</span><span class="sxs-lookup"><span data-stu-id="29fa7-217">Create a managed OS disk using the VHD from the classic VM.</span></span>

    <span data-ttu-id="29fa7-218">Assurez-vous que vous avez indiqué l’URI complet du disque dur virtuel du système d’exploitation dans le paramètre $osVhdUri.</span><span class="sxs-lookup"><span data-stu-id="29fa7-218">Ensure that you have provided the complete URI of the OS VHD to the $osVhdUri parameter.</span></span> <span data-ttu-id="29fa7-219">De plus, dans **Type de compte**, indiquez **PremiumLRS** ou **StandardLRS** selon le type de disque (Premium ou Standard) vers lequel vous effectuez la migration.</span><span class="sxs-lookup"><span data-stu-id="29fa7-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="29fa7-220">Attachez le disque du système d’exploitation à la nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="29fa7-220">Attach the OS disk to the new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="29fa7-221">Créez un disque de données géré à partir du fichier de disque dur virtuel de données et ajoutez-le à la nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="29fa7-221">Create a managed data disk from the data VHD file and add it to the new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="29fa7-222">Créez la machine virtuelle en définissant l’adresse IP publique, le réseau virtuel et la carte réseau.</span><span class="sxs-lookup"><span data-stu-id="29fa7-222">Create the new VM by setting public IP, Virtual Network and NIC.</span></span>

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
><span data-ttu-id="29fa7-223">Des étapes supplémentaires susceptibles de ne pas être exposées dans ce guide peuvent être nécessaires pour prendre en charge vos applications.</span><span class="sxs-lookup"><span data-stu-id="29fa7-223">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="29fa7-224">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29fa7-224">Next steps</span></span>

- <span data-ttu-id="29fa7-225">Connectez-vous à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="29fa7-225">Connect to the virtual machine.</span></span> <span data-ttu-id="29fa7-226">Pour plus d’informations, voir [Connexion à une machine virtuelle Azure exécutant Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="29fa7-226">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

