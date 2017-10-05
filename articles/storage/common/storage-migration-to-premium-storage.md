---
title: Migration de machines virtuelles vers le stockage Azure Premium | Microsoft Docs
description: "Migrez vos machines virtuelles existantes vers le stockage Azure Premium. Premium Storage offre une prise en charge très performante et à faible latence des disques pour les charges de travail utilisant beaucoup d'E/S exécutées sur les machines virtuelles Azure."
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: ca893f87b155a92c457e3bf6d9d39aaf86bf5fb3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="migrating-to-azure-premium-storage-unmanaged-disks"></a><span data-ttu-id="32a46-104">Migration vers le stockage Azure Premium (disques non gérés)</span><span class="sxs-lookup"><span data-stu-id="32a46-104">Migrating to Azure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="32a46-105">Cet article explique comment migrer une machine virtuelle qui utilise des disques standard non gérés vers une machine virtuelle qui utilise des disques premium non gérés.</span><span class="sxs-lookup"><span data-stu-id="32a46-105">This article discusses how to migrate a VM that uses unmanaged standard disks to a VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="32a46-106">Nous vous recommandons d’utiliser Azure Managed Disks pour les nouvelles machines virtuelles et de convertir vos anciens disques non gérés en disques gérés.</span><span class="sxs-lookup"><span data-stu-id="32a46-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks to managed disks.</span></span> <span data-ttu-id="32a46-107">Azure Managed Disks gère les comptes de stockage sous-jacents à votre place.</span><span class="sxs-lookup"><span data-stu-id="32a46-107">Managed Disks handle the underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="32a46-108">Pour plus d’informations, consultez [Vue d’ensemble d’Azure Managed Disks](../../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32a46-108">For more information, please see our [Managed Disks Overview](../../virtual-machines/windows/managed-disks-overview.md).</span></span>
>

<span data-ttu-id="32a46-109">Azure Premium Storage offre une prise en charge très performante et à faible latence des disques pour les machines virtuelles exécutant des charges de travail qui utilisent beaucoup d'E/S.</span><span class="sxs-lookup"><span data-stu-id="32a46-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="32a46-110">Vous pouvez migrer les disques de machine virtuelle de votre application dans Azure Premium Storage pour tirer parti de la vitesse et des performances de ces disques.</span><span class="sxs-lookup"><span data-stu-id="32a46-110">You can take advantage of the speed and performance of these disks by migrating your application's VM disks to Azure Premium Storage.</span></span>

<span data-ttu-id="32a46-111">L’objectif de ce guide est d’aider les nouveaux utilisateurs d’Azure Premium Storage à mieux se préparer pour effectuer une transition en douceur de leur système actuel vers Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="32a46-111">The purpose of this guide is to help new users of Azure Premium Storage better prepare to make a smooth transition from their current system to Premium Storage.</span></span> <span data-ttu-id="32a46-112">Le guide traite des trois composants clés inclus dans ce processus :</span><span class="sxs-lookup"><span data-stu-id="32a46-112">The guide addresses three of the key components in this process:</span></span>

