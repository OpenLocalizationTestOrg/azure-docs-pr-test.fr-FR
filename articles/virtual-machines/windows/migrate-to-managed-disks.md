---
title: aaaMigrate disques de machines virtuelles Azure tooManaged | Documents Microsoft
description: "Migrer des machines virtuelles créées à l’aide de disques non managés dans toouse de comptes de stockage des disques gérés."
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
ms.openlocfilehash: 29420f13c4ffd5b25726e0ef1aafe89347286a89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-vms-toomanaged-disks-in-azure"></a><span data-ttu-id="3baef-103">Migrer des machines virtuelles Azure tooManaged des disques dans Azure</span><span class="sxs-lookup"><span data-stu-id="3baef-103">Migrate Azure VMs tooManaged Disks in Azure</span></span>

<span data-ttu-id="3baef-104">Des disques gérés Azure simplifie la gestion du stockage en supprimant la nécessité de hello tooseparately gérer les comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="3baef-104">Azure Managed Disks simplifies your storage management by removing hello need tooseparately manage storage accounts.</span></span>  <span data-ttu-id="3baef-105">Vous pouvez également migrer votre toobenefit de disques tooManaged machines virtuelles Azure existante à partir d’une meilleure fiabilité des machines virtuelles sur un ensemble de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="3baef-105">You can also migrate your existing Azure VMs tooManaged Disks toobenefit from better reliability of VMs in an Availability Set.</span></span> <span data-ttu-id="3baef-106">Elle garantit que les disques hello des différentes machines virtuelles dans un ensemble de disponibilité sera suffisamment isolés à partir de chaque autre point unique tooavoid d’échecs.</span><span class="sxs-lookup"><span data-stu-id="3baef-106">It ensures that hello disks of different VMs in an Availability Set will be sufficiently isolated from each other tooavoid single point of failures.</span></span> <span data-ttu-id="3baef-107">Il place automatiquement les disques de différentes machines virtuelles dans un ensemble de disponibilité dans différentes unités d’échelle de stockage (horodatages) qui limite l’impact hello de pannes d’unité de montée en puissance du stockage uniques dû en raison d’échecs toohardware et logiciels.</span><span class="sxs-lookup"><span data-stu-id="3baef-107">It automatically places disks of different VMs in an Availability Set in different Storage scale units (stamps) which limits hello impact of single Storage scale unit failures caused due toohardware and software failures.</span></span>
<span data-ttu-id="3baef-108">Selon vos besoins, vous avez le choix entre deux types d’options de stockage :</span><span class="sxs-lookup"><span data-stu-id="3baef-108">Based on your needs, you can choose from two types of storage options:</span></span>

- <span data-ttu-id="3baef-109">Les [disques gérés Premium](../../storage/common/storage-premium-storage.md) sont des supports basés sur des disques SSD (Solide State Drive) qui assurent de hautes performances et une faible latence pour les machines virtuelles dont les charges de travail nécessitent de nombreuses E/S.</span><span class="sxs-lookup"><span data-stu-id="3baef-109">[Premium Managed Disks](../../storage/common/storage-premium-storage.md) are Solid State Drive (SSD) based storage media which delivers highperformance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="3baef-110">Vous pouvez tirer parti de la vitesse de hello et les performances de ces disques par des disques gérés migration tooPremium.</span><span class="sxs-lookup"><span data-stu-id="3baef-110">You can take advantage of hello speed and performance of these disks by migrating tooPremium Managed Disks.</span></span>

- <span data-ttu-id="3baef-111">[Standard de disques gérés](../../storage/common/storage-standard-storage.md) utiliser le lecteur de disque dur (HDD) en fonction des supports de stockage et les mieux adaptés pour le développement et de Test et d’autres charges de travail peu fréquentes d’accès qui sont moins sensibles tooperformance variabilité.</span><span class="sxs-lookup"><span data-stu-id="3baef-111">[Standard Managed Disks](../../storage/common/storage-standard-storage.md) use Hard Disk Drive (HDD) based storage media and are best suited for Dev/Test and other infrequent access workloads that are less sensitive tooperformance variability.</span></span>

<span data-ttu-id="3baef-112">Vous pouvez migrer des disques tooManaged dans les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="3baef-112">You can migrate tooManaged Disks in following scenarios:</span></span>

