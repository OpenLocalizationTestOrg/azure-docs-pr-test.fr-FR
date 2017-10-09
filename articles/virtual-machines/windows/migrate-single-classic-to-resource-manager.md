---
title: "aaaMigrate un tooan VM classique ARM gérés disque VM | Documents Microsoft"
description: "Migrer des machines virtuelles Azure à partir de déploiement classique de hello tooManaged des disques dans le modèle de déploiement du Gestionnaire de ressources hello de modèle."
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
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a><span data-ttu-id="3c264-103">Migrer manuellement un tooa VM classique ARM gérés disque machine virtuelle à partir de hello disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="3c264-103">Manually migrate a Classic VM tooa new ARM Managed Disk VM from hello VHD</span></span> 


<span data-ttu-id="3c264-104">Cette section vous aide à vous toomigrate vos machines virtuelles Azure existantes à partir du modèle de déploiement classique hello trop[disques gérés](managed-disks-overview.md) dans le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="3c264-104">This section helps you toomigrate your existing Azure VMs from hello classic deployment model too[Managed Disks](managed-disks-overview.md) in hello Resource Manager deployment model.</span></span>


## <a name="plan-for-hello-migration-toomanaged-disks"></a><span data-ttu-id="3c264-105">Planifier la migration de hello de tooManaged disques</span><span class="sxs-lookup"><span data-stu-id="3c264-105">Plan for hello migration tooManaged Disks</span></span>

<span data-ttu-id="3c264-106">Cette section vous aide à toomake hello meilleure décision sur les types de machine virtuelle et le disque.</span><span class="sxs-lookup"><span data-stu-id="3c264-106">This section helps you toomake hello best decision on VM and disk types.</span></span>


### <a name="location"></a><span data-ttu-id="3c264-107">Lieu</span><span class="sxs-lookup"><span data-stu-id="3c264-107">Location</span></span>