* [<span data-ttu-id="32a46-113">Planification de la migration vers Premium Storage</span><span class="sxs-lookup"><span data-stu-id="32a46-113">Plan for the Migration to Premium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="32a46-114">Préparation et copie de disques durs virtuels (VHD) vers le stockage Premium</span><span class="sxs-lookup"><span data-stu-id="32a46-114">Prepare and Copy Virtual Hard Disks (VHDs) to Premium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="32a46-115">Création d’une machine virtuelle Azure utilisant Premium Storage</span><span class="sxs-lookup"><span data-stu-id="32a46-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="32a46-116">Vous pouvez migrer des machines virtuelles d’autres plateformes vers Azure Premium Storage ou migrer des machines virtuelles Azure existantes du stockage Standard vers le stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="32a46-116">You can either migrate VMs from other platforms to Azure Premium Storage or migrate existing Azure VMs from Standard Storage to Premium Storage.</span></span> <span data-ttu-id="32a46-117">Ce guide décrit les étapes pour les deux scénarios.</span><span class="sxs-lookup"><span data-stu-id="32a46-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="32a46-118">Suivez les étapes spécifiées dans la section appropriée selon votre scénario.</span><span class="sxs-lookup"><span data-stu-id="32a46-118">Follow the steps specified in the relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="32a46-119">Vous pouvez consulter un aperçu des fonctionnalités et de la tarification dans [Premium Storage : stockage hautes performances pour les charges de travail des machines virtuelles Azure](storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="32a46-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="32a46-120">Nous vous recommandons de migrer les disques de machine virtuelle nécessitant un nombre élevé d’IOPS dans Azure Premium Storage pour que votre application bénéficie de performances optimales.</span><span class="sxs-lookup"><span data-stu-id="32a46-120">We recommend migrating any virtual machine disk requiring high IOPS to Azure Premium Storage for the best performance for your application.</span></span> <span data-ttu-id="32a46-121">Si votre disque ne nécessite pas un nombre élevé d'IOPS, vous pouvez limiter les coûts en le conservant dans le stockage Standard qui stocke les données de disque de machine virtuelle sur des disques durs et non des disques SSD.</span><span class="sxs-lookup"><span data-stu-id="32a46-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="32a46-122">L’exécution du processus de migration dans son intégralité peut nécessiter des actions supplémentaires précédant et suivant les étapes fournies dans ce guide.</span><span class="sxs-lookup"><span data-stu-id="32a46-122">Completing the migration process in its entirety may require additional actions both before and after the steps provided in this guide.</span></span> <span data-ttu-id="32a46-123">Par exemple, la configuration de réseaux virtuels ou de points de terminaison ou l’intégration de modifications de code dans l’application elle-même, ce qui peut nécessiter un certain temps d’indisponibilité dans votre application.</span><span class="sxs-lookup"><span data-stu-id="32a46-123">Examples include configuring virtual networks or endpoints or making code changes within the application itself which may require some downtime in your application.</span></span> <span data-ttu-id="32a46-124">Ces actions sont propres à chaque application, et vous devez les exécuter en plus des étapes indiquées dans ce guide pour effectuer la transition complète vers Premium Storage de manière aussi transparente que possible.</span><span class="sxs-lookup"><span data-stu-id="32a46-124">These actions are unique to each application, and you should complete them along with the steps provided in this guide to make the full transition to Premium Storage as seamless as possible.</span></span>

## <span data-ttu-id="32a46-125"><a name="plan-the-migration-to-premium-storage"></a>Planification de la migration vers Premium Storage</span><span class="sxs-lookup"><span data-stu-id="32a46-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for the migration to Premium Storage</span></span>
<span data-ttu-id="32a46-126">Cette section vous permet de vous assurer que vous êtes prêt à suivre les étapes de migration de cet article et vous permet de prendre la bonne décision sur les types de machines virtuelles et de disques.</span><span class="sxs-lookup"><span data-stu-id="32a46-126">This section ensures that you are ready to follow the migration steps in this article, and helps you to make the best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="32a46-127">Composants requis</span><span class="sxs-lookup"><span data-stu-id="32a46-127">Prerequisites</span></span>
* <span data-ttu-id="32a46-128">Vous aurez besoin d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="32a46-128">You will need an Azure subscription.</span></span> <span data-ttu-id="32a46-129">Si vous n’en avez pas, vous pouvez souscrire un abonnement pour un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/) d’un mois ou visiter [Tarification Azure](https://azure.microsoft.com/pricing/) pour plus d’options.</span><span class="sxs-lookup"><span data-stu-id="32a46-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="32a46-130">Pour exécuter les applets de commande PowerShell, vous avez besoin du module Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32a46-130">To execute PowerShell cmdlets, you will need the Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="32a46-131">Consultez la rubrique [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) pour des instructions sur l’installation et le point d’installation.</span><span class="sxs-lookup"><span data-stu-id="32a46-131">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the install point and installation instructions.</span></span>
* <span data-ttu-id="32a46-132">Lorsque vous prévoyez d’utiliser des machines virtuelles Azure exécutées sur Premium Storage, vous devez utiliser les machines virtuelles compatibles Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="32a46-132">When you plan to use Azure VMs running on Premium Storage, you need to use the Premium Storage capable VMs.</span></span> <span data-ttu-id="32a46-133">Vous pouvez utiliser des disques de Stockage Standard et Premium avec les machines virtuelles compatibles avec Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="32a46-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="32a46-134">Les disques de stockage Premium seront bientôt disponibles avec plusieurs types de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="32a46-134">Premium storage disks will be available with more VM types in the future.</span></span> <span data-ttu-id="32a46-135">Pour plus d’informations sur les tailles et les types de disque de machine virtuelle Azure disponibles, consultez [Tailles des machines virtuelles](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) et [Tailles des services cloud](../../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="32a46-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="32a46-136">Considérations</span><span class="sxs-lookup"><span data-stu-id="32a46-136">Considerations</span></span>
<span data-ttu-id="32a46-137">Une machine virtuelle Azure prend en charge l’association de plusieurs disques Premium Storage afin que vos applications puissent avoir jusqu'à 256 To de stockage par machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="32a46-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up to 256 TB of storage per VM.</span></span> <span data-ttu-id="32a46-138">Avec Premium Storage, vos applications peuvent atteindre jusqu'à 80 000 IOPS (opérations d'E/S par seconde) par machine virtuelle et un débit de disque de 2 000 Mo par seconde, avec une latence extrêmement faible pour les opérations de lecture.</span><span class="sxs-lookup"><span data-stu-id="32a46-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="32a46-139">Vous disposez de diverses options de machines virtuelles et disques.</span><span class="sxs-lookup"><span data-stu-id="32a46-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="32a46-140">Cette section est là pour vous aider à trouver l’option qui correspond le mieux à votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="32a46-140">This section is to help you to find an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="32a46-141">Tailles de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="32a46-141">VM sizes</span></span>
<span data-ttu-id="32a46-142">Les spécifications des tailles des machines virtuelles Azure sont répertoriées dans la section [Tailles des machines virtuelles](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="32a46-142">The Azure VM size specifications are listed in [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="32a46-143">Passez en revue les caractéristiques de performances des machines virtuelles fonctionnant avec Premium Storage et choisissez la taille de machine virtuelle la mieux adaptée à votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="32a46-143">Review the performance characteristics of virtual machines that work with Premium Storage and choose the most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="32a46-144">Assurez-vous que la bande passante disponible est suffisante sur votre machine virtuelle pour gérer le trafic du disque.</span><span class="sxs-lookup"><span data-stu-id="32a46-144">Make sure that there is sufficient bandwidth available on your VM to drive the disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="32a46-145">Tailles du disque</span><span class="sxs-lookup"><span data-stu-id="32a46-145">Disk sizes</span></span>
<span data-ttu-id="32a46-146">Il existe cinq types de disque qui peuvent être utilisés avec votre machine virtuelle et chacun d’eux présentant des limites d’E/S par seconde et de débits spécifiques.</span><span class="sxs-lookup"><span data-stu-id="32a46-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="32a46-147">Prenez en compte ces limites lors de la sélection du type de disque pour votre machine virtuelle en fonction des besoins de votre application en termes de capacité, de performances, d’extensibilité et de charges maximales.</span><span class="sxs-lookup"><span data-stu-id="32a46-147">Take into consideration these limits when choosing the disk type for your VM based on the needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="32a46-148">Type de disque Premium</span><span class="sxs-lookup"><span data-stu-id="32a46-148">Premium Disks Type</span></span>  | <span data-ttu-id="32a46-149">P10</span><span class="sxs-lookup"><span data-stu-id="32a46-149">P10</span></span>   | <span data-ttu-id="32a46-150">P20</span><span class="sxs-lookup"><span data-stu-id="32a46-150">P20</span></span>   | <span data-ttu-id="32a46-151">P30</span><span class="sxs-lookup"><span data-stu-id="32a46-151">P30</span></span>            | <span data-ttu-id="32a46-152">P40</span><span class="sxs-lookup"><span data-stu-id="32a46-152">P40</span></span>            | <span data-ttu-id="32a46-153">P50</span><span class="sxs-lookup"><span data-stu-id="32a46-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="32a46-154">Taille du disque</span><span class="sxs-lookup"><span data-stu-id="32a46-154">Disk size</span></span>           | <span data-ttu-id="32a46-155">128 Go</span><span class="sxs-lookup"><span data-stu-id="32a46-155">128 GB</span></span>| <span data-ttu-id="32a46-156">512 Go</span><span class="sxs-lookup"><span data-stu-id="32a46-156">512 GB</span></span>| <span data-ttu-id="32a46-157">1024 Go (1 To)</span><span class="sxs-lookup"><span data-stu-id="32a46-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="32a46-158">2 048 Go (2 To)</span><span class="sxs-lookup"><span data-stu-id="32a46-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="32a46-159">4 095 Go (4 To)</span><span class="sxs-lookup"><span data-stu-id="32a46-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="32a46-160">IOPS par disque</span><span class="sxs-lookup"><span data-stu-id="32a46-160">IOPS per disk</span></span>       | <span data-ttu-id="32a46-161">500</span><span class="sxs-lookup"><span data-stu-id="32a46-161">500</span></span>   | <span data-ttu-id="32a46-162">2 300</span><span class="sxs-lookup"><span data-stu-id="32a46-162">2300</span></span>  | <span data-ttu-id="32a46-163">5 000</span><span class="sxs-lookup"><span data-stu-id="32a46-163">5000</span></span>           | <span data-ttu-id="32a46-164">7500</span><span class="sxs-lookup"><span data-stu-id="32a46-164">7500</span></span>           | <span data-ttu-id="32a46-165">7500</span><span class="sxs-lookup"><span data-stu-id="32a46-165">7500</span></span>           | 
| <span data-ttu-id="32a46-166">Débit par disque</span><span class="sxs-lookup"><span data-stu-id="32a46-166">Throughput per disk</span></span> | <span data-ttu-id="32a46-167">100 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="32a46-167">100 MB per second</span></span> | <span data-ttu-id="32a46-168">150 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="32a46-168">150 MB per second</span></span> | <span data-ttu-id="32a46-169">200 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="32a46-169">200 MB per second</span></span> | <span data-ttu-id="32a46-170">250 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="32a46-170">250 MB per second</span></span> | <span data-ttu-id="32a46-171">250 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="32a46-171">250 MB per second</span></span> |

<span data-ttu-id="32a46-172">En fonction de votre charge de travail, déterminez si les disques de données supplémentaires sont nécessaires pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="32a46-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="32a46-173">Vous pouvez joindre plusieurs disques de données persistantes à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="32a46-173">You can attach several persistent data disks to your VM.</span></span> <span data-ttu-id="32a46-174">Si nécessaire, vous pouvez répartir les données sur les disques pour augmenter la capacité et les performances du volume.</span><span class="sxs-lookup"><span data-stu-id="32a46-174">If needed, you can stripe across the disks to increase the capacity and performance of the volume.</span></span> <span data-ttu-id="32a46-175">(Découvrez ce qu’est l’entrelacement de disques [ici](storage-premium-storage-performance.md#disk-striping).) Si vous équilibrez les disques de données Stockage Premium à l’aide des [espaces de stockage][4], vous devez les configurer avec une colonne pour chaque disque utilisé.</span><span class="sxs-lookup"><span data-stu-id="32a46-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="32a46-176">Dans le cas contraire, les performances globales du volume agrégé par bandes peuvent être limitées, en raison d'une distribution inégale du trafic sur les disques.</span><span class="sxs-lookup"><span data-stu-id="32a46-176">Otherwise, the overall performance of the striped volume may be lower than expected due to uneven distribution of traffic across the disks.</span></span> <span data-ttu-id="32a46-177">Pour les machines virtuelles Linux, vous pouvez utiliser l’utilitaire *mdadm* pour obtenir le même résultat.</span><span class="sxs-lookup"><span data-stu-id="32a46-177">For Linux VMs you can use the *mdadm* utility to achieve the same.</span></span> <span data-ttu-id="32a46-178">Consultez l’article [Configuration d’un RAID logiciel sur Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="32a46-178">See article [Configure Software RAID on Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="32a46-179">Objectifs d’évolutivité de compte de stockage</span><span class="sxs-lookup"><span data-stu-id="32a46-179">Storage account scalability targets</span></span>
<span data-ttu-id="32a46-180">Les comptes de stockage Premium ont les objectifs d’évolutivité suivants en plus des [Objectifs d’évolutivité et de performances de stockage Azure](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="32a46-180">Premium Storage accounts have the following scalability targets in addition to the [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="32a46-181">Si les besoins de votre application dépassent les objectifs d’évolutivité d’un compte de stockage unique, générez votre application pour qu’elle utilise plusieurs comptes de stockage et partitionnez vos données sur ces comptes.</span><span class="sxs-lookup"><span data-stu-id="32a46-181">If your application requirements exceed the scalability targets of a single storage account, build your application to use multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="32a46-182">Capacité totale des comptes</span><span class="sxs-lookup"><span data-stu-id="32a46-182">Total Account Capacity</span></span> | <span data-ttu-id="32a46-183">Bande passante totale pour un compte de stockage localement redondant</span><span class="sxs-lookup"><span data-stu-id="32a46-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="32a46-184">Capacité du disque : 35 To</span><span class="sxs-lookup"><span data-stu-id="32a46-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="32a46-185">Capacité d’instantané : 10 To</span><span class="sxs-lookup"><span data-stu-id="32a46-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="32a46-186">Jusqu'à 50 Go par seconde pour les données entrantes/sortantes</span><span class="sxs-lookup"><span data-stu-id="32a46-186">Up to 50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="32a46-187">Pour plus d’informations sur les spécifications de Premium Storage, consultez la page [Objectifs d’évolutivité et de performances lors de l’utilisation de Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="32a46-187">For the more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="32a46-188">Stratégie de mise en cache du disque</span><span class="sxs-lookup"><span data-stu-id="32a46-188">Disk caching policy</span></span>
<span data-ttu-id="32a46-189">Par défaut, la stratégie de mise en cache est *Lecture seule* pour tous les disques de données Premium et *Lecture-écriture* pour le disque du système d’exploitation Premium attaché à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="32a46-189">By default, disk caching policy is *Read-Only* for all the Premium data disks, and *Read-Write* for the Premium operating system disk attached to the VM.</span></span> <span data-ttu-id="32a46-190">Ce paramètre de configuration est recommandé pour optimiser les performances des E/S de votre application.</span><span class="sxs-lookup"><span data-stu-id="32a46-190">This configuration setting is recommended to achieve the optimal performance for your application's IOs.</span></span> <span data-ttu-id="32a46-191">Pour les disques de données en écriture seule ou avec d'importantes opérations d'écriture (par ex., les fichiers journaux de SQL Server), désactivez la mise en cache du disque pour de meilleures performances de l'application.</span><span class="sxs-lookup"><span data-stu-id="32a46-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="32a46-192">Les paramètres du cache pour les disques de données existants peuvent être mis à jour à l’aide du [portail Azure Portal](https://portal.azure.com) ou du paramètre *-HostCaching* de l’applet de commande *Set-AzureDataDisk*.</span><span class="sxs-lookup"><span data-stu-id="32a46-192">The cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or the *-HostCaching* parameter of the *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="32a46-193">Lieu</span><span class="sxs-lookup"><span data-stu-id="32a46-193">Location</span></span>
<span data-ttu-id="32a46-194">Choisissez un emplacement où le stockage Azure Premium est disponible.</span><span class="sxs-lookup"><span data-stu-id="32a46-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="32a46-195">Pour obtenir des informations à jour sur les emplacements disponibles, consultez [Services Azure par région](https://azure.microsoft.com/regions/#services) .</span><span class="sxs-lookup"><span data-stu-id="32a46-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="32a46-196">Les machines virtuelles situées dans la même région que le compte de stockage qui stocke les disques de la machine virtuelle offrent des performances bien meilleures que si elles se trouvent dans des régions distinctes.</span><span class="sxs-lookup"><span data-stu-id="32a46-196">VMs located in the same region as the Storage account that stores the disks for the VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="32a46-197">Autres paramètres de configuration de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="32a46-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="32a46-198">Lorsque vous créez une machine virtuelle Azure, vous devez en configurer certains paramètres.</span><span class="sxs-lookup"><span data-stu-id="32a46-198">When creating an Azure VM, you will be asked to configure certain VM settings.</span></span> <span data-ttu-id="32a46-199">N’oubliez pas : certains paramètres sont fixes pour la durée de vie de la machine virtuelle, tandis que d’autres peuvent être modifiés ou ajoutés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="32a46-199">Remember, few settings are fixed for the lifetime of the VM, while you can modify or add others later.</span></span> <span data-ttu-id="32a46-200">Passez en revue les paramètres de configuration des machines virtuelles Azure et assurez-vous qu’ils sont correctement configurés pour répondre aux besoins de votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="32a46-200">Review these Azure VM configuration settings and make sure that these are configured appropriately to match your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="32a46-201">Optimisation</span><span class="sxs-lookup"><span data-stu-id="32a46-201">Optimization</span></span>
<span data-ttu-id="32a46-202">[Azure Premium Storage : conception sous le signe de la haute performance](storage-premium-storage-performance.md) fournit des instructions pour la création d’applications hautes performances avec Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="32a46-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="32a46-203">Vous pouvez suivre les instructions parallèlement aux bonnes pratiques de performances applicables aux technologies utilisées par votre application.</span><span class="sxs-lookup"><span data-stu-id="32a46-203">You can follow the guidelines combined with performance best practices applicable to technologies used by your application.</span></span>

## <span data-ttu-id="32a46-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Préparation et copie de disques durs virtuels (VHD) vers le stockage Premium</span><span class="sxs-lookup"><span data-stu-id="32a46-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) to Premium Storage</span></span>
<span data-ttu-id="32a46-205">La section suivante fournit des instructions pour la préparation des disques durs virtuels à partir de votre machine virtuelle et la copie des disques durs virtuels vers le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="32a46-205">The following section provides guidelines for preparing VHDs from your VM and copying VHDs to Azure Storage.</span></span>

* [<span data-ttu-id="32a46-206">Scénario 1 : « Migration des machines virtuelles Azure existantes vers Azure Premium Storage. »</span><span class="sxs-lookup"><span data-stu-id="32a46-206">Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="32a46-207">Scénario 2 : « Migration de machines virtuelles depuis d’autres plateformes vers Azure Premium Storage ».</span><span class="sxs-lookup"><span data-stu-id="32a46-207">Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="32a46-208">Composants requis</span><span class="sxs-lookup"><span data-stu-id="32a46-208">Prerequisites</span></span>
<span data-ttu-id="32a46-209">Pour préparer les disques durs virtuels pour la migration, vous devez :</span><span class="sxs-lookup"><span data-stu-id="32a46-209">To prepare the VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="32a46-210">Un abonnement Azure, un compte de stockage et un conteneur dans ce compte de stockage sur lequel vous pouvez copier votre disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="32a46-210">An Azure subscription, a storage account, and a container in that storage account to which you can copy your VHD.</span></span> <span data-ttu-id="32a46-211">Notez que le compte de stockage de destination peut être un compte de stockage Standard ou Premium selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="32a46-211">Note that the destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="32a46-212">Un outil pour généraliser le disque dur virtuel si vous envisagez de créer plusieurs instances de machine virtuelle à partir de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="32a46-212">A tool to generalize the VHD if you plan to create multiple VM instances from it.</span></span> <span data-ttu-id="32a46-213">Par exemple, sysprep pour Windows ou virt-sysprep pour Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="32a46-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="32a46-214">Un outil pour télécharger le fichier de disque dur virtuel sur le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="32a46-214">A tool to upload the VHD file to the Storage account.</span></span> <span data-ttu-id="32a46-215">Consultez [Transfert de données avec l’utilitaire de ligne de commande AzCopy](storage-use-azcopy.md) ou utilisez [l’explorateur Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="32a46-215">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="32a46-216">Ce guide décrit la copie de votre disque dur virtuel à l’aide de l’outil AzCopy.</span><span class="sxs-lookup"><span data-stu-id="32a46-216">This guide describes copying your VHD using the AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="32a46-217">Si vous choisissez l’option de copie asynchrone pour AzCopy, pour des performances optimales, copiez votre disque dur virtuel en exécutant l’un de ces outils à partir d’une machine virtuelle Azure se trouvant dans la même région que le compte de stockage de destination.</span><span class="sxs-lookup"><span data-stu-id="32a46-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in the same region as the destination storage account.</span></span> <span data-ttu-id="32a46-218">Si vous copiez un disque dur virtuel à partir d’une machine virtuelle Azure se trouvant dans une autre région, les performances risquent d’être ralenties.</span><span class="sxs-lookup"><span data-stu-id="32a46-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="32a46-219">Pour copier une grande quantité de données avec une bande passante limitée, envisagez d’utiliser le [service Azure Import/Export pour transférer les données vers Blob Storage](../storage-import-export-service.md). Cela permet de transférer les données par expédition des disques durs à un centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="32a46-219">For copying a large amount of data over limited bandwidth, consider [using the Azure Import/Export service to transfer data to Blob Storage](../storage-import-export-service.md); this allows you to transfer your data by shipping hard disk drives to an Azure datacenter.</span></span> <span data-ttu-id="32a46-220">Vous pouvez utiliser le service Azure Import/Export pour copier les données vers un compte de stockage Standard uniquement.</span><span class="sxs-lookup"><span data-stu-id="32a46-220">You can use the Azure Import/Export service to copy data to a standard storage account only.</span></span> <span data-ttu-id="32a46-221">Une fois les données dans votre compte de stockage Standard, utilisez [l’API copie d’objet blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) ou AzCopy pour transférer les données vers votre compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="32a46-221">Once the data is in your standard storage account, you can use either the [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy to transfer the data to your premium storage account.</span></span>
>
> <span data-ttu-id="32a46-222">Notez que Microsoft Azure prend uniquement en charge les fichiers de disque dur virtuel de taille fixe.</span><span class="sxs-lookup"><span data-stu-id="32a46-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="32a46-223">Les fichiers VHDX ou les disques durs virtuels dynamiques ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="32a46-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="32a46-224">Si vous avez un disque dur virtuel dynamique, vous pouvez le convertir à taille fixe à l’aide de l’applet de commande [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) .</span><span class="sxs-lookup"><span data-stu-id="32a46-224">If you have a dynamic VHD, you can convert it to fixed size using the [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="32a46-225"><a name="scenario1"></a>Scénario 1 : « Migration des machines virtuelles Azure existantes vers Azure Premium Storage. »</span><span class="sxs-lookup"><span data-stu-id="32a46-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs to Azure Premium Storage."</span></span>
<span data-ttu-id="32a46-226">Si vous faites migrer des machines virtuelles Azure existantes, arrêtez la machine virtuelle, préparez les disques durs virtuels pour le type de disque dur virtuel souhaité, puis copiez le disque dur virtuel avec AzCopy ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32a46-226">If you are migrating existing Azure VMs, stop the VM, prepare VHDs per the type of VHD you want, and then copy the VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="32a46-227">La machine virtuelle doit être complètement arrêtée pour migrer un état propre.</span><span class="sxs-lookup"><span data-stu-id="32a46-227">The VM needs to be completely down to migrate a clean state.</span></span> <span data-ttu-id="32a46-228">L’interruption de service se poursuivra jusqu’à la fin de la migration.</span><span class="sxs-lookup"><span data-stu-id="32a46-228">There will be a downtime until the migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="32a46-229">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="32a46-229">Step 1.</span></span> <span data-ttu-id="32a46-230">Préparer des disques durs virtuels pour la migration</span><span class="sxs-lookup"><span data-stu-id="32a46-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="32a46-231">Si vous faites migrer des machines virtuelles Azure existantes vers le stockage Premium, votre disque dur Virtuel peut être :</span><span class="sxs-lookup"><span data-stu-id="32a46-231">If you are migrating existing Azure VMs to Premium Storage, your VHD may be:</span></span>

* <span data-ttu-id="32a46-232">Une image du système d'exploitation généralisée</span><span class="sxs-lookup"><span data-stu-id="32a46-232">A generalized operating system image</span></span>
* <span data-ttu-id="32a46-233">Un disque de système d’exploitation unique</span><span class="sxs-lookup"><span data-stu-id="32a46-233">A unique operating system disk</span></span>
* <span data-ttu-id="32a46-234">Un disque de données</span><span class="sxs-lookup"><span data-stu-id="32a46-234">A data disk</span></span>

<span data-ttu-id="32a46-235">Nous vous présentons ci-dessous 3 scénarios pour la préparation de vos disques durs virtuels.</span><span class="sxs-lookup"><span data-stu-id="32a46-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-to-create-multiple-vm-instances"></a><span data-ttu-id="32a46-236">Utilisez un disque dur virtuel de système d’exploitation généralisé pour créer plusieurs instances de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="32a46-236">Use a generalized Operating System VHD to create multiple VM instances</span></span>
<span data-ttu-id="32a46-237">Si vous téléchargez un disque dur virtuel qui permet de créer plusieurs instances de machine virtuelle Azure génériques, vous devez tout d’abord généraliser un disque dur virtuel à l’aide d’un utilitaire sysprep.</span><span class="sxs-lookup"><span data-stu-id="32a46-237">If you are uploading a VHD that will be used to create multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="32a46-238">Cette procédure s’applique à un disque dur virtuel local ou dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="32a46-238">This applies to a VHD that is on-premises or in the cloud.</span></span> <span data-ttu-id="32a46-239">Sysprep supprime des informations spécifiques sur une machine à partir du disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="32a46-239">Sysprep removes any machine-specific information from the VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32a46-240">Réalisez un instantané ou une sauvegarde de votre machine virtuelle avant la généralisation.</span><span class="sxs-lookup"><span data-stu-id="32a46-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="32a46-241">L’exécution de sysprep arrêtera et désallouera l’instance de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="32a46-241">Running sysprep will stop and deallocate the VM instance.</span></span> <span data-ttu-id="32a46-242">Suivez les étapes ci-dessous pour exécuter sysprep sur un disque dur virtuel de système d’exploitation Windows.</span><span class="sxs-lookup"><span data-stu-id="32a46-242">Follow steps below to sysprep a Windows OS VHD.</span></span> <span data-ttu-id="32a46-243">Notez que vous devez arrêter la machine virtuelle pour pouvoir exécuter la commande Sysprep.</span><span class="sxs-lookup"><span data-stu-id="32a46-243">Note that running the Sysprep command will require you to shut down the virtual machine.</span></span> <span data-ttu-id="32a46-244">Pour plus d’informations sur Sysprep, consultez [Présentation de Sysprep](http://technet.microsoft.com/library/hh825209.aspx) ou le [Manuel de référence technique Sysprep](http://technet.microsoft.com/library/cc766049.aspx).</span><span class="sxs-lookup"><span data-stu-id="32a46-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="32a46-245">Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="32a46-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="32a46-246">Entrez la commande suivante pour ouvrir Sypsrep :</span><span class="sxs-lookup"><span data-stu-id="32a46-246">Enter the following command to open Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="32a46-247">Dans l’outil de préparation du système, choisissez Entrer en mode OOBE (Out-of-Box Experience), activez la case à cocher Généraliser, sélectionnez **Arrêter**, puis cliquez sur **OK**, comme illustré dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="32a46-247">In the System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select the Generalize check box, select **Shutdown**, and then click **OK**, as shown in the image below.</span></span> <span data-ttu-id="32a46-248">Le système d’exploitation sera généralisé et le système arrêté par sysprep.</span><span class="sxs-lookup"><span data-stu-id="32a46-248">Sysprep will generalize the operating system and shut down the system.</span></span>

    ![][1]

<span data-ttu-id="32a46-249">Pour une machine virtuelle Ubuntu, utilisez virt-sysprep pour obtenir le même résultat.</span><span class="sxs-lookup"><span data-stu-id="32a46-249">For an Ubuntu VM, use virt-sysprep to achieve the same.</span></span> <span data-ttu-id="32a46-250">Pour plus d’informations, consultez la page [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) .</span><span class="sxs-lookup"><span data-stu-id="32a46-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="32a46-251">Consultez également les informations relatives à certains des [logiciels de configuration du serveur Linux](http://www.cyberciti.biz/tips/server-provisioning-software.html) open source pour d’autres systèmes d’exploitation Linux.</span><span class="sxs-lookup"><span data-stu-id="32a46-251">See also some of the open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-to-create-a-single-vm-instance"></a><span data-ttu-id="32a46-252">Utilisation d’un disque dur virtuel de système d’exploitation unique pour créer une seule instance de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="32a46-252">Use a unique Operating System VHD to create a single VM instance</span></span>
<span data-ttu-id="32a46-253">Si une application exécutée sur la machine virtuelle requiert les données spécifiques de la machine, ne généralisez pas le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="32a46-253">If you have an application running on the VM which requires the machine specific data, do not generalize the VHD.</span></span> <span data-ttu-id="32a46-254">Un disque dur virtuel non généralisé peut servir à créer une instance de machine virtuelle Azure unique.</span><span class="sxs-lookup"><span data-stu-id="32a46-254">A non-generalized VHD can be used to create a unique Azure VM instance.</span></span> <span data-ttu-id="32a46-255">Par exemple, si vous avez un contrôleur de domaine sur votre disque dur virtuel, l’exécution de sysprep le rend inefficace comme contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="32a46-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="32a46-256">Passez en revue les applications s’exécutant sur votre machine virtuelle et l’impact de sysprep s’exécutant sur ces dernières avant la généralisation du disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="32a46-256">Review the applications running on your VM and the impact of running sysprep on them before generalizing the VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="32a46-257">Enregistrement du disque dur virtuel de données</span><span class="sxs-lookup"><span data-stu-id="32a46-257">Register data disk VHD</span></span>
<span data-ttu-id="32a46-258">Si vous avez des disques de données dans Azure à migrer, vous devez vous assurer que les machines virtuelles qui utilisent ces disques de données sont arrêtées.</span><span class="sxs-lookup"><span data-stu-id="32a46-258">If you have data disks in Azure to be migrated, you must make sure the VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="32a46-259">Suivez les étapes décrites ci-dessous pour copier un disque dur virtuel vers Azure Premium Storage et l’enregistrer en tant que disque de données configuré.</span><span class="sxs-lookup"><span data-stu-id="32a46-259">Follow the steps described below to copy VHD to Azure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="32a46-260">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="32a46-260">Step 2.</span></span> <span data-ttu-id="32a46-261">Création de la destination de votre disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="32a46-261">Create the destination for your VHD</span></span>
<span data-ttu-id="32a46-262">Créez un compte de stockage pour gérer vos disques durs virtuels.</span><span class="sxs-lookup"><span data-stu-id="32a46-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="32a46-263">Prenez en compte les points suivants lors de la planification de l’emplacement où stocker vos disques durs virtuels :</span><span class="sxs-lookup"><span data-stu-id="32a46-263">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="32a46-264">Le compte de stockage Premium cible.</span><span class="sxs-lookup"><span data-stu-id="32a46-264">The target Premium storage account.</span></span>
* <span data-ttu-id="32a46-265">L’emplacement du compte de stockage doit être identique dans les machines virtuelles Azure compatibles Premium Storage que vous allez créer lors de l’étape finale.</span><span class="sxs-lookup"><span data-stu-id="32a46-265">The storage account location must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="32a46-266">Vous pouvez copier vers un nouveau compte de stockage, ou envisager d’utiliser le même compte de stockage selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="32a46-266">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="32a46-267">Copiez et enregistrez la clé de compte de stockage du compte de stockage de destination pour l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="32a46-267">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="32a46-268">Pour les disques de données, vous pouvez choisir d’en conserver certains dans un compte de stockage Standard (par exemple, les disques qui ont un stockage de refroidissement), mais nous vous conseillons fortement de déplacer toutes vos données de charge de travail de production pour utiliser le compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="32a46-268">For data disks, you can choose to keep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <span data-ttu-id="32a46-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Étape 3.</span><span class="sxs-lookup"><span data-stu-id="32a46-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="32a46-270">Copie du disque dur virtuel avec AzCopy ou PowerShell</span><span class="sxs-lookup"><span data-stu-id="32a46-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="32a46-271">Vous devez rechercher le chemin d’accès de votre conteneur et la clé du compte de stockage pour traiter une de ces deux options.</span><span class="sxs-lookup"><span data-stu-id="32a46-271">You will need to find your container path and storage account key to process either of these two options.</span></span> <span data-ttu-id="32a46-272">Vous trouverez le chemin d’accès au conteneur et le compte de stockage dans le **Portail Azure** > **Stockage**.</span><span class="sxs-lookup"><span data-stu-id="32a46-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="32a46-273">L’URL du conteneur sera au format « https://moncompte.blob.core.windows.net/monconteneur/ ».</span><span class="sxs-lookup"><span data-stu-id="32a46-273">The container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="32a46-274">Option 1 : Copie d’un disque dur virtuel avec AzCopy (copie asynchrone)</span><span class="sxs-lookup"><span data-stu-id="32a46-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="32a46-275">À l’aide d’AzCopy, vous pouvez facilement télécharger le disque dur virtuel sur Internet.</span><span class="sxs-lookup"><span data-stu-id="32a46-275">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="32a46-276">Selon la taille des disques durs virtuels, cela peut prendre du temps.</span><span class="sxs-lookup"><span data-stu-id="32a46-276">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="32a46-277">N’oubliez pas de vérifier les limites d’entrées/sorties de compte de stockage lors de l’utilisation de cette option.</span><span class="sxs-lookup"><span data-stu-id="32a46-277">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="32a46-278">Pour plus d’informations, consultez [Objectifs de performance et d’évolutivité d’Azure Storage](storage-scalability-targets.md) .</span><span class="sxs-lookup"><span data-stu-id="32a46-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="32a46-279">Téléchargez et installez AzCopy à partir d’ici : [version la plus récente d’AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="32a46-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="32a46-280">Ouvrez Azure PowerShell et accédez au dossier où AzCopy est installé.</span><span class="sxs-lookup"><span data-stu-id="32a46-280">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="32a46-281">Utilisez la commande suivante pour copier le fichier de disque dur virtuel à partir de « Source » vers « Destination ».</span><span class="sxs-lookup"><span data-stu-id="32a46-281">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="32a46-282">Exemple :</span><span class="sxs-lookup"><span data-stu-id="32a46-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="32a46-283">Les paramètres utilisés dans la commande AzCopy sont décrits ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="32a46-283">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="32a46-284">**/Source: *&lt;&gt;source :*** emplacement du dossier ou URL du conteneur de stockage qui contient le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="32a46-284">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="32a46-285">**/SourceKey : *&lt;source-account-key&gt; :*** clé de compte de stockage du compte de stockage source.</span><span class="sxs-lookup"><span data-stu-id="32a46-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="32a46-286">**/Dest : *&lt;destination&gt; :*** URL du conteneur de stockage où copier le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="32a46-286">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="32a46-287">**/DestKey : *&lt;dest-account-key&gt; :*** clé de compte de stockage du compte de stockage de destination.</span><span class="sxs-lookup"><span data-stu-id="32a46-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="32a46-288">**/Pattern : *&lt;file-name&gt; :*** spécifie le nom du fichier du disque dur virtuel à copier.</span><span class="sxs-lookup"><span data-stu-id="32a46-288">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="32a46-289">Pour plus d’informations sur l’utilisation d’AzCopy, consultez [Transfert de données avec l’utilitaire de ligne de commande AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="32a46-289">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="32a46-290">Option 2 : Copie d’un disque dur virtuel avec PowerShell (copie synchronisée)</span><span class="sxs-lookup"><span data-stu-id="32a46-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="32a46-291">Vous pouvez également copier le fichier de disque dur virtuel à l’aide de l’applet de commande Start-AzureStorageBlobCopy.</span><span class="sxs-lookup"><span data-stu-id="32a46-291">You can also copy the VHD file using the PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="32a46-292">Utilisez la commande suivante sur Azure PowerShell pour copier le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="32a46-292">Use the following command on Azure PowerShell to copy VHD.</span></span> <span data-ttu-id="32a46-293">Remplacez les valeurs entre <> par les valeurs correspondantes de votre compte de stockage source et de destination.</span><span class="sxs-lookup"><span data-stu-id="32a46-293">Replace the values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="32a46-294">Pour utiliser cette commande, vous devez disposer d’un conteneur appelé vhds (disques durs virtuels) dans votre compte de stockage de destination.</span><span class="sxs-lookup"><span data-stu-id="32a46-294">To use this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="32a46-295">Si le conteneur n’existe pas, créez-le avant d’exécuter la commande.</span><span class="sxs-lookup"><span data-stu-id="32a46-295">If the container doesn't exist, create one before running the command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="32a46-296">Exemple :</span><span class="sxs-lookup"><span data-stu-id="32a46-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="32a46-297"><a name="scenario2"></a>Scénario 2 : « Migration de machines virtuelles depuis d’autres plateformes vers Azure Premium Storage ».</span><span class="sxs-lookup"><span data-stu-id="32a46-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms to Azure Premium Storage."</span></span>
<span data-ttu-id="32a46-298">Si vous migrez un disque dur virtuel d’un stockage cloud non Azure vers Azure, vous devez d’abord exporter le disque dur virtuel vers un répertoire local.</span><span class="sxs-lookup"><span data-stu-id="32a46-298">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="32a46-299">Ayez à disposition le chemin d’accès source complet du répertoire local sur lequel le disque dur virtuel est stocké, et utilisez AzCopy pour le télécharger vers le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="32a46-299">Have the complete source path of the local directory where VHD is stored handy, and then using AzCopy to upload it to Azure Storage.</span></span>

#### <a name="step-1-export-vhd-to-a-local-directory"></a><span data-ttu-id="32a46-300">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="32a46-300">Step 1.</span></span> <span data-ttu-id="32a46-301">Exportation d’un disque dur virtuel vers un répertoire local</span><span class="sxs-lookup"><span data-stu-id="32a46-301">Export VHD to a local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="32a46-302">Copie d’un disque dur virtuel depuis AWS</span><span class="sxs-lookup"><span data-stu-id="32a46-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="32a46-303">Si vous utilisez AWS, exportez l’instance EC2 vers un disque dur virtuel dans un compartiment S3 Amazon.</span><span class="sxs-lookup"><span data-stu-id="32a46-303">If you are using AWS, export the EC2 instance to a VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="32a46-304">Suivez les étapes décrites dans la section Exportation des instances Amazon EC2 de la documentation Amazon pour installer l’outil d’interface de ligne de commande (CLI) Amazon EC2 et exécutez la commande create-instance-export-task pour exporter l’instance EC2 vers un fichier de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="32a46-304">Follow the steps described in the Amazon documentation for Exporting Amazon EC2 Instances to install the Amazon EC2 command-line interface (CLI) tool and run the create-instance-export-task command to export the EC2 instance to a VHD file.</span></span> <span data-ttu-id="32a46-305">Veillez à utiliser **VHD** pour la variable DISK&#95;IMAGE&#95;FORMAT lors de l’exécution de la commande **create-instance-export-task**.</span><span class="sxs-lookup"><span data-stu-id="32a46-305">Be sure to use **VHD** for the DISK&#95;IMAGE&#95;FORMAT variable when running the **create-instance-export-task** command.</span></span> <span data-ttu-id="32a46-306">Le fichier de disque dur virtuel exporté est enregistré dans le compartiment Amazon S3 que vous désignez au cours de ce processus.</span><span class="sxs-lookup"><span data-stu-id="32a46-306">The exported VHD file is saved in the Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="32a46-307">Téléchargez le fichier de disque dur virtuel depuis le compartiment S3.</span><span class="sxs-lookup"><span data-stu-id="32a46-307">Download the VHD file from the S3 bucket.</span></span> <span data-ttu-id="32a46-308">Sélectionnez le fichier de disque dur virtuel, puis **Actions** > **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="32a46-308">Select the VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="32a46-309">Copie d’un disque dur virtuel à partir d’autres cloud hors Azure</span><span class="sxs-lookup"><span data-stu-id="32a46-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="32a46-310">Si vous migrez un disque dur virtuel d’un stockage cloud non Azure vers Azure, vous devez d’abord exporter le disque dur virtuel vers un répertoire local.</span><span class="sxs-lookup"><span data-stu-id="32a46-310">If you are migrating VHD from non-Azure Cloud Storage to Azure, you must first export the VHD to a local directory.</span></span> <span data-ttu-id="32a46-311">Copiez le chemin source complet du répertoire local où le disque dur virtuel est stocké.</span><span class="sxs-lookup"><span data-stu-id="32a46-311">Copy the complete source path of the local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="32a46-312">Copie d’un disque dur virtuel en local</span><span class="sxs-lookup"><span data-stu-id="32a46-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="32a46-313">Si vous migrez un disque dur virtuel à partir d’un environnement local, vous avez besoin du chemin source complet où le disque dur virtuel est stocké.</span><span class="sxs-lookup"><span data-stu-id="32a46-313">If you are migrating VHD from an on-premises environment, you will need the complete source path where VHD is stored.</span></span> <span data-ttu-id="32a46-314">Le chemin d’accès source peut être un partage de fichiers ou un emplacement de serveur.</span><span class="sxs-lookup"><span data-stu-id="32a46-314">The source path could be a server location or file share.</span></span>

#### <a name="step-2-create-the-destination-for-your-vhd"></a><span data-ttu-id="32a46-315">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="32a46-315">Step 2.</span></span> <span data-ttu-id="32a46-316">Création de la destination de votre disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="32a46-316">Create the destination for your VHD</span></span>
<span data-ttu-id="32a46-317">Créez un compte de stockage pour gérer vos disques durs virtuels.</span><span class="sxs-lookup"><span data-stu-id="32a46-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="32a46-318">Prenez en compte les points suivants lors de la planification de l’emplacement où stocker vos disques durs virtuels :</span><span class="sxs-lookup"><span data-stu-id="32a46-318">Consider the following points when planning where to store your VHDs:</span></span>

* <span data-ttu-id="32a46-319">Le compte de stockage cible peut être Standard ou Premium selon les besoins de votre application.</span><span class="sxs-lookup"><span data-stu-id="32a46-319">The target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="32a46-320">La région du compte de stockage doit être identique dans les machines virtuelles Azure de série DS que vous allez créer lors de l’étape finale.</span><span class="sxs-lookup"><span data-stu-id="32a46-320">The storage account region must be same as Premium Storage capable Azure VMs you will create in the final stage.</span></span> <span data-ttu-id="32a46-321">Vous pouvez copier vers un nouveau compte de stockage, ou envisager d’utiliser le même compte de stockage selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="32a46-321">You could copy to a new storage account, or plan to use the same storage account based on your needs.</span></span>
* <span data-ttu-id="32a46-322">Copiez et enregistrez la clé de compte de stockage du compte de stockage de destination pour l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="32a46-322">Copy and save the storage account key of the destination storage account for the next stage.</span></span>

<span data-ttu-id="32a46-323">Nous vous recommandons fortement de déplacer toutes les données de charge de production pour utiliser le stockage premium.</span><span class="sxs-lookup"><span data-stu-id="32a46-323">We strongly recommend you moving all data for production workload to use premium storage.</span></span>

#### <a name="step-3-upload-the-vhd-to-azure-storage"></a><span data-ttu-id="32a46-324">Étape 3.</span><span class="sxs-lookup"><span data-stu-id="32a46-324">Step 3.</span></span> <span data-ttu-id="32a46-325">Téléchargement du disque dur virtuel vers le stockage Azure</span><span class="sxs-lookup"><span data-stu-id="32a46-325">Upload the VHD to Azure Storage</span></span>
<span data-ttu-id="32a46-326">Maintenant que vous avez votre disque dur virtuel dans le répertoire local, vous pouvez utiliser AzCopy ou AzurePowerShell pour télécharger le fichier .vhd vers le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="32a46-326">Now that you have your VHD in the local directory, you can use AzCopy or AzurePowerShell to upload the .vhd file to Azure Storage.</span></span> <span data-ttu-id="32a46-327">Les deux options sont fournies ici :</span><span class="sxs-lookup"><span data-stu-id="32a46-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-to-upload-the-vhd-file"></a><span data-ttu-id="32a46-328">Option 1 : Utilisation d’Add-AzureVhd d’Azure PowerShell pour télécharger le fichier .vhd</span><span class="sxs-lookup"><span data-stu-id="32a46-328">Option 1: Using Azure PowerShell Add-AzureVhd to upload the .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="32a46-329">Un exemple <Uri>peut être ***« https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd »***.</span><span class="sxs-lookup"><span data-stu-id="32a46-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="32a46-330">Un exemple <FileInfo>peut être ***« C:\path\to\upload.vhd »***.</span><span class="sxs-lookup"><span data-stu-id="32a46-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-to-upload-the-vhd-file"></a><span data-ttu-id="32a46-331">Option 2 : Utilisation d’AzCopy pour télécharger le fichier .vhd</span><span class="sxs-lookup"><span data-stu-id="32a46-331">Option 2: Using AzCopy to upload the .vhd file</span></span>
<span data-ttu-id="32a46-332">À l’aide d’AzCopy, vous pouvez facilement télécharger le disque dur virtuel sur Internet.</span><span class="sxs-lookup"><span data-stu-id="32a46-332">Using AzCopy, you can easily upload the VHD over the Internet.</span></span> <span data-ttu-id="32a46-333">Selon la taille des disques durs virtuels, cela peut prendre du temps.</span><span class="sxs-lookup"><span data-stu-id="32a46-333">Depending on the size of the VHDs, this may take time.</span></span> <span data-ttu-id="32a46-334">N’oubliez pas de vérifier les limites d’entrées/sorties de compte de stockage lors de l’utilisation de cette option.</span><span class="sxs-lookup"><span data-stu-id="32a46-334">Remember to check the storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="32a46-335">Pour plus d’informations, consultez [Objectifs de performance et d’évolutivité d’Azure Storage](storage-scalability-targets.md) .</span><span class="sxs-lookup"><span data-stu-id="32a46-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="32a46-336">Téléchargez et installez AzCopy à partir d’ici : [version la plus récente d’AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="32a46-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="32a46-337">Ouvrez Azure PowerShell et accédez au dossier où AzCopy est installé.</span><span class="sxs-lookup"><span data-stu-id="32a46-337">Open Azure PowerShell and go to the folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="32a46-338">Utilisez la commande suivante pour copier le fichier de disque dur virtuel à partir de « Source » vers « Destination ».</span><span class="sxs-lookup"><span data-stu-id="32a46-338">Use the following command to copy the VHD file from "Source" to "Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="32a46-339">Exemple :</span><span class="sxs-lookup"><span data-stu-id="32a46-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="32a46-340">Les paramètres utilisés dans la commande AzCopy sont décrits ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="32a46-340">Here are descriptions of the parameters used in the AzCopy command:</span></span>

   * <span data-ttu-id="32a46-341">**/Source: *&lt;&gt;source :*** emplacement du dossier ou URL du conteneur de stockage qui contient le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="32a46-341">**/Source: *&lt;source&gt;:*** Location of the folder or storage container URL that contains the VHD.</span></span>
   * <span data-ttu-id="32a46-342">**/SourceKey : *&lt;source-account-key&gt; :*** clé de compte de stockage du compte de stockage source.</span><span class="sxs-lookup"><span data-stu-id="32a46-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of the source storage account.</span></span>
   * <span data-ttu-id="32a46-343">**/Dest : *&lt;destination&gt; :*** URL du conteneur de stockage où copier le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="32a46-343">**/Dest: *&lt;destination&gt;:*** Storage container URL to copy the VHD to.</span></span>
   * <span data-ttu-id="32a46-344">**/DestKey : *&lt;dest-account-key&gt; :*** clé de compte de stockage du compte de stockage de destination.</span><span class="sxs-lookup"><span data-stu-id="32a46-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of the destination storage account.</span></span>
   * <span data-ttu-id="32a46-345">**/BlobType: page :** spécifie si la destination est un objet blob de pages.</span><span class="sxs-lookup"><span data-stu-id="32a46-345">**/BlobType: page:** Specifies that the destination is a page blob.</span></span>
   * <span data-ttu-id="32a46-346">**/Pattern : *&lt;file-name&gt; :*** spécifie le nom du fichier du disque dur virtuel à copier.</span><span class="sxs-lookup"><span data-stu-id="32a46-346">**/Pattern: *&lt;file-name&gt;:*** Specify the file name of the VHD to copy.</span></span>

<span data-ttu-id="32a46-347">Pour plus d’informations sur l’utilisation d’AzCopy, consultez [Transfert de données avec l’utilitaire de ligne de commande AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="32a46-347">For details on using AzCopy tool, see [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="32a46-348">Autres options de téléchargement d’un disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="32a46-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="32a46-349">Vous pouvez également télécharger un disque dur virtuel sur votre compte de stockage en utilisant l’un des moyens suivants :</span><span class="sxs-lookup"><span data-stu-id="32a46-349">You can also upload a VHD to your storage account using one of the following means:</span></span>

* [<span data-ttu-id="32a46-350">API de copie d’un objet blob de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="32a46-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="32a46-351">Téléchargement d’objets blob dans Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="32a46-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="32a46-352">Référence sur l’API REST du service Import/Export Storage</span><span class="sxs-lookup"><span data-stu-id="32a46-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="32a46-353">Nous recommandons l’utilisation de du service d’importation/exportation si l’estimation du temps de téléchargement est de plus de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="32a46-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="32a46-354">Vous pouvez utiliser [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) pour estimer le temps à partir de la taille des données et de l’unité de transfert.</span><span class="sxs-lookup"><span data-stu-id="32a46-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="32a46-355">Le service Import/Export permet de copier sur un compte de stockage Standard.</span><span class="sxs-lookup"><span data-stu-id="32a46-355">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="32a46-356">Vous devez effectuer une copie d’un compte de stockage Standard vers un compte de stockage Premium à l’aide d’un outil tel qu’AzCopy.</span><span class="sxs-lookup"><span data-stu-id="32a46-356">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="32a46-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Créer des machines virtuelles Azure à l’aide du stockage Premium</span><span class="sxs-lookup"><span data-stu-id="32a46-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="32a46-358">Une fois le disque dur virtuel téléchargé ou copié vers le compte de stockage souhaité, suivez les instructions de cette section pour inscrire le disque dur virtuel en tant qu’image de système d’exploitation ou disque de système d’exploitation en fonction de votre scénario et créez ensuite une instance de machine virtuelle à partir de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="32a46-358">After the VHD is uploaded or copied to the desired storage account, follow the instructions in this section to register the VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="32a46-359">Le disque dur virtuel de disque de données peut être joint à la machine virtuelle qui a été créée.</span><span class="sxs-lookup"><span data-stu-id="32a46-359">The data disk VHD can be attached to the VM once it is created.</span></span>
<span data-ttu-id="32a46-360">Un exemple de script de migration est fourni à la fin de cette section.</span><span class="sxs-lookup"><span data-stu-id="32a46-360">A sample migration script is provided at the end of this section.</span></span> <span data-ttu-id="32a46-361">Ce script simple ne correspond pas à tous les scénarios.</span><span class="sxs-lookup"><span data-stu-id="32a46-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="32a46-362">Vous devrez peut-être le mettre à jour pour qu’il corresponde à votre scénario spécifique.</span><span class="sxs-lookup"><span data-stu-id="32a46-362">You may need to update the script to match with your specific scenario.</span></span> <span data-ttu-id="32a46-363">Pour voir si ce script s’applique à votre scénario, consultez la section [Un exemple de script de migration](#a-sample-migration-script) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="32a46-363">To see if this script applies to your scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="32a46-364">Liste de contrôle</span><span class="sxs-lookup"><span data-stu-id="32a46-364">Checklist</span></span>
1. <span data-ttu-id="32a46-365">Patientez jusqu'à ce que la copie de tous disques durs virtuels soit terminée.</span><span class="sxs-lookup"><span data-stu-id="32a46-365">Wait until all the VHD disks copying is complete.</span></span>
2. <span data-ttu-id="32a46-366">Vérifiez que Premium Storage est disponible dans la région vers laquelle vous effectuez la migration.</span><span class="sxs-lookup"><span data-stu-id="32a46-366">Make sure Premium Storage is available in the region you are migrating to.</span></span>
3. <span data-ttu-id="32a46-367">Choisissez la nouvelle série de machines virtuelles que vous allez utiliser.</span><span class="sxs-lookup"><span data-stu-id="32a46-367">Decide the new VM series you will be using.</span></span> <span data-ttu-id="32a46-368">La compatibilité avec Premium Storage est indispensable et la taille dépend de la disponibilité dans la région et de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="32a46-368">It should be a Premium Storage capable, and the size should be depending on the availability in the region and based on your needs.</span></span>
4. <span data-ttu-id="32a46-369">Choisissez la taille exacte de machine virtuelle que vous allez utiliser.</span><span class="sxs-lookup"><span data-stu-id="32a46-369">Decide the exact VM size you will use.</span></span> <span data-ttu-id="32a46-370">La taille de machine virtuelle doit être suffisante pour prendre en charge le nombre de disques de données dont vous disposez.</span><span class="sxs-lookup"><span data-stu-id="32a46-370">VM size needs to be large enough to support the number of data disks you have.</span></span> <span data-ttu-id="32a46-371">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="32a46-371">E.g.</span></span> <span data-ttu-id="32a46-372">Si vous disposez de 4 disques de données, la machine virtuelle doit disposer d’au moins 2 cœurs.</span><span class="sxs-lookup"><span data-stu-id="32a46-372">if you have 4 data disks, the VM must have 2 or more cores.</span></span> <span data-ttu-id="32a46-373">Prenez également en considération les besoins en puissance, mémoire et bande passante réseau.</span><span class="sxs-lookup"><span data-stu-id="32a46-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="32a46-374">Créez un compte Premium Storage dans la région cible.</span><span class="sxs-lookup"><span data-stu-id="32a46-374">Create a Premium Storage account in the target region.</span></span> <span data-ttu-id="32a46-375">C’est le compte que vous utiliserez pour la nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="32a46-375">This is the account you will use for the new VM.</span></span>
6. <span data-ttu-id="32a46-376">Gardez à portée de main les informations détaillées sur les machines virtuelles, notamment la liste des disques et des blobs de disques durs virtuels correspondants.</span><span class="sxs-lookup"><span data-stu-id="32a46-376">Have the current VM details handy, including the list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="32a46-377">Préparez votre application pour les interruptions de service.</span><span class="sxs-lookup"><span data-stu-id="32a46-377">Prepare your application for downtime.</span></span> <span data-ttu-id="32a46-378">Pour effectuer une migration sans erreur, vous devez arrêter tous les processus en cours d’exécution dans le système actuel.</span><span class="sxs-lookup"><span data-stu-id="32a46-378">To do a clean migration, you have to stop all the processing in the current system.</span></span> <span data-ttu-id="32a46-379">Ce n’est qu’à cette condition que le système présentera un état cohérent, permettant sa migration vers la nouvelle plateforme.</span><span class="sxs-lookup"><span data-stu-id="32a46-379">Only then you can get it to consistent state which you can migrate to the new platform.</span></span> <span data-ttu-id="32a46-380">La durée de l’interruption de service dépend de la quantité de données dans les disques à migrer.</span><span class="sxs-lookup"><span data-stu-id="32a46-380">Downtime duration will depend on the amount of data in the disks to migrate.</span></span>

> [!NOTE]
> <span data-ttu-id="32a46-381">Si vous créez une machine virtuelle Azure Resource Manager à partir d’un disque dur virtuel spécialisé, reportez-vous à [ce modèle](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) pour le déploiement d’une machine virtuelle Resource Manager à l’aide du disque existant.</span><span class="sxs-lookup"><span data-stu-id="32a46-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer to [this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="32a46-382">Enregistrez votre disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="32a46-382">Register your VHD</span></span>
<span data-ttu-id="32a46-383">Pour créer une machine virtuelle à partir du disque dur virtuel de système d’exploitation ou joindre un disque de données à une nouvelle machine virtuelle, vous devez tout d’abord les inscrire.</span><span class="sxs-lookup"><span data-stu-id="32a46-383">To create a VM from OS VHD or to attach a data disk to a new VM, you must first register them.</span></span> <span data-ttu-id="32a46-384">Suivez les étapes ci-dessous en fonction de votre scénario de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="32a46-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="32a46-385">Disque dur virtuel de système d’exploitation généralisé pour créer plusieurs instances de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="32a46-385">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="32a46-386">Une fois le disque dur virtuel d’image du système d’exploitation généralisé téléchargé vers le compte de stockage, inscrivez-le comme une **Image de machine virtuelle Azure** afin de pouvoir créer une ou plusieurs instances de machine virtuelle à partir de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="32a46-386">After generalized OS image VHD is uploaded to the storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="32a46-387">Utilisez les applets de commande PowerShell suivantes pour inscrire votre disque dur virtuel comme image de système d’exploitation de la machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="32a46-387">Use the following PowerShell cmdlets to register your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="32a46-388">Fournissez l’URL de conteneur complet où le disque dur virtuel a été copié.</span><span class="sxs-lookup"><span data-stu-id="32a46-388">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="32a46-389">Copiez et enregistrez le nom de cette nouvelle image de machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="32a46-389">Copy and save the name of this new Azure VM Image.</span></span> <span data-ttu-id="32a46-390">Dans l’exemple ci-dessus, il s’agit de *OSImageName*.</span><span class="sxs-lookup"><span data-stu-id="32a46-390">In the example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="32a46-391">Disque dur virtuel de système d’exploitation unique pour créer une seule instance de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="32a46-391">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="32a46-392">Une fois le disque dur virtuel de système d’exploitation unique téléchargé vers le compte de stockage, inscrivez-le comme **disque de système d’exploitation Azure** afin de pouvoir créer une instance de machine virtuelle à partir de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="32a46-392">After the unique OS VHD is uploaded to the storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="32a46-393">Utilisez les applets de commande PowerShell suivantes pour inscrire votre disque dur virtuel comme disque de système d’exploitation Azure.</span><span class="sxs-lookup"><span data-stu-id="32a46-393">Use these PowerShell cmdlets to register your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="32a46-394">Fournissez l’URL de conteneur complet où le disque dur virtuel a été copié.</span><span class="sxs-lookup"><span data-stu-id="32a46-394">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="32a46-395">Copiez et enregistrez le nom de ce nouveau disque de système d’exploitation Azure.</span><span class="sxs-lookup"><span data-stu-id="32a46-395">Copy and save the name of this new Azure OS Disk.</span></span> <span data-ttu-id="32a46-396">Dans l’exemple ci-dessus, il s’agit de *OSDisk*.</span><span class="sxs-lookup"><span data-stu-id="32a46-396">In the example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-to-be-attached-to-new-azure-vm-instances"></a><span data-ttu-id="32a46-397">Disque dur virtuel de disque de données à joindre aux nouvelles instances de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="32a46-397">Data disk VHD to be attached to new Azure VM instance(s)</span></span>
<span data-ttu-id="32a46-398">Une fois le disque dur virtuel de disque de données téléchargé vers le compte de stockage, inscrivez-le comme disque de données Azure afin qu’il puisse être joint à votre nouvelle instance de machine virtuelle Azure de série DS, DSv2 ou GS.</span><span class="sxs-lookup"><span data-stu-id="32a46-398">After the data disk VHD is uploaded to storage account, register it as an Azure Data Disk so that it can be attached to your new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="32a46-399">Utilisez les applets de commande PowerShell suivantes pour inscrire votre disque dur virtuel comme disque de données Azure.</span><span class="sxs-lookup"><span data-stu-id="32a46-399">Use these PowerShell cmdlets to register your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="32a46-400">Fournissez l’URL de conteneur complet où le disque dur virtuel a été copié.</span><span class="sxs-lookup"><span data-stu-id="32a46-400">Provide the complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="32a46-401">Copiez et enregistrez le nom de ce nouveau disque de données Azure.</span><span class="sxs-lookup"><span data-stu-id="32a46-401">Copy and save the name of this new Azure Data Disk.</span></span> <span data-ttu-id="32a46-402">Dans l’exemple ci-dessus, il s’agit de *DataDisk*.</span><span class="sxs-lookup"><span data-stu-id="32a46-402">In the example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="32a46-403">Création d’un compte compatible Premium Storage</span><span class="sxs-lookup"><span data-stu-id="32a46-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="32a46-404">Une fois l’image du système d’exploitation ou le disque du système d’exploitation inscrit, créez une nouvelle machine virtuelle série DS, DSv2 ou GS.</span><span class="sxs-lookup"><span data-stu-id="32a46-404">Once the OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="32a46-405">Vous utiliserez l’image du système d’exploitation ou le nom de disque de système d’exploitation que vous avez inscrit.</span><span class="sxs-lookup"><span data-stu-id="32a46-405">You will be using the operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="32a46-406">Sélectionnez le type de machine virtuelle à partir du niveau de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="32a46-406">Select the VM type from the Premium Storage tier.</span></span> <span data-ttu-id="32a46-407">Dans l’exemple ci-dessous, nous utilisons la taille de machine virtuelle *Standard_DS2*.</span><span class="sxs-lookup"><span data-stu-id="32a46-407">In example below, we are using the *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="32a46-408">Mettez à jour la taille du disque pour vous assurer qu’il correspond à votre capacité, à l’exigence de performance et aux tailles de disque Azure disponibles.</span><span class="sxs-lookup"><span data-stu-id="32a46-408">Update the disk size to make sure it matches your capacity and performance requirements and the available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="32a46-409">Suivez les applets de commande PowerShell étape par étape ci-dessous pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="32a46-409">Follow the step by step PowerShell cmdlets below to create the new VM.</span></span> <span data-ttu-id="32a46-410">Tout d’abord, définissez les paramètres communs :</span><span class="sxs-lookup"><span data-stu-id="32a46-410">First, set the common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="32a46-411">Commencez par créer un service cloud dans lequel vous hébergerez vos nouvelles machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="32a46-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="32a46-412">Ensuite, selon votre scénario, créez l’instance de machine virtuelle Azure à partir de l’image de système d’exploitation ou du disque de système d’exploitation que vous avez inscrit.</span><span class="sxs-lookup"><span data-stu-id="32a46-412">Next, depending on your scenario, create the Azure VM instance from either the OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-to-create-multiple-azure-vm-instances"></a><span data-ttu-id="32a46-413">Disque dur virtuel de système d’exploitation généralisé pour créer plusieurs instances de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="32a46-413">Generalized Operating System VHD to create multiple Azure VM instances</span></span>
<span data-ttu-id="32a46-414">Créez la ou les nouvelles instances de machine virtuelle Azure de série DS à l’aide de l’ **Image de système d’exploitation Azure** que vous avez inscrite.</span><span class="sxs-lookup"><span data-stu-id="32a46-414">Create the one or more new DS Series Azure VM instances using the **Azure OS Image** that you registered.</span></span> <span data-ttu-id="32a46-415">Spécifiez ce nom d’image de système d’exploitation dans la configuration de la machine virtuelle lors de la création de nouvelles machines virtuelles comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="32a46-415">Specify this OS Image name in the VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-to-create-a-single-azure-vm-instance"></a><span data-ttu-id="32a46-416">Disque dur virtuel de système d’exploitation unique pour créer une seule instance de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="32a46-416">Unique Operating System VHD to create a single Azure VM instance</span></span>
<span data-ttu-id="32a46-417">Créez une nouvelle instance de machine virtuelle Azure de série DS à l’aide du **disque de système d’exploitation Azure** que vous avez inscrit.</span><span class="sxs-lookup"><span data-stu-id="32a46-417">Create a new DS series Azure VM instance using the **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="32a46-418">Spécifiez ce nom de disque du système d’exploitation dans la configuration de la machine virtuelle lors de la création de la nouvelle machine virtuelle comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="32a46-418">Specify this OS Disk name in the VM configuration when creating the new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="32a46-419">Spécifiez d’autres informations de machine virtuelle Azure, comme un service cloud, une région, un compte de stockage, un groupe à haute disponibilité et une stratégie de mise en cache.</span><span class="sxs-lookup"><span data-stu-id="32a46-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="32a46-420">Notez que l’instance de machine virtuelle doit se trouver avec le système d’exploitation ou les disques de données associés ; le service cloud, la région et le compte de stockage sélectionnés doivent donc tous se trouver au même emplacement que les disques durs virtuels sous-jacents de ces disques.</span><span class="sxs-lookup"><span data-stu-id="32a46-420">Note that the VM instance must be co-located with associated operating system or data disks, so the selected cloud service, region and storage account must all be in the same location as the underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="32a46-421">Attacher un disque de données</span><span class="sxs-lookup"><span data-stu-id="32a46-421">Attach data disk</span></span>
<span data-ttu-id="32a46-422">Enfin, si vous avez inscrit les disques durs virtuels des disques de données, joignez-les à la nouvelle machine virtuelle Azure compatible Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="32a46-422">Lastly, if you have registered data disk VHDs, attach them to the new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="32a46-423">Utilisez l’applet de commande PowerShell suivante pour joindre un disque de données à la nouvelle machine virtuelle et spécifiez la stratégie de mise en cache.</span><span class="sxs-lookup"><span data-stu-id="32a46-423">Use following PowerShell cmdlet to attach data disk to the new VM and specify the caching policy.</span></span> <span data-ttu-id="32a46-424">Dans l’exemple ci-dessous, la stratégie de mise en cache est définie sur *Lecture seule*.</span><span class="sxs-lookup"><span data-stu-id="32a46-424">In example below the caching policy is set to *ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="32a46-425">Des étapes supplémentaires susceptibles de ne pas être exposées dans ce guide peuvent être nécessaires pour prendre en charge vos applications.</span><span class="sxs-lookup"><span data-stu-id="32a46-425">There may be additional steps necessary to support your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="32a46-426">Vérification et planification de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="32a46-426">Checking and plan backup</span></span>
<span data-ttu-id="32a46-427">Une fois la nouvelle machine virtuelle opérationnelle, accédez-y en utilisant les mêmes ID de connexion et mot de passe que sur la machine virtuelle d’origine et vérifiez que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="32a46-427">Once the new VM is up and running, access it using the same login id and password is as the original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="32a46-428">Tous les paramètres, y compris les volumes agrégés par bandes doivent être présents dans la nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="32a46-428">All the settings, including the striped volumes, would be present in the new VM.</span></span>

<span data-ttu-id="32a46-429">La dernière étape consiste à planifier la sauvegarde et la maintenance de la nouvelle machine virtuelle en fonction des besoins de l’application.</span><span class="sxs-lookup"><span data-stu-id="32a46-429">The last step is to plan backup and maintenance schedule for the new VM based on the application's needs.</span></span>

### <span data-ttu-id="32a46-430"><a name="a-sample-migration-script"></a>Un exemple de script de migration</span><span class="sxs-lookup"><span data-stu-id="32a46-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="32a46-431">Si vous avez plusieurs machines virtuelles à migrer, il peut s’avérer utile d’automatiser ces tâches via des scripts PowerShell.</span><span class="sxs-lookup"><span data-stu-id="32a46-431">If you have multiple VMs to migrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="32a46-432">Voici un exemple de script qui automatise la migration d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="32a46-432">Following is a sample script that automates the migration of a VM.</span></span> <span data-ttu-id="32a46-433">Notez que le script ci-dessous n’est qu’un exemple, reposant sur des hypothèses concernant la configuration des disques de la machine virtuelle actuelle.</span><span class="sxs-lookup"><span data-stu-id="32a46-433">Note that below script is only an example, and there are few assumptions made about the current VM disks.</span></span> <span data-ttu-id="32a46-434">Vous devrez peut-être le mettre à jour pour qu’il corresponde à votre scénario spécifique.</span><span class="sxs-lookup"><span data-stu-id="32a46-434">You may need to update the script to match with your specific scenario.</span></span>

<span data-ttu-id="32a46-435">Nous supposons que :</span><span class="sxs-lookup"><span data-stu-id="32a46-435">The assumptions are:</span></span>

* <span data-ttu-id="32a46-436">Vous créez des machines virtuelles Azure classiques.</span><span class="sxs-lookup"><span data-stu-id="32a46-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="32a46-437">Vos disques de système d’exploitation source et disques de données source sont sur le même compte de stockage et le même conteneur.</span><span class="sxs-lookup"><span data-stu-id="32a46-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="32a46-438">Si vos disques de système d’exploitation et disques de données ne sont pas au même emplacement, vous pouvez utiliser AzCopy ou Azure PowerShell pour copier les disques durs virtuels sur des conteneurs et comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="32a46-438">If your OS Disks and Data Disks are not in the same place, you can use AzCopy or Azure PowerShell to copy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="32a46-439">Reportez-vous à l’étape précédente : [Copie du disque dur virtuel avec AzCopy ou PowerShell](#copy-vhd-with-azcopy-or-powershell).</span><span class="sxs-lookup"><span data-stu-id="32a46-439">Refer to the previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="32a46-440">La modification de ce script pour répondre à votre scénario est une autre possibilité, mais nous recommandons l’utilisation d’AzCopy ou de PowerShell, car cela est plus facile et plus rapide.</span><span class="sxs-lookup"><span data-stu-id="32a46-440">Editing this script to meet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="32a46-441">Le script d’automatisation est fourni ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="32a46-441">The automation script is provided below.</span></span> <span data-ttu-id="32a46-442">Remplacez le texte par vos informations et mettez à jour le script pour correspondre à votre scénario spécifique.</span><span class="sxs-lookup"><span data-stu-id="32a46-442">Replace text with your information and update the script to match with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="32a46-443">L’utilisation du script existant ne conserve pas la configuration réseau de votre machine virtuelle source.</span><span class="sxs-lookup"><span data-stu-id="32a46-443">Using the existing script does not preserve the network configuration of your source VM.</span></span> <span data-ttu-id="32a46-444">Vous devrez reconfigurer les paramètres réseau sur vos machines virtuelles migrées.</span><span class="sxs-lookup"><span data-stu-id="32a46-444">You will need to re-config the networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE to show how to migrate a VM from a standard storage account to a premium storage account. You can customize it according to your specific requirements.

    .Description
    The script will copy the vhds (page blobs) of the source VM to the new storage account.
    And then it will create a new VM from these copied vhds based on the inputs that you specified for the new VM.
    You can modify the script to satisfy your specific requirement, but please be aware of the items specified
    in the Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. THE ENTIRE RISK OF USE, INABILITY TO USE, OR
    RESULTS FROM THE USE OF THIS CODE REMAINS WITH THE USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    To find more information about how to set up Azure PowerShell, refer to the following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # the cloud service name of the VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # The VM name to copy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # The destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # The destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # the destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # the destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # the location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not to copy the os disk, the default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently to report the copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # the name suffix to add to new created disks to avoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import the Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check the Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer to this article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ to connect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if the VM is shut down
    #  Stopping the VM is a required step so that the file system is consistent when you do the copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - The source VM doesn't exist in the current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping the VM is a required step so that the file system is consistent when you do the copy operation. Azure does not support live migration at this time. If you'd like to create a VM from a generalized image, sys-prep the Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish to stop $SourceVMName now? Input 'N' if you want to shut down the VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until the VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName to shut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting the sourve vm to a configuration file, you can restore the original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration to $vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy the vhds of the source vm
    #  You can choose to copy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly to be $false. The default is to copy only data disk vhds
    #  and the new VM will boot from the original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering the data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in the destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need to copy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting the source VM so that dest VM can boot
        # from the same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose to copy data disks only. Moving VM requires removing the original VM (the disks and backing vhd files will NOT be deleted) so that the new VM can boot from the same vhd. This is an irreversible action. Do you wish to proceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing the original VM (the vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill the OS disk is released by source VM. This may take up to several minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy the os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update the media link to point to the target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy to complete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  the new VM can be created from the copied disks or the original os disk.
    #  You can ddd your own logic here to satisfy your specific requirements of the vm.
    #######################################################################

    # Create a VM from the existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached the copied data disks to the new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of the source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want to add more custimization to the new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="32a46-445"><a name="optimization"></a>Optimisation</span><span class="sxs-lookup"><span data-stu-id="32a46-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="32a46-446">La configuration de votre machine virtuelle actuelle peut être personnalisée spécifiquement pour fonctionner correctement avec des disques Standard.</span><span class="sxs-lookup"><span data-stu-id="32a46-446">Your current VM configuration may be customized specifically to work well with Standard disks.</span></span> <span data-ttu-id="32a46-447">Par exemple, vous pouvez augmenter les performances en utilisant de nombreux disques dans un volume agrégé par bandes.</span><span class="sxs-lookup"><span data-stu-id="32a46-447">For instance, to increase the performance by using many disks in a striped volume.</span></span> <span data-ttu-id="32a46-448">Par exemple, au lieu d’utiliser 4 disques séparément sur Premium Storage, vous pourrez optimiser le coût en n’utilisant qu’un seul disque.</span><span class="sxs-lookup"><span data-stu-id="32a46-448">For example, instead of using 4 disks separately on Premium Storage, you may be able to optimize the cost by having a single disk.</span></span> <span data-ttu-id="32a46-449">Des optimisations comme celles-ci doivent être étudiées au cas par cas et requièrent l’exécution d’étapes personnalisées après la migration.</span><span class="sxs-lookup"><span data-stu-id="32a46-449">Optimizations like this need to be handled on a case by case basis and require custom steps after the migration.</span></span> <span data-ttu-id="32a46-450">Notez également que ce processus est susceptible de ne pas bien fonctionner pour les bases de données et les applications qui dépendent de la disposition du disque définie dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="32a46-450">Also, note that this process may not well work for databases and applications that depend on the disk layout defined in the setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="32a46-451">Préparation</span><span class="sxs-lookup"><span data-stu-id="32a46-451">Preparation</span></span>
1. <span data-ttu-id="32a46-452">Terminez la migration simple comme décrit dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="32a46-452">Complete the Simple Migration as described in the earlier section.</span></span> <span data-ttu-id="32a46-453">Les optimisations seront effectuées sur la nouvelle machine virtuelle après la migration.</span><span class="sxs-lookup"><span data-stu-id="32a46-453">Optimizations will be performed on the new VM after the migration.</span></span>
2. <span data-ttu-id="32a46-454">Définissez les tailles requises pour les nouveaux disques pour une configuration optimisée.</span><span class="sxs-lookup"><span data-stu-id="32a46-454">Define the new disk sizes needed for the optimized configuration.</span></span>
3. <span data-ttu-id="32a46-455">Déterminez les spécifications du mappage des volumes/disques actuels aux nouveaux disques.</span><span class="sxs-lookup"><span data-stu-id="32a46-455">Determine mapping of the current disks/volumes to the new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="32a46-456">Étapes d'exécution</span><span class="sxs-lookup"><span data-stu-id="32a46-456">Execution steps</span></span>
1. <span data-ttu-id="32a46-457">Créez les nouveaux disques avec les tailles appropriées sur la machine virtuelle Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="32a46-457">Create the new disks with the right sizes on the Premium Storage VM.</span></span>
2. <span data-ttu-id="32a46-458">Connectez-vous à la machine virtuelle et copiez les données du volume actuel vers le nouveau disque mappé à ce volume.</span><span class="sxs-lookup"><span data-stu-id="32a46-458">Login to the VM and copy the data from the current volume to the new disk that maps to that volume.</span></span> <span data-ttu-id="32a46-459">Utilisez cette même procédure pour tous les volumes actuels devant être mappés à un nouveau disque.</span><span class="sxs-lookup"><span data-stu-id="32a46-459">Do this for all the current volumes that need to map to a new disk.</span></span>
3. <span data-ttu-id="32a46-460">Ensuite, modifiez les paramètres d’application pour basculer vers les nouveaux disques et détachez les anciens volumes.</span><span class="sxs-lookup"><span data-stu-id="32a46-460">Next, change the application settings to switch to the new disks, and detach the old volumes.</span></span>

<span data-ttu-id="32a46-461">Pour optimiser l’application pour de meilleures performances de disque, reportez-vous à [Optimisation des performances applicatives](storage-premium-storage-performance.md#optimizing-application-performance).</span><span class="sxs-lookup"><span data-stu-id="32a46-461">For tuning the application for better disk performance, please refer to [Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="32a46-462">Migrations des applications</span><span class="sxs-lookup"><span data-stu-id="32a46-462">Application migrations</span></span>
<span data-ttu-id="32a46-463">Les bases de données et autres applications complexes peuvent nécessiter des étapes spéciales, telles que définies par le fournisseur de l’application pour la migration.</span><span class="sxs-lookup"><span data-stu-id="32a46-463">Databases and other complex applications may require special steps as defined by the application provider for the migration.</span></span> <span data-ttu-id="32a46-464">Reportez-vous à la documentation correspondante de l’application.</span><span class="sxs-lookup"><span data-stu-id="32a46-464">Please refer to respective application documentation.</span></span> <span data-ttu-id="32a46-465">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="32a46-465">E.g.</span></span> <span data-ttu-id="32a46-466">la migration des bases de données se fait généralement via des étapes de sauvegarde et de restauration.</span><span class="sxs-lookup"><span data-stu-id="32a46-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32a46-467">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="32a46-467">Next steps</span></span>
<span data-ttu-id="32a46-468">Consultez les ressources suivantes pour des scénarios spécifiques de migration des machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="32a46-468">See the following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="32a46-469">Migrer des machines virtuelles Azure entre les comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="32a46-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="32a46-470">Création et téléchargement d’un disque dur virtuel Windows Server dans Azure.</span><span class="sxs-lookup"><span data-stu-id="32a46-470">Create and upload a Windows Server VHD to Azure.</span></span>](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="32a46-471">Création et téléchargement d’un disque dur virtuel contenant le système d’exploitation Linux</span><span class="sxs-lookup"><span data-stu-id="32a46-471">Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System</span></span>](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="32a46-472">Migration de machines virtuelles à partir d’Amazon AWS vers Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="32a46-472">Migrating Virtual Machines from Amazon AWS to Microsoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="32a46-473">Consultez également les ressources suivantes pour en savoir plus sur Azure Storage et les machines virtuelles Azure :</span><span class="sxs-lookup"><span data-stu-id="32a46-473">Also, see the following resources to learn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="32a46-474">Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="32a46-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="32a46-475">Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="32a46-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="32a46-476">Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="32a46-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