| <span data-ttu-id="3baef-113">Migrer...</span><span class="sxs-lookup"><span data-stu-id="3baef-113">Migrate...</span></span>                                            | <span data-ttu-id="3baef-114">Lien vers la documentation</span><span class="sxs-lookup"><span data-stu-id="3baef-114">Documentation link</span></span>                                                                                                                                                                                                                                                                  |
|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3baef-115">Convertir des machines virtuelles de manière autonome et les machines virtuelles dans un jeu de disponibilité toomanaged des disques</span><span class="sxs-lookup"><span data-stu-id="3baef-115">Convert stand alone VMs and VMs in an availability set toomanaged disks</span></span>   | [<span data-ttu-id="3baef-116">Convertir les disques de machines virtuelles toouse géré</span><span class="sxs-lookup"><span data-stu-id="3baef-116">Convert VMs toouse managed disks</span></span>](convert-unmanaged-to-managed-disks.md) |
| <span data-ttu-id="3baef-117">Une seule machine virtuelle à partir de tooResource classique Manager sur des disques gérés</span><span class="sxs-lookup"><span data-stu-id="3baef-117">A single VM from classic tooResource Manager on managed disks</span></span>     | [<span data-ttu-id="3baef-118">Migrer une machine virtuelle unique</span><span class="sxs-lookup"><span data-stu-id="3baef-118">Migrate a single VM</span></span>](migrate-single-classic-to-resource-manager.md)  | 
| <span data-ttu-id="3baef-119">Tous les ordinateurs virtuels de hello dans un réseau virtuel à partir de tooResource classique Manager sur des disques gérés</span><span class="sxs-lookup"><span data-stu-id="3baef-119">All hello VMs in a vNet from classic tooResource Manager on managed disks</span></span>     | <span data-ttu-id="3baef-120">[Migrer les ressources IaaS classique tooResource Manager](migration-classic-resource-manager-ps.md) , puis [convertir un ordinateur virtuel à partir de disques toomanaged de disques non managé](convert-unmanaged-to-managed-disks.md)</span><span class="sxs-lookup"><span data-stu-id="3baef-120">[Migrate IaaS resources from classic tooResource Manager](migration-classic-resource-manager-ps.md) and then [Convert a VM from unmanaged disks toomanaged disks](convert-unmanaged-to-managed-disks.md)</span></span> | 






## <a name="plan-for-hello-conversion-toomanaged-disks"></a><span data-ttu-id="3baef-121">Planifier pour la conversion de hello tooManaged disques</span><span class="sxs-lookup"><span data-stu-id="3baef-121">Plan for hello conversion tooManaged Disks</span></span>

<span data-ttu-id="3baef-122">Cette section vous aide à toomake hello meilleure décision sur les types de machine virtuelle et le disque.</span><span class="sxs-lookup"><span data-stu-id="3baef-122">This section helps you toomake hello best decision on VM and disk types.</span></span>


## <a name="location"></a><span data-ttu-id="3baef-123">Lieu</span><span class="sxs-lookup"><span data-stu-id="3baef-123">Location</span></span>