<span data-ttu-id="3c264-108">Choisissez un emplacement où Azure Managed Disks est disponible.</span><span class="sxs-lookup"><span data-stu-id="3c264-108">Pick a location where Azure Managed Disks are available.</span></span> <span data-ttu-id="3c264-109">Si vous migrez des disques gérés tooPremium, vérifiez également que le stockage Premium est disponible dans la région de hello lorsque vous prévoyez de toomigrate à.</span><span class="sxs-lookup"><span data-stu-id="3c264-109">If you are migrating tooPremium Managed Disks, also ensure that Premium storage is available in hello region where you are planning toomigrate to.</span></span> <span data-ttu-id="3c264-110">Pour obtenir des informations à jour sur les emplacements disponibles, consultez [Services Azure par région](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="3c264-110">See [Azure Services byRegion](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="3c264-111">Tailles de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3c264-111">VM sizes</span></span>

<span data-ttu-id="3c264-112">Si vous effectuez une migration tooPremium des disques gérés, vous tooupdate hello taille êtes de hello VM tooPremium taille capable de stockage disponible dans la région de hello où se trouve la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3c264-112">If you are migrating tooPremium Managed Disks, you have tooupdate hello size of hello VM tooPremium Storage capable size available in hello region where VM is located.</span></span> <span data-ttu-id="3c264-113">Passez en revue les tailles de machine virtuelle hello qui sont capables de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="3c264-113">Review hello VM sizes that are Premium Storage capable.</span></span> <span data-ttu-id="3c264-114">spécifications de taille de machine virtuelle Azure Hello sont répertoriées dans [tailles des machines virtuelles](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="3c264-114">hello Azure VM size specifications are listed in [Sizes for virtual machines](sizes.md).</span></span>
<span data-ttu-id="3c264-115">Passez en revue les caractéristiques de performances hello d’ordinateurs virtuels qui fonctionnent avec un stockage Premium et choisissez hello plus approprié taille de machine virtuelle qui convient le mieux à votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="3c264-115">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="3c264-116">Assurez-vous qu’il y suffisamment de bande passante disponible sur votre trafic de disque de machine virtuelle toodrive hello.</span><span class="sxs-lookup"><span data-stu-id="3c264-116">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

### <a name="disk-sizes"></a><span data-ttu-id="3c264-117">Tailles du disque</span><span class="sxs-lookup"><span data-stu-id="3c264-117">Disk sizes</span></span>

<span data-ttu-id="3c264-118">**Disques gérés Premium**</span><span class="sxs-lookup"><span data-stu-id="3c264-118">**Premium Managed Disks**</span></span>

<span data-ttu-id="3c264-119">Il existe sept types de disques gérés Premium qui peuvent être utilisés avec votre machine virtuelle, chacun d’eux présentant des limites d’E/S par seconde et de débit spécifiques.</span><span class="sxs-lookup"><span data-stu-id="3c264-119">There are seven types of premium Managed disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="3c264-120">Prendre en compte ces limites lorsque vous choisissez hello le type de disque Premium pour votre machine virtuelle en fonction des besoins de hello de votre application en termes de capacité, les performances, l’évolutivité, et des pics.</span><span class="sxs-lookup"><span data-stu-id="3c264-120">Consider these limits when choosing hello Premium disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="3c264-121">Type de disque Premium</span><span class="sxs-lookup"><span data-stu-id="3c264-121">Premium Disks Type</span></span>  | <span data-ttu-id="3c264-122">P4</span><span class="sxs-lookup"><span data-stu-id="3c264-122">P4</span></span>    | <span data-ttu-id="3c264-123">P6</span><span class="sxs-lookup"><span data-stu-id="3c264-123">P6</span></span>    | <span data-ttu-id="3c264-124">P10</span><span class="sxs-lookup"><span data-stu-id="3c264-124">P10</span></span>   | <span data-ttu-id="3c264-125">P20</span><span class="sxs-lookup"><span data-stu-id="3c264-125">P20</span></span>   | <span data-ttu-id="3c264-126">P30</span><span class="sxs-lookup"><span data-stu-id="3c264-126">P30</span></span>   | <span data-ttu-id="3c264-127">P40</span><span class="sxs-lookup"><span data-stu-id="3c264-127">P40</span></span>   | <span data-ttu-id="3c264-128">P50</span><span class="sxs-lookup"><span data-stu-id="3c264-128">P50</span></span>   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| <span data-ttu-id="3c264-129">Taille du disque</span><span class="sxs-lookup"><span data-stu-id="3c264-129">Disk size</span></span>           | <span data-ttu-id="3c264-130">128 Go</span><span class="sxs-lookup"><span data-stu-id="3c264-130">128 GB</span></span>| <span data-ttu-id="3c264-131">512 Go</span><span class="sxs-lookup"><span data-stu-id="3c264-131">512 GB</span></span>| <span data-ttu-id="3c264-132">128 Go</span><span class="sxs-lookup"><span data-stu-id="3c264-132">128 GB</span></span>| <span data-ttu-id="3c264-133">512 Go</span><span class="sxs-lookup"><span data-stu-id="3c264-133">512 GB</span></span>            | <span data-ttu-id="3c264-134">1024 Go (1 To)</span><span class="sxs-lookup"><span data-stu-id="3c264-134">1024 GB (1 TB)</span></span>    | <span data-ttu-id="3c264-135">2 048 Go (2 To)</span><span class="sxs-lookup"><span data-stu-id="3c264-135">2048 GB (2 TB)</span></span>    | <span data-ttu-id="3c264-136">4 095 Go (4 To)</span><span class="sxs-lookup"><span data-stu-id="3c264-136">4095 GB (4 TB)</span></span>    | 
| <span data-ttu-id="3c264-137">IOPS par disque</span><span class="sxs-lookup"><span data-stu-id="3c264-137">IOPS per disk</span></span>       | <span data-ttu-id="3c264-138">120</span><span class="sxs-lookup"><span data-stu-id="3c264-138">120</span></span>   | <span data-ttu-id="3c264-139">240</span><span class="sxs-lookup"><span data-stu-id="3c264-139">240</span></span>   | <span data-ttu-id="3c264-140">500</span><span class="sxs-lookup"><span data-stu-id="3c264-140">500</span></span>   | <span data-ttu-id="3c264-141">2 300</span><span class="sxs-lookup"><span data-stu-id="3c264-141">2300</span></span>              | <span data-ttu-id="3c264-142">5 000</span><span class="sxs-lookup"><span data-stu-id="3c264-142">5000</span></span>              | <span data-ttu-id="3c264-143">7500</span><span class="sxs-lookup"><span data-stu-id="3c264-143">7500</span></span>              | <span data-ttu-id="3c264-144">7500</span><span class="sxs-lookup"><span data-stu-id="3c264-144">7500</span></span>              | 
| <span data-ttu-id="3c264-145">Débit par disque</span><span class="sxs-lookup"><span data-stu-id="3c264-145">Throughput per disk</span></span> | <span data-ttu-id="3c264-146">25 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3c264-146">25 MB per second</span></span>  | <span data-ttu-id="3c264-147">50 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3c264-147">50 MB per second</span></span>  | <span data-ttu-id="3c264-148">100 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3c264-148">100 MB per second</span></span> | <span data-ttu-id="3c264-149">150 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3c264-149">150 MB per second</span></span> | <span data-ttu-id="3c264-150">200 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3c264-150">200 MB per second</span></span> | <span data-ttu-id="3c264-151">250 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3c264-151">250 MB per second</span></span> | <span data-ttu-id="3c264-152">250 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3c264-152">250 MB per second</span></span> | 

<span data-ttu-id="3c264-153">**Disques gérés Standard**</span><span class="sxs-lookup"><span data-stu-id="3c264-153">**Standard Managed Disks**</span></span>

<span data-ttu-id="3c264-154">Il existe sept types de disques gérés Standard qui peuvent être utilisés avec votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3c264-154">There are seven types of Standard Managed disks that can be used with your VM.</span></span> <span data-ttu-id="3c264-155">Chacun d’eux dispose d’une capacité différente, mais ils partagent les mêmes limites d’E/S par seconde et de débit.</span><span class="sxs-lookup"><span data-stu-id="3c264-155">Each of them have different capacity but have same IOPS and throughput limits.</span></span> <span data-ttu-id="3c264-156">Choisissez le type hello de disques gérés Standard selon les besoins en capacité hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="3c264-156">Choose hello type of Standard Managed disks based on hello capacity needs of your application.</span></span>

| <span data-ttu-id="3c264-157">Type de disque Standard</span><span class="sxs-lookup"><span data-stu-id="3c264-157">Standard Disk Type</span></span>  | <span data-ttu-id="3c264-158">S4</span><span class="sxs-lookup"><span data-stu-id="3c264-158">S4</span></span>               | <span data-ttu-id="3c264-159">S6</span><span class="sxs-lookup"><span data-stu-id="3c264-159">S6</span></span>               | <span data-ttu-id="3c264-160">S10</span><span class="sxs-lookup"><span data-stu-id="3c264-160">S10</span></span>              | <span data-ttu-id="3c264-161">S20</span><span class="sxs-lookup"><span data-stu-id="3c264-161">S20</span></span>              | <span data-ttu-id="3c264-162">S30</span><span class="sxs-lookup"><span data-stu-id="3c264-162">S30</span></span>              | <span data-ttu-id="3c264-163">S40</span><span class="sxs-lookup"><span data-stu-id="3c264-163">S40</span></span>              | <span data-ttu-id="3c264-164">S50</span><span class="sxs-lookup"><span data-stu-id="3c264-164">S50</span></span>              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| <span data-ttu-id="3c264-165">Taille du disque</span><span class="sxs-lookup"><span data-stu-id="3c264-165">Disk size</span></span>           | <span data-ttu-id="3c264-166">30 Go</span><span class="sxs-lookup"><span data-stu-id="3c264-166">30 GB</span></span>            | <span data-ttu-id="3c264-167">64 Go</span><span class="sxs-lookup"><span data-stu-id="3c264-167">64 GB</span></span>            | <span data-ttu-id="3c264-168">128 Go</span><span class="sxs-lookup"><span data-stu-id="3c264-168">128 GB</span></span>           | <span data-ttu-id="3c264-169">512 Go</span><span class="sxs-lookup"><span data-stu-id="3c264-169">512 GB</span></span>           | <span data-ttu-id="3c264-170">1024 Go (1 To)</span><span class="sxs-lookup"><span data-stu-id="3c264-170">1024 GB (1 TB)</span></span>   | <span data-ttu-id="3c264-171">2 048 Go (2 To)</span><span class="sxs-lookup"><span data-stu-id="3c264-171">2048 GB (2TB)</span></span>    | <span data-ttu-id="3c264-172">4 095 Go (4 To)</span><span class="sxs-lookup"><span data-stu-id="3c264-172">4095 GB (4 TB)</span></span>   | 
| <span data-ttu-id="3c264-173">IOPS par disque</span><span class="sxs-lookup"><span data-stu-id="3c264-173">IOPS per disk</span></span>       | <span data-ttu-id="3c264-174">500</span><span class="sxs-lookup"><span data-stu-id="3c264-174">500</span></span>              | <span data-ttu-id="3c264-175">500</span><span class="sxs-lookup"><span data-stu-id="3c264-175">500</span></span>              | <span data-ttu-id="3c264-176">500</span><span class="sxs-lookup"><span data-stu-id="3c264-176">500</span></span>              | <span data-ttu-id="3c264-177">500</span><span class="sxs-lookup"><span data-stu-id="3c264-177">500</span></span>              | <span data-ttu-id="3c264-178">500</span><span class="sxs-lookup"><span data-stu-id="3c264-178">500</span></span>              | <span data-ttu-id="3c264-179">500</span><span class="sxs-lookup"><span data-stu-id="3c264-179">500</span></span>             | <span data-ttu-id="3c264-180">500</span><span class="sxs-lookup"><span data-stu-id="3c264-180">500</span></span>              | 
| <span data-ttu-id="3c264-181">Débit par disque</span><span class="sxs-lookup"><span data-stu-id="3c264-181">Throughput per disk</span></span> | <span data-ttu-id="3c264-182">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3c264-182">60 MB per second</span></span> | <span data-ttu-id="3c264-183">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3c264-183">60 MB per second</span></span> | <span data-ttu-id="3c264-184">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3c264-184">60 MB per second</span></span> | <span data-ttu-id="3c264-185">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3c264-185">60 MB per second</span></span> | <span data-ttu-id="3c264-186">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3c264-186">60 MB per second</span></span> | <span data-ttu-id="3c264-187">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3c264-187">60 MB per second</span></span> | <span data-ttu-id="3c264-188">60 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="3c264-188">60 MB per second</span></span> | 


### <a name="disk-caching-policy"></a><span data-ttu-id="3c264-189">Stratégie de mise en cache du disque</span><span class="sxs-lookup"><span data-stu-id="3c264-189">Disk caching policy</span></span> 

<span data-ttu-id="3c264-190">**Disques gérés Premium**</span><span class="sxs-lookup"><span data-stu-id="3c264-190">**Premium Managed Disks**</span></span>

<span data-ttu-id="3c264-191">Par défaut, la mise en cache de stratégie est *en lecture seule* pour tous les hello disques de données Premium, et *en lecture-écriture* hello Premium système d’exploitation attaché toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3c264-191">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="3c264-192">Ce paramètre de configuration est recommandé tooachieve hello des performances optimales IOs de votre application.</span><span class="sxs-lookup"><span data-stu-id="3c264-192">This configuration setting is recommended tooachieve hello optimal performance for your application’s IOs.</span></span> <span data-ttu-id="3c264-193">Pour les disques de données en écriture seule ou avec d'importantes opérations d'écriture (par ex., les fichiers journaux de SQL Server), désactivez la mise en cache du disque pour de meilleures performances de l'application.</span><span class="sxs-lookup"><span data-stu-id="3c264-193">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span>

### <a name="pricing"></a><span data-ttu-id="3c264-194">Tarification</span><span class="sxs-lookup"><span data-stu-id="3c264-194">Pricing</span></span>

<span data-ttu-id="3c264-195">Hello de révision [prix des disques gérés](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="3c264-195">Review hello [pricing for Managed Disks](https://azure.microsoft.com/en-us/pricing/details/managed-disks/).</span></span> <span data-ttu-id="3c264-196">Tarification de disques gérés de Premium est identique hello les disques Premium non managé.</span><span class="sxs-lookup"><span data-stu-id="3c264-196">Pricing of Premium Managed Disks is same as hello Premium Unmanaged Disks.</span></span> <span data-ttu-id="3c264-197">En revanche, la tarification des disques gérés Standard est différente de celle des disques non gérés Standard.</span><span class="sxs-lookup"><span data-stu-id="3c264-197">But pricing for Standard Managed Disks is different than Standard Unmanaged Disks.</span></span>


## <a name="checklist"></a><span data-ttu-id="3c264-198">Liste de contrôle</span><span class="sxs-lookup"><span data-stu-id="3c264-198">Checklist</span></span>

1.  <span data-ttu-id="3c264-199">Si vous migrez des disques gérés tooPremium, assurez-vous qu’il est disponible dans la région de hello que vous effectuez la migration.</span><span class="sxs-lookup"><span data-stu-id="3c264-199">If you are migrating tooPremium Managed Disks, make sure it is available in hello region you are migrating to.</span></span>

2.  <span data-ttu-id="3c264-200">Décidez nouvelle série VM hello, que vous allez utiliser.</span><span class="sxs-lookup"><span data-stu-id="3c264-200">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="3c264-201">Il doit être un stockage Premium compatibles si vous migrez des disques gérés tooPremium.</span><span class="sxs-lookup"><span data-stu-id="3c264-201">It should be a Premium Storage capable if you are migrating tooPremium Managed Disks.</span></span>

3.  <span data-ttu-id="3c264-202">Décidez hello exacte taille de machine virtuelle que vous utiliserez qui sont disponibles dans la région de hello que vous effectuez la migration.</span><span class="sxs-lookup"><span data-stu-id="3c264-202">Decide hello exact VM size you will use which are available in hello region you are migrating to.</span></span> <span data-ttu-id="3c264-203">Taille de machine virtuelle doit toobe toosupport suffisamment grand hello différents disques de données que vous avez.</span><span class="sxs-lookup"><span data-stu-id="3c264-203">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="3c264-204">Par exemple, si vous avez quatre disques de données, hello machine virtuelle doit avoir deux ou plusieurs noyaux.</span><span class="sxs-lookup"><span data-stu-id="3c264-204">For example, if you have four data disks, hello VM must have two or more cores.</span></span> <span data-ttu-id="3c264-205">Prenez également en considération les besoins en puissance, mémoire et bande passante réseau.</span><span class="sxs-lookup"><span data-stu-id="3c264-205">Also, consider processing power, memory and network bandwidth needs.</span></span>

4.  <span data-ttu-id="3c264-206">Des informations VM hello en cours pratiques, y compris les listes de hello des disques et des objets BLOB de disque dur virtuel correspondant.</span><span class="sxs-lookup"><span data-stu-id="3c264-206">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="3c264-207">Préparez votre application pour les interruptions de service.</span><span class="sxs-lookup"><span data-stu-id="3c264-207">Prepare your application for downtime.</span></span> <span data-ttu-id="3c264-208">toodo une nouvelle migration, vous avez toostop tout traitement hello dans le système actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="3c264-208">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="3c264-209">Alors seulement vous pouvez l’obtenir état tooconsistent dont vous pouvez migrer toohello nouvelle plateforme.</span><span class="sxs-lookup"><span data-stu-id="3c264-209">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="3c264-210">Temps d’arrêt dépend de la quantité de hello de données dans toomigrate de disques hello.</span><span class="sxs-lookup"><span data-stu-id="3c264-210">Downtime duration depends on hello amount of data in hello disks toomigrate.</span></span>


## <a name="migrate-hello-vm"></a><span data-ttu-id="3c264-211">Migrer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3c264-211">Migrate hello VM</span></span>

<span data-ttu-id="3c264-212">Préparez votre application pour les interruptions de service.</span><span class="sxs-lookup"><span data-stu-id="3c264-212">Prepare your application for downtime.</span></span> <span data-ttu-id="3c264-213">toodo une nouvelle migration, vous avez toostop tout traitement hello dans le système actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="3c264-213">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="3c264-214">Alors seulement vous pouvez l’obtenir état tooconsistent dont vous pouvez migrer toohello nouvelle plateforme.</span><span class="sxs-lookup"><span data-stu-id="3c264-214">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="3c264-215">Temps d’arrêt dépend de quantité hello d’hello disques toomigrate.</span><span class="sxs-lookup"><span data-stu-id="3c264-215">Downtime duration depends hello amount of data in hello disks toomigrate.</span></span>


1.  <span data-ttu-id="3c264-216">Tout d’abord, définissez les paramètres communs hello :</span><span class="sxs-lookup"><span data-stu-id="3c264-216">First, set hello common parameters:</span></span>

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

2.  <span data-ttu-id="3c264-217">Créer un disque du système d’exploitation géré à l’aide de hello disque dur virtuel à partir de hello VM classique.</span><span class="sxs-lookup"><span data-stu-id="3c264-217">Create a managed OS disk using hello VHD from hello classic VM.</span></span>

    <span data-ttu-id="3c264-218">Assurez-vous d’avoir fourni hello compléter URI Hello paramètre toohello $osVhdUri de disque dur virtuel du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="3c264-218">Ensure that you have provided hello complete URI of hello OS VHD toohello $osVhdUri parameter.</span></span> <span data-ttu-id="3c264-219">De plus, dans **Type de compte**, indiquez **PremiumLRS** ou **StandardLRS** selon le type de disque (Premium ou Standard) vers lequel vous effectuez la migration.</span><span class="sxs-lookup"><span data-stu-id="3c264-219">Also, enter **-AccountType** as **PremiumLRS** or **StandardLRS** based on type of disks (Premium or Standard) you are migrating to.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  <span data-ttu-id="3c264-220">Attacher hello du système d’exploitation disque toohello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3c264-220">Attach hello OS disk toohello new VM.</span></span>

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  <span data-ttu-id="3c264-221">Créer un disque de données managées à partir du fichier de disque dur virtuel de données hello et l’ajouter toohello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3c264-221">Create a managed data disk from hello data VHD file and add it toohello new VM.</span></span>

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  <span data-ttu-id="3c264-222">Créer hello du nouvel ordinateur virtuel par définition publique IP, réseau virtuel et carte réseau.</span><span class="sxs-lookup"><span data-stu-id="3c264-222">Create hello new VM by setting public IP, Virtual Network and NIC.</span></span>

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
><span data-ttu-id="3c264-223">Il peut y avoir toosupport nécessaire des étapes supplémentaires votre application est ne pas couvert par ce guide.</span><span class="sxs-lookup"><span data-stu-id="3c264-223">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="3c264-224">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3c264-224">Next steps</span></span>

- <span data-ttu-id="3c264-225">Connecter l’ordinateur virtuel de toohello.</span><span class="sxs-lookup"><span data-stu-id="3c264-225">Connect toohello virtual machine.</span></span> <span data-ttu-id="3c264-226">Pour obtenir des instructions, consultez [comment tooconnect et ouverture de session tooan Azure virtual machine exécutant Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3c264-226">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