<span data-ttu-id="3baef-124">Choisissez un emplacement où Azure Managed Disks est disponible.</span><span class="sxs-lookup"><span data-stu-id="3baef-124">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="3baef-125">Si vous déplacez des disques gérés tooPremium, vérifiez également que le stockage Premium est disponible dans la région de hello lorsque vous prévoyez de toomove à.</span><span class="sxs-lookup"><span data-stu-id="3baef-125">If you are moving tooPremium Managed Disks, also ensure that Premium storage is available in hello region where you are planning toomove to.</span></span> <span data-ttu-id="3baef-126">Pour obtenir des informations à jour sur les emplacements disponibles, consultez [Services Azure par région](https://azure.microsoft.com/regions/#services) .</span><span class="sxs-lookup"><span data-stu-id="3baef-126">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

## <a name="vm-sizes"></a><span data-ttu-id="3baef-127">Tailles de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3baef-127">VM sizes</span></span>

<span data-ttu-id="3baef-128">Si vous effectuez une migration tooPremium des disques gérés, vous tooupdate hello taille êtes de hello VM tooPremium taille capable de stockage disponible dans la région de hello où se trouve la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3baef-128">If you are migrating tooPremium Managed Disks, you have tooupdate hello size of hello VM tooPremium Storage capable size available in hello region where VM is located.</span></span> <span data-ttu-id="3baef-129">Passez en revue les tailles de machine virtuelle hello qui sont capables de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="3baef-129">Review hello VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="3baef-130">spécifications de taille de machine virtuelle Azure Hello sont répertoriées dans [tailles des machines virtuelles](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="3baef-130">hello Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="3baef-131">Passez en revue les caractéristiques de performances hello d’ordinateurs virtuels qui fonctionnent avec un stockage Premium et choisissez hello plus approprié taille de machine virtuelle qui convient le mieux à votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="3baef-131">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="3baef-132">Assurez-vous qu’il y suffisamment de bande passante disponible sur votre trafic de disque de machine virtuelle toodrive hello.</span><span class="sxs-lookup"><span data-stu-id="3baef-132">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

## <a name="disk-sizes"></a><span data-ttu-id="3baef-133">Tailles du disque</span><span class="sxs-lookup"><span data-stu-id="3baef-133">Disk sizes</span></span>

<span data-ttu-id="3baef-134">**Disques gérés Premium**</span><span class="sxs-lookup"><span data-stu-id="3baef-134">**Premium Managed Disks**</span></span>

<span data-ttu-id="3baef-135">Il existe sept types de disques gérés Premium qui peuvent être utilisés avec votre machine virtuelle, chacun d’eux présentant des limites d’E/S par seconde et de débit spécifiques.</span><span class="sxs-lookup"><span data-stu-id="3baef-135">There are seven types of premium managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="3baef-136">Prenez en compte ces limites lorsque vous choisissez hello le type de disque Premium pour votre machine virtuelle en fonction des besoins de hello de votre application en termes de capacité, les performances, l’évolutivité, et des pics.</span><span class="sxs-lookup"><span data-stu-id="3baef-136">Take into consideration these limits when choosing hello Premium disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="3baef-137">Type de disque Premium</span><span class="sxs-lookup"><span data-stu-id="3baef-137">Premium Disks Type</span></span>  | <span data-ttu-id="3baef-138">P4</span><span class="sxs-lookup"><span data-stu-id="3baef-138">P4</span></span>    | <span data-ttu-id="3baef-139">P6</span><span class="sxs-lookup"><span data-stu-id="3baef-139">P6</span></span>    | <span data-ttu-id="3baef-140">P10</span><span class="sxs-lookup"><span data-stu-id="3baef-140">P10</span></span>   | <span data-ttu-id="3baef-141">P20</span><span class="sxs-lookup"><span data-stu-id="3baef-141">P20</span></span>   | <span data-ttu-id="3baef-142">P30</span><span class="sxs-lookup"><span data-stu-id="3baef-142">P30</span></span>   | <span data-ttu-id="3baef-143">P40</span><span class="sxs-lookup"><span data-stu-id="3baef-143">P40</span></span>   | <span data-ttu-id="3baef-144">P50</span><span class="sxs-lookup"><span data-stu-id="3baef-144">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="3baef-145">Taille du disque</span><span class="sxs-lookup"><span data-stu-id="3baef-145">Disk size</span></span>           | <span data-ttu-id="3baef-146">128 Go</span><span class="sxs-lookup"><span data-stu-id="3baef-146">128 GB</span></span>| <span data-ttu-id="3baef-147">512 Go</span><span class="sxs-lookup"><span data-stu-id="3baef-147">512 GB</span></span>| <span data-ttu-id="3baef-148">128 Go</span><span class="sxs-lookup"><span data-stu-id="3baef-148">128 GB</span></span>| <span data-ttu-id="3baef-149">512 Go</span><span class="sxs-lookup"><span data-stu-id="3baef-149">512 GB</span></span>            | <span data-ttu-id="3baef-150">1024 Go (1 To)</span><span class="sxs-lookup"><span data-stu-id="3baef-150">1024 GB (1 TB)</span></span>    | <span data-ttu-id="3baef-151">2 048 Go (2 To)</span><span class="sxs-lookup"><span data-stu-id="3baef-151">2048 GB (2 TB)</span></span>    | <span data-ttu-id="3baef-152">4 095 Go (4 To)</span><span class="sxs-lookup"><span data-stu-id="3baef-152">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="3baef-153">IOPS par disque</span><span class="sxs-lookup"><span data-stu-id="3baef-153">IOPS per disk</span></span>       | <span data-ttu-id="3baef-154">120</span><span class="sxs-lookup"><span data-stu-id="3baef-154">120</span></span>   | <span data-ttu-id="3baef-155">240</span><span class="sxs-lookup"><span data-stu-id="3baef-155">240</span></span>   | <span data-ttu-id="3baef-156">500</span><span class="sxs-lookup"><span data-stu-id="3baef-156">500</span></span>   | <span data-ttu-id="3baef-157">2 300</span><span class="sxs-lookup"><span data-stu-id="3baef-157">2300</span></span>              | <span data-ttu-id="3baef-158">5 000</span><span class="sxs-lookup"><span data-stu-id="3baef-158">5000</span></span>              | <span data-ttu-id="3baef-159">7500</span><span class="sxs-lookup"><span data-stu-id="3baef-159">7500</span></span>              | <span data-ttu-id="3baef-160">7500</span><span class="sxs-lookup"><span data-stu-id="3baef-160">7500</span></span>              | 
| <span data-ttu-id="3baef-161">Débit par disque</span><span class="sxs-lookup"><span data-stu-id="3baef-161">Throughput per disk</span></span> | <span data-ttu-id="3baef-162">25 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3baef-162">25 MB per second</span></span>  | <span data-ttu-id="3baef-163">50 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3baef-163">50 MB per second</span></span>  | <span data-ttu-id="3baef-164">100 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3baef-164">100 MB per second</span></span> | <span data-ttu-id="3baef-165">150 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3baef-165">150 MB per second</span></span> | <span data-ttu-id="3baef-166">200 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3baef-166">200 MB per second</span></span> | <span data-ttu-id="3baef-167">250 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3baef-167">250 MB per second</span></span> | <span data-ttu-id="3baef-168">250 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3baef-168">250 MB per second</span></span> |

<span data-ttu-id="3baef-169">**Disques gérés Standard**</span><span class="sxs-lookup"><span data-stu-id="3baef-169">**Standard Managed Disks**</span></span>

<span data-ttu-id="3baef-170">Il existe sept types de disques gérés Standard qui peuvent être utilisés avec votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3baef-170">There are seven types of standard managed disks that can be used with your VM.</span></span> <span data-ttu-id="3baef-171">Chacun d’eux dispose d’une capacité différente, mais ils partagent les mêmes limites d’E/S par seconde et de débit.</span><span class="sxs-lookup"><span data-stu-id="3baef-171">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="3baef-172">Choisissez le type hello de disques gérés Standard selon les besoins en capacité hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="3baef-172">Choose hello type of Standard Managed disks based on hello capacity needs of your application.</span></span>

| <span data-ttu-id="3baef-173">Type de disque Standard</span><span class="sxs-lookup"><span data-stu-id="3baef-173">Standard Disk Type</span></span>  | <span data-ttu-id="3baef-174">S4</span><span class="sxs-lookup"><span data-stu-id="3baef-174">S4</span></span>               | <span data-ttu-id="3baef-175">S6</span><span class="sxs-lookup"><span data-stu-id="3baef-175">S6</span></span>               | <span data-ttu-id="3baef-176">S10</span><span class="sxs-lookup"><span data-stu-id="3baef-176">S10</span></span>              | <span data-ttu-id="3baef-177">S20</span><span class="sxs-lookup"><span data-stu-id="3baef-177">S20</span></span>              | <span data-ttu-id="3baef-178">S30</span><span class="sxs-lookup"><span data-stu-id="3baef-178">S30</span></span>              | <span data-ttu-id="3baef-179">S40</span><span class="sxs-lookup"><span data-stu-id="3baef-179">S40</span></span>              | <span data-ttu-id="3baef-180">S50</span><span class="sxs-lookup"><span data-stu-id="3baef-180">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="3baef-181">Taille du disque</span><span class="sxs-lookup"><span data-stu-id="3baef-181">Disk size</span></span>           | <span data-ttu-id="3baef-182">30 Go</span><span class="sxs-lookup"><span data-stu-id="3baef-182">30 GB</span></span>            | <span data-ttu-id="3baef-183">64 Go</span><span class="sxs-lookup"><span data-stu-id="3baef-183">64 GB</span></span>            | <span data-ttu-id="3baef-184">128 Go</span><span class="sxs-lookup"><span data-stu-id="3baef-184">128 GB</span></span>           | <span data-ttu-id="3baef-185">512 Go</span><span class="sxs-lookup"><span data-stu-id="3baef-185">512 GB</span></span>           | <span data-ttu-id="3baef-186">1024 Go (1 To)</span><span class="sxs-lookup"><span data-stu-id="3baef-186">1024 GB (1 TB)</span></span>   | <span data-ttu-id="3baef-187">2 048 Go (2 To)</span><span class="sxs-lookup"><span data-stu-id="3baef-187">2048 GB (2TB)</span></span>    | <span data-ttu-id="3baef-188">4 095 Go (4 To)</span><span class="sxs-lookup"><span data-stu-id="3baef-188">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="3baef-189">IOPS par disque</span><span class="sxs-lookup"><span data-stu-id="3baef-189">IOPS per disk</span></span>       | <span data-ttu-id="3baef-190">500</span><span class="sxs-lookup"><span data-stu-id="3baef-190">500</span></span>              | <span data-ttu-id="3baef-191">500</span><span class="sxs-lookup"><span data-stu-id="3baef-191">500</span></span>              | <span data-ttu-id="3baef-192">500</span><span class="sxs-lookup"><span data-stu-id="3baef-192">500</span></span>              | <span data-ttu-id="3baef-193">500</span><span class="sxs-lookup"><span data-stu-id="3baef-193">500</span></span>              | <span data-ttu-id="3baef-194">500</span><span class="sxs-lookup"><span data-stu-id="3baef-194">500</span></span>              | <span data-ttu-id="3baef-195">500</span><span class="sxs-lookup"><span data-stu-id="3baef-195">500</span></span>             | <span data-ttu-id="3baef-196">500</span><span class="sxs-lookup"><span data-stu-id="3baef-196">500</span></span>              | 
| <span data-ttu-id="3baef-197">Débit par disque</span><span class="sxs-lookup"><span data-stu-id="3baef-197">Throughput per disk</span></span> | <span data-ttu-id="3baef-198">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3baef-198">60 MB per second</span></span> | <span data-ttu-id="3baef-199">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3baef-199">60 MB per second</span></span> | <span data-ttu-id="3baef-200">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3baef-200">60 MB per second</span></span> | <span data-ttu-id="3baef-201">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3baef-201">60 MB per second</span></span> | <span data-ttu-id="3baef-202">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3baef-202">60 MB per second</span></span> | <span data-ttu-id="3baef-203">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3baef-203">60 MB per second</span></span> | <span data-ttu-id="3baef-204">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3baef-204">60 MB per second</span></span> | 

## <a name="disk-caching-policy"></a><span data-ttu-id="3baef-205">Stratégie de mise en cache du disque</span><span class="sxs-lookup"><span data-stu-id="3baef-205">Disk caching policy</span></span>

<span data-ttu-id="3baef-206">**Disques gérés Premium**</span><span class="sxs-lookup"><span data-stu-id="3baef-206">**Premium Managed Disks**</span></span>

<span data-ttu-id="3baef-207">Par défaut, la mise en cache de stratégie est *en lecture seule* pour tous les hello disques de données Premium, et *en lecture-écriture* hello Premium système d’exploitation attaché toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3baef-207">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="3baef-208">Ce paramètre de configuration est recommandé tooachieve hello des performances optimales IOs de votre application.</span><span class="sxs-lookup"><span data-stu-id="3baef-208">This configuration setting is recommended tooachieve hello optimal performance for your application’s IOs.</span></span> <span data-ttu-id="3baef-209">Pour les disques de données en écriture seule ou avec d'importantes opérations d'écriture (par ex., les fichiers journaux de SQL Server), désactivez la mise en cache du disque pour de meilleures performances de l'application.</span><span class="sxs-lookup"><span data-stu-id="3baef-209">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

## <a name="pricing"></a><span data-ttu-id="3baef-210">Tarification</span><span class="sxs-lookup"><span data-stu-id="3baef-210">Pricing</span></span>

<span data-ttu-id="3baef-211">Hello de révision [prix des disques gérés](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="3baef-211">Review hello [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="3baef-212">Tarification de disques gérés de Premium est identique hello les disques Premium non managé.</span><span class="sxs-lookup"><span data-stu-id="3baef-212">Pricing of Premium Managed Disks is same as hello Premium Unmanaged Disks.</span></span> <span data-ttu-id="3baef-213">En revanche, la tarification des disques gérés Standard est différente de celle des disques non gérés Standard.</span><span class="sxs-lookup"><span data-stu-id="3baef-213">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>



## <a name="next-steps"></a><span data-ttu-id="3baef-214">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3baef-214">Next steps</span></span>

- <span data-ttu-id="3baef-215">En savoir plus sur les [disques gérés](managed-disks-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3baef-215">Learn more about [Managed Disks](managed-disks-overview.md)</span></span>