---
title: "machines virtuelles d’aaaMigrating tooAzure stockage Premium | Documents Microsoft"
description: "Migrez votre tooAzure de machines virtuelles existante stockage Premium. Premium Storage offre une prise en charge très performante et à faible latence des disques pour les charges de travail utilisant beaucoup d'E/S exécutées sur les machines virtuelles Azure."
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
ms.openlocfilehash: 19aaf2b7594e570f5a964baa00958a7a8eaae97b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a><span data-ttu-id="327e5-104">Migration tooAzure Premium stockage (disques non managées)</span><span class="sxs-lookup"><span data-stu-id="327e5-104">Migrating tooAzure Premium Storage (Unmanaged Disks)</span></span>

> [!NOTE]
> <span data-ttu-id="327e5-105">Cet article explique comment toomigrate une machine virtuelle qui utilise des disques standard non managé tooa ordinateur virtuel qui utilise non managée disques premium.</span><span class="sxs-lookup"><span data-stu-id="327e5-105">This article discusses how toomigrate a VM that uses unmanaged standard disks tooa VM that uses unmanaged premium disks.</span></span> <span data-ttu-id="327e5-106">Nous vous recommandons d’utiliser des disques de Azure géré pour les nouvelles machines virtuelles, et que vous convertissez vos disques toomanaged de disques non managé précédente.</span><span class="sxs-lookup"><span data-stu-id="327e5-106">We recommend that you use Azure Managed Disks for new VMs, and that you convert your previous unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="327e5-107">Géré les comptes de stockage sous-jacent de disques handle hello afin que vous n’êtes pas obligé.</span><span class="sxs-lookup"><span data-stu-id="327e5-107">Managed Disks handle hello underlying storage accounts so you don't have to.</span></span> <span data-ttu-id="327e5-108">Pour plus d’informations, consultez [Vue d’ensemble d’Azure Managed Disks](../../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="327e5-108">For more information, please see our [Managed Disks Overview](../../virtual-machines/windows/managed-disks-overview.md).</span></span>
>

<span data-ttu-id="327e5-109">Azure Premium Storage offre une prise en charge très performante et à faible latence des disques pour les machines virtuelles exécutant des charges de travail qui utilisent beaucoup d'E/S.</span><span class="sxs-lookup"><span data-stu-id="327e5-109">Azure Premium Storage delivers high-performance, low-latency disk support for virtual machines running I/O-intensive workloads.</span></span> <span data-ttu-id="327e5-110">Vous pouvez tirer parti de la vitesse de hello et les performances de ces disques en effectuant une migration tooAzure de disques de machine virtuelle de votre application stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="327e5-110">You can take advantage of hello speed and performance of these disks by migrating your application's VM disks tooAzure Premium Storage.</span></span>

<span data-ttu-id="327e5-111">Hello de ce guide vise toohelp nouveaux utilisateurs de stockage Azure Premium mieux préparer toomake une transition en douceur de leur tooPremium système actuel stockage.</span><span class="sxs-lookup"><span data-stu-id="327e5-111">hello purpose of this guide is toohelp new users of Azure Premium Storage better prepare toomake a smooth transition from their current system tooPremium Storage.</span></span> <span data-ttu-id="327e5-112">guide de Hello traite des trois composants clés de hello dans ce processus :</span><span class="sxs-lookup"><span data-stu-id="327e5-112">hello guide addresses three of hello key components in this process:</span></span>

* [<span data-ttu-id="327e5-113">Planifier la Migration de hello tooPremium stockage</span><span class="sxs-lookup"><span data-stu-id="327e5-113">Plan for hello Migration tooPremium Storage</span></span>](#plan-the-migration-to-premium-storage)
* [<span data-ttu-id="327e5-114">Préparer et copier les disques durs virtuels (VHD) tooPremium stockage</span><span class="sxs-lookup"><span data-stu-id="327e5-114">Prepare and Copy Virtual Hard Disks (VHDs) tooPremium Storage</span></span>](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [<span data-ttu-id="327e5-115">Création d’une machine virtuelle Azure utilisant Premium Storage</span><span class="sxs-lookup"><span data-stu-id="327e5-115">Create Azure Virtual Machine using Premium Storage</span></span>](#create-azure-virtual-machine-using-premium-storage)

<span data-ttu-id="327e5-116">Vous pouvez migrer des machines virtuelles à partir d’autres plateformes de tooAzure stockage Premium ou migrer des machines virtuelles Azure existantes à partir du stockage Standard tooPremium stockage.</span><span class="sxs-lookup"><span data-stu-id="327e5-116">You can either migrate VMs from other platforms tooAzure Premium Storage or migrate existing Azure VMs from Standard Storage tooPremium Storage.</span></span> <span data-ttu-id="327e5-117">Ce guide décrit les étapes pour les deux scénarios.</span><span class="sxs-lookup"><span data-stu-id="327e5-117">This guide covers steps for both two scenarios.</span></span> <span data-ttu-id="327e5-118">Suivez les étapes de hello spécifiés dans la section pertinentes de hello en fonction de votre scénario.</span><span class="sxs-lookup"><span data-stu-id="327e5-118">Follow hello steps specified in hello relevant section depending on your scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="327e5-119">Vous pouvez consulter un aperçu des fonctionnalités et de la tarification dans [Premium Storage : stockage hautes performances pour les charges de travail des machines virtuelles Azure](storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="327e5-119">You can find a feature overview and pricing of Premium Storage in Premium Storage: [High-Performance Storage for Azure Virtual Machine Workloads](storage-premium-storage.md).</span></span> <span data-ttu-id="327e5-120">Nous vous recommandons de migrer n’importe quel disque de machine virtuelle nécessitant une haute IOPS tooAzure stockage Premium pour optimiser les performances hello pour votre application.</span><span class="sxs-lookup"><span data-stu-id="327e5-120">We recommend migrating any virtual machine disk requiring high IOPS tooAzure Premium Storage for hello best performance for your application.</span></span> <span data-ttu-id="327e5-121">Si votre disque ne nécessite pas un nombre élevé d'IOPS, vous pouvez limiter les coûts en le conservant dans le stockage Standard qui stocke les données de disque de machine virtuelle sur des disques durs et non des disques SSD.</span><span class="sxs-lookup"><span data-stu-id="327e5-121">If your disk does not require high IOPS, you can limit costs by maintaining it in Standard Storage, which stores virtual machine disk data on Hard Disk Drives (HDDs) instead of SSDs.</span></span>
>

<span data-ttu-id="327e5-122">Fin du processus de migration hello dans son intégralité peut nécessiter des actions supplémentaires avant et après les étapes hello fournies dans ce guide.</span><span class="sxs-lookup"><span data-stu-id="327e5-122">Completing hello migration process in its entirety may require additional actions both before and after hello steps provided in this guide.</span></span> <span data-ttu-id="327e5-123">Configuration des réseaux virtuels ou des points de terminaison ou l’apport de modifications du code au sein de l’application hello elle-même et ce qui peut nécessiter un temps d’arrêt dans votre application sont des exemples.</span><span class="sxs-lookup"><span data-stu-id="327e5-123">Examples include configuring virtual networks or endpoints or making code changes within hello application itself which may require some downtime in your application.</span></span> <span data-ttu-id="327e5-124">Ces actions sont tooeach unique à l’application, et elles doivent être exécutées en même temps que les étapes de hello fournies dans cette tooPremium de transition complète guide toomake hello plus transparent possible du stockage.</span><span class="sxs-lookup"><span data-stu-id="327e5-124">These actions are unique tooeach application, and you should complete them along with hello steps provided in this guide toomake hello full transition tooPremium Storage as seamless as possible.</span></span>

## <span data-ttu-id="327e5-125"><a name="plan-the-migration-to-premium-storage"></a>Planifier la migration de hello tooPremium stockage</span><span class="sxs-lookup"><span data-stu-id="327e5-125"><a name="plan-the-migration-to-premium-storage"></a>Plan for hello migration tooPremium Storage</span></span>
<span data-ttu-id="327e5-126">Cette section permet de s’assurer que vous êtes prêt toofollow étapes de migration hello dans cet article et vous aide à toomake hello meilleure décision sur les types de machine virtuelle et le disque.</span><span class="sxs-lookup"><span data-stu-id="327e5-126">This section ensures that you are ready toofollow hello migration steps in this article, and helps you toomake hello best decision on VM and Disk types.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="327e5-127">Composants requis</span><span class="sxs-lookup"><span data-stu-id="327e5-127">Prerequisites</span></span>
* <span data-ttu-id="327e5-128">Vous aurez besoin d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="327e5-128">You will need an Azure subscription.</span></span> <span data-ttu-id="327e5-129">Si vous n’en avez pas, vous pouvez souscrire un abonnement pour un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/) d’un mois ou visiter [Tarification Azure](https://azure.microsoft.com/pricing/) pour plus d’options.</span><span class="sxs-lookup"><span data-stu-id="327e5-129">If you don't have one, you can create a one-month [free trial](https://azure.microsoft.com/pricing/free-trial/) subscription or visit [Azure Pricing](https://azure.microsoft.com/pricing/) for more options.</span></span>
* <span data-ttu-id="327e5-130">tooexecute applets de commande PowerShell, vous aurez besoin de module de Microsoft Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-130">tooexecute PowerShell cmdlets, you will need hello Microsoft Azure PowerShell module.</span></span> <span data-ttu-id="327e5-131">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) Pourquoi installer instructions d’installation et de point.</span><span class="sxs-lookup"><span data-stu-id="327e5-131">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello install point and installation instructions.</span></span>
* <span data-ttu-id="327e5-132">Lorsque vous planifiez des machines virtuelles Azure de toouse en cours d’exécution sur le stockage Premium, vous devez toouse hello machines virtuelles capables de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="327e5-132">When you plan toouse Azure VMs running on Premium Storage, you need toouse hello Premium Storage capable VMs.</span></span> <span data-ttu-id="327e5-133">Vous pouvez utiliser des disques de Stockage Standard et Premium avec les machines virtuelles compatibles avec Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="327e5-133">You can use both Standard and Premium Storage disks with Premium Storage capable VMs.</span></span> <span data-ttu-id="327e5-134">Les disques de stockage Premium sera disponibles avec plusieurs types de machine virtuelle Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="327e5-134">Premium storage disks will be available with more VM types in hello future.</span></span> <span data-ttu-id="327e5-135">Pour plus d’informations sur les tailles et les types de disque de machine virtuelle Azure disponibles, consultez [Tailles des machines virtuelles](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) et [Tailles des services cloud](../../cloud-services/cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="327e5-135">For more information on all available Azure VM disk types and sizes, see [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Sizes for Cloud Services](../../cloud-services/cloud-services-sizes-specs.md).</span></span>

### <a name="considerations"></a><span data-ttu-id="327e5-136">Considérations</span><span class="sxs-lookup"><span data-stu-id="327e5-136">Considerations</span></span>
<span data-ttu-id="327e5-137">Une machine virtuelle Azure prend en charge l’attachement de plusieurs disques de stockage Premium afin que vos applications peuvent avoir jusqu'à to too256 de stockage par la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="327e5-137">An Azure VM supports attaching several Premium Storage disks so that your applications can have up too256 TB of storage per VM.</span></span> <span data-ttu-id="327e5-138">Avec Premium Storage, vos applications peuvent atteindre jusqu'à 80 000 IOPS (opérations d'E/S par seconde) par machine virtuelle et un débit de disque de 2 000 Mo par seconde, avec une latence extrêmement faible pour les opérations de lecture.</span><span class="sxs-lookup"><span data-stu-id="327e5-138">With Premium Storage, your applications can achieve 80,000 IOPS (input/output operations per second) per VM and 2000 MB per second disk throughput per VM with extremely low latencies for read operations.</span></span> <span data-ttu-id="327e5-139">Vous disposez de diverses options de machines virtuelles et disques.</span><span class="sxs-lookup"><span data-stu-id="327e5-139">You have options in a variety of VMs and Disks.</span></span> <span data-ttu-id="327e5-140">Cette section est toohelp toofind une option qui convient le mieux à votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="327e5-140">This section is toohelp you toofind an option that best suits your workload.</span></span>

#### <a name="vm-sizes"></a><span data-ttu-id="327e5-141">Tailles de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="327e5-141">VM sizes</span></span>
<span data-ttu-id="327e5-142">spécifications de taille de machine virtuelle Azure Hello sont répertoriées dans [tailles des machines virtuelles](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="327e5-142">hello Azure VM size specifications are listed in [Sizes for virtual machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="327e5-143">Passez en revue les caractéristiques de performances hello d’ordinateurs virtuels qui fonctionnent avec un stockage Premium et choisissez hello plus approprié taille de machine virtuelle qui convient le mieux à votre charge de travail.</span><span class="sxs-lookup"><span data-stu-id="327e5-143">Review hello performance characteristics of virtual machines that work with Premium Storage and choose hello most appropriate VM size that best suits your workload.</span></span> <span data-ttu-id="327e5-144">Assurez-vous qu’il y suffisamment de bande passante disponible sur votre trafic de disque de machine virtuelle toodrive hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-144">Make sure that there is sufficient bandwidth available on your VM toodrive hello disk traffic.</span></span>

#### <a name="disk-sizes"></a><span data-ttu-id="327e5-145">Tailles du disque</span><span class="sxs-lookup"><span data-stu-id="327e5-145">Disk sizes</span></span>
<span data-ttu-id="327e5-146">Il existe cinq types de disque qui peuvent être utilisés avec votre machine virtuelle et chacun d’eux présentant des limites d’E/S par seconde et de débits spécifiques.</span><span class="sxs-lookup"><span data-stu-id="327e5-146">There are five types of disks that can be used with your VM and each has specific IOPs and throughput limits.</span></span> <span data-ttu-id="327e5-147">Prenez en compte ces limites lorsqu’en choisissant le type de disque hello pour votre machine virtuelle en fonction des besoins de hello de votre application en termes de capacité, les performances, l’évolutivité, et des pics.</span><span class="sxs-lookup"><span data-stu-id="327e5-147">Take into consideration these limits when choosing hello disk type for your VM based on hello needs of your application in terms of capacity, performance, scalability, and peak loads.</span></span>

| <span data-ttu-id="327e5-148">Type de disque Premium</span><span class="sxs-lookup"><span data-stu-id="327e5-148">Premium Disks Type</span></span>  | <span data-ttu-id="327e5-149">P10</span><span class="sxs-lookup"><span data-stu-id="327e5-149">P10</span></span>   | <span data-ttu-id="327e5-150">P20</span><span class="sxs-lookup"><span data-stu-id="327e5-150">P20</span></span>   | <span data-ttu-id="327e5-151">P30</span><span class="sxs-lookup"><span data-stu-id="327e5-151">P30</span></span>            | <span data-ttu-id="327e5-152">P40</span><span class="sxs-lookup"><span data-stu-id="327e5-152">P40</span></span>            | <span data-ttu-id="327e5-153">P50</span><span class="sxs-lookup"><span data-stu-id="327e5-153">P50</span></span>            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| <span data-ttu-id="327e5-154">Taille du disque</span><span class="sxs-lookup"><span data-stu-id="327e5-154">Disk size</span></span>           | <span data-ttu-id="327e5-155">128 Go</span><span class="sxs-lookup"><span data-stu-id="327e5-155">128 GB</span></span>| <span data-ttu-id="327e5-156">512 Go</span><span class="sxs-lookup"><span data-stu-id="327e5-156">512 GB</span></span>| <span data-ttu-id="327e5-157">1024 Go (1 To)</span><span class="sxs-lookup"><span data-stu-id="327e5-157">1024 GB (1 TB)</span></span> | <span data-ttu-id="327e5-158">2 048 Go (2 To)</span><span class="sxs-lookup"><span data-stu-id="327e5-158">2048 GB (2 TB)</span></span> | <span data-ttu-id="327e5-159">4 095 Go (4 To)</span><span class="sxs-lookup"><span data-stu-id="327e5-159">4095 GB (4 TB)</span></span> | 
| <span data-ttu-id="327e5-160">IOPS par disque</span><span class="sxs-lookup"><span data-stu-id="327e5-160">IOPS per disk</span></span>       | <span data-ttu-id="327e5-161">500</span><span class="sxs-lookup"><span data-stu-id="327e5-161">500</span></span>   | <span data-ttu-id="327e5-162">2 300</span><span class="sxs-lookup"><span data-stu-id="327e5-162">2300</span></span>  | <span data-ttu-id="327e5-163">5 000</span><span class="sxs-lookup"><span data-stu-id="327e5-163">5000</span></span>           | <span data-ttu-id="327e5-164">7500</span><span class="sxs-lookup"><span data-stu-id="327e5-164">7500</span></span>           | <span data-ttu-id="327e5-165">7500</span><span class="sxs-lookup"><span data-stu-id="327e5-165">7500</span></span>           | 
| <span data-ttu-id="327e5-166">Débit par disque</span><span class="sxs-lookup"><span data-stu-id="327e5-166">Throughput per disk</span></span> | <span data-ttu-id="327e5-167">100 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="327e5-167">100 MB per second</span></span> | <span data-ttu-id="327e5-168">150 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="327e5-168">150 MB per second</span></span> | <span data-ttu-id="327e5-169">200 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="327e5-169">200 MB per second</span></span> | <span data-ttu-id="327e5-170">250 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="327e5-170">250 MB per second</span></span> | <span data-ttu-id="327e5-171">250 Mo par seconde</span><span class="sxs-lookup"><span data-stu-id="327e5-171">250 MB per second</span></span> |

<span data-ttu-id="327e5-172">En fonction de votre charge de travail, déterminez si les disques de données supplémentaires sont nécessaires pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="327e5-172">Depending on your workload, determine if additional data disks are necessary for your VM.</span></span> <span data-ttu-id="327e5-173">Vous pouvez attacher plusieurs tooyour de disques de données persistantes machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="327e5-173">You can attach several persistent data disks tooyour VM.</span></span> <span data-ttu-id="327e5-174">Si nécessaire, vous pouvez répartir sur la capacité de hello disques tooincrease hello et les performances du volume de hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-174">If needed, you can stripe across hello disks tooincrease hello capacity and performance of hello volume.</span></span> <span data-ttu-id="327e5-175">(Découvrez ce qu’est l’entrelacement de disques [ici](storage-premium-storage-performance.md#disk-striping).) Si vous équilibrez les disques de données Stockage Premium à l’aide des [espaces de stockage][4], vous devez les configurer avec une colonne pour chaque disque utilisé.</span><span class="sxs-lookup"><span data-stu-id="327e5-175">(See what is Disk Striping [here](storage-premium-storage-performance.md#disk-striping).) If you stripe Premium Storage data disks using [Storage Spaces][4], you should configure it with one column for each disk that is used.</span></span> <span data-ttu-id="327e5-176">Dans le cas contraire, hello globalement les performances du volume de hello agrégés par bande peuvent être inférieure que prévu en raison de la distribution toouneven du trafic sur les disques hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-176">Otherwise, hello overall performance of hello striped volume may be lower than expected due toouneven distribution of traffic across hello disks.</span></span> <span data-ttu-id="327e5-177">Pour les machines virtuelles Linux, vous pouvez utiliser hello *mdadm* utilitaire tooachieve hello identiques.</span><span class="sxs-lookup"><span data-stu-id="327e5-177">For Linux VMs you can use hello *mdadm* utility tooachieve hello same.</span></span> <span data-ttu-id="327e5-178">Consultez l’article [Configuration d’un RAID logiciel sur Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="327e5-178">See article [Configure Software RAID on Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for details.</span></span>

#### <a name="storage-account-scalability-targets"></a><span data-ttu-id="327e5-179">Objectifs d’évolutivité de compte de stockage</span><span class="sxs-lookup"><span data-stu-id="327e5-179">Storage account scalability targets</span></span>
<span data-ttu-id="327e5-180">Comptes de stockage Premium ont hello suivant les objectifs d’évolutivité dans Ajout toohello [évolutivité du stockage Azure et les objectifs de performances](storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="327e5-180">Premium Storage accounts have hello following scalability targets in addition toohello [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="327e5-181">Si les exigences de votre application dépassent les objectifs d’évolutivité hello d’un compte de stockage unique, générez votre toouse application plusieurs comptes de stockage et partitionner vos données sur ces comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="327e5-181">If your application requirements exceed hello scalability targets of a single storage account, build your application toouse multiple storage accounts, and partition your data across those storage accounts.</span></span>

| <span data-ttu-id="327e5-182">Capacité totale des comptes</span><span class="sxs-lookup"><span data-stu-id="327e5-182">Total Account Capacity</span></span> | <span data-ttu-id="327e5-183">Bande passante totale pour un compte de stockage localement redondant</span><span class="sxs-lookup"><span data-stu-id="327e5-183">Total Bandwidth for a Locally Redundant Storage Account</span></span> |
|:--- |:--- |
| <span data-ttu-id="327e5-184">Capacité du disque : 35 To</span><span class="sxs-lookup"><span data-stu-id="327e5-184">Disk capacity: 35TB</span></span><br /><span data-ttu-id="327e5-185">Capacité d’instantané : 10 To</span><span class="sxs-lookup"><span data-stu-id="327e5-185">Snapshot capacity: 10 TB</span></span> |<span data-ttu-id="327e5-186">Les too50 les gigabits par seconde pour entrante + sortante</span><span class="sxs-lookup"><span data-stu-id="327e5-186">Up too50 gigabits per second for Inbound + Outbound</span></span> |

<span data-ttu-id="327e5-187">Pour hello plus d’informations sur les spécifications de stockage Premium, consultez [objectifs d’évolutivité et performances lors de l’utilisation du stockage Premium](storage-premium-storage.md#scalability-and-performance-targets).</span><span class="sxs-lookup"><span data-stu-id="327e5-187">For hello more information on Premium Storage specifications, check out [Scalability and Performance Targets when using Premium Storage](storage-premium-storage.md#scalability-and-performance-targets).</span></span>

#### <a name="disk-caching-policy"></a><span data-ttu-id="327e5-188">Stratégie de mise en cache du disque</span><span class="sxs-lookup"><span data-stu-id="327e5-188">Disk caching policy</span></span>
<span data-ttu-id="327e5-189">Par défaut, la mise en cache de stratégie est *en lecture seule* pour tous les hello disques de données Premium, et *en lecture-écriture* hello Premium système d’exploitation attaché toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="327e5-189">By default, disk caching policy is *Read-Only* for all hello Premium data disks, and *Read-Write* for hello Premium operating system disk attached toohello VM.</span></span> <span data-ttu-id="327e5-190">Ce paramètre de configuration est recommandé tooachieve hello des performances optimales IOs de votre application.</span><span class="sxs-lookup"><span data-stu-id="327e5-190">This configuration setting is recommended tooachieve hello optimal performance for your application's IOs.</span></span> <span data-ttu-id="327e5-191">Pour les disques de données en écriture seule ou avec d'importantes opérations d'écriture (par ex., les fichiers journaux de SQL Server), désactivez la mise en cache du disque pour de meilleures performances de l'application.</span><span class="sxs-lookup"><span data-stu-id="327e5-191">For write-heavy or write-only data disks (such as SQL Server log files), disable disk caching so that you can achieve better application performance.</span></span> <span data-ttu-id="327e5-192">paramètres de cache de Hello pour les disques de données existants peuvent être mis à jour à l’aide de [Azure Portal](https://portal.azure.com) ou hello *- HostCaching* paramètre Hello *Set-AzureDataDisk* applet de commande.</span><span class="sxs-lookup"><span data-stu-id="327e5-192">hello cache settings for existing data disks can be updated using [Azure Portal](https://portal.azure.com) or hello *-HostCaching* parameter of hello *Set-AzureDataDisk* cmdlet.</span></span>

#### <a name="location"></a><span data-ttu-id="327e5-193">Lieu</span><span class="sxs-lookup"><span data-stu-id="327e5-193">Location</span></span>
<span data-ttu-id="327e5-194">Choisissez un emplacement où le stockage Azure Premium est disponible.</span><span class="sxs-lookup"><span data-stu-id="327e5-194">Pick a location where Azure Premium Storage is available.</span></span> <span data-ttu-id="327e5-195">Pour obtenir des informations à jour sur les emplacements disponibles, consultez [Services Azure par région](https://azure.microsoft.com/regions/#services) .</span><span class="sxs-lookup"><span data-stu-id="327e5-195">See [Azure Services by Region](https://azure.microsoft.com/regions/#services) for up-to-date information on available locations.</span></span> <span data-ttu-id="327e5-196">Machines virtuelles situées dans hello même région de hello compte de stockage que les magasins hello disques pour hello VM donnera de meilleures performances que si elles figurent dans les régions séparées.</span><span class="sxs-lookup"><span data-stu-id="327e5-196">VMs located in hello same region as hello Storage account that stores hello disks for hello VM will give much better performance than if they are in separate regions.</span></span>

#### <a name="other-azure-vm-configuration-settings"></a><span data-ttu-id="327e5-197">Autres paramètres de configuration de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="327e5-197">Other Azure VM configuration settings</span></span>
<span data-ttu-id="327e5-198">Lorsque vous créez une machine virtuelle Azure, vous serez invité tooconfigure certains paramètres.</span><span class="sxs-lookup"><span data-stu-id="327e5-198">When creating an Azure VM, you will be asked tooconfigure certain VM settings.</span></span> <span data-ttu-id="327e5-199">N’oubliez pas, certains paramètres sont fixes pour la durée de vie hello Hello machine virtuelle, tandis que vous pouvez modifier ou ajouter d’autres plus tard.</span><span class="sxs-lookup"><span data-stu-id="327e5-199">Remember, few settings are fixed for hello lifetime of hello VM, while you can modify or add others later.</span></span> <span data-ttu-id="327e5-200">Passez en revue ces paramètres de configuration de machine virtuelle Azure et vous assurer qu’ils sont configurés correctement toomatch vos charges de travail.</span><span class="sxs-lookup"><span data-stu-id="327e5-200">Review these Azure VM configuration settings and make sure that these are configured appropriately toomatch your workload requirements.</span></span>

### <a name="optimization"></a><span data-ttu-id="327e5-201">Optimisation</span><span class="sxs-lookup"><span data-stu-id="327e5-201">Optimization</span></span>
<span data-ttu-id="327e5-202">[Azure Premium Storage : conception sous le signe de la haute performance](storage-premium-storage-performance.md) fournit des instructions pour la création d’applications hautes performances avec Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="327e5-202">[Azure Premium Storage: Design for High Performance](storage-premium-storage-performance.md) provides guidelines for building high-performance applications using Azure Premium Storage.</span></span> <span data-ttu-id="327e5-203">Vous pouvez suivre les instructions hello combinées avec des performances tootechnologies d’applicable meilleures de pratiques intégré utilisé par votre application.</span><span class="sxs-lookup"><span data-stu-id="327e5-203">You can follow hello guidelines combined with performance best practices applicable tootechnologies used by your application.</span></span>

## <span data-ttu-id="327e5-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Préparer et copier les disques durs virtuels (VHD) tooPremium stockage</span><span class="sxs-lookup"><span data-stu-id="327e5-204"><a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Prepare and copy virtual hard disks (VHDs) tooPremium Storage</span></span>
<span data-ttu-id="327e5-205">Hello suivant la section fournit des instructions pour la préparation des disques durs virtuels à partir de votre machine virtuelle et la copie des disques durs virtuels tooAzure stockage.</span><span class="sxs-lookup"><span data-stu-id="327e5-205">hello following section provides guidelines for preparing VHDs from your VM and copying VHDs tooAzure Storage.</span></span>

* [<span data-ttu-id="327e5-206">Scénario 1 : « je migre existant tooAzure de machines virtuelles Azure Premium Storage. »</span><span class="sxs-lookup"><span data-stu-id="327e5-206">Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>](#scenario1)
* [<span data-ttu-id="327e5-207">Scénario 2 : « je suis migration d’ordinateurs virtuels à partir d’autres plateformes de tooAzure stockage Premium. »</span><span class="sxs-lookup"><span data-stu-id="327e5-207">Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>](#scenario2)

### <a name="prerequisites"></a><span data-ttu-id="327e5-208">Composants requis</span><span class="sxs-lookup"><span data-stu-id="327e5-208">Prerequisites</span></span>
<span data-ttu-id="327e5-209">tooprepare hello disques durs virtuels pour la migration, vous devez :</span><span class="sxs-lookup"><span data-stu-id="327e5-209">tooprepare hello VHDs for migration, you'll need:</span></span>

* <span data-ttu-id="327e5-210">Un abonnement Azure, un compte de stockage et un conteneur de stockage du compte toowhich, vous pouvez copier votre disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="327e5-210">An Azure subscription, a storage account, and a container in that storage account toowhich you can copy your VHD.</span></span> <span data-ttu-id="327e5-211">Notez que le compte de stockage de destination hello peut être un compte Standard ou Premium Storage, selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="327e5-211">Note that hello destination storage account can be a Standard or Premium Storage account depending on your requirement.</span></span>
* <span data-ttu-id="327e5-212">Un Bonjour de toogeneralize outil disque dur virtuel si vous envisagez de toocreate plusieurs instances de machine virtuelle à partir de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="327e5-212">A tool toogeneralize hello VHD if you plan toocreate multiple VM instances from it.</span></span> <span data-ttu-id="327e5-213">Par exemple, sysprep pour Windows ou virt-sysprep pour Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="327e5-213">For example, sysprep for Windows or virt-sysprep for Ubuntu.</span></span>
* <span data-ttu-id="327e5-214">Un outil tooupload hello VHD fichier toohello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="327e5-214">A tool tooupload hello VHD file toohello Storage account.</span></span> <span data-ttu-id="327e5-215">Consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md) ou utilisez un [Explorateur de stockage Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span><span class="sxs-lookup"><span data-stu-id="327e5-215">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md) or use an [Azure storage explorer](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx).</span></span> <span data-ttu-id="327e5-216">Ce guide décrit la copie de votre disque dur virtuel à l’aide d’outil de AzCopy hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-216">This guide describes copying your VHD using hello AzCopy tool.</span></span>

> [!NOTE]
> <span data-ttu-id="327e5-217">Si vous choisissez l’option de copie synchrone avec AzCopy, pour des performances optimales, copiez votre disque dur virtuel en exécutant un de ces outils à partir d’une machine virtuelle Azure qui se trouve dans hello même région que le compte de stockage de destination hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-217">If you choose synchronous copy option with AzCopy, for optimal performance, copy your VHD by running one of these tools from an Azure VM that is in hello same region as hello destination storage account.</span></span> <span data-ttu-id="327e5-218">Si vous copiez un disque dur virtuel à partir d’une machine virtuelle Azure se trouvant dans une autre région, les performances risquent d’être ralenties.</span><span class="sxs-lookup"><span data-stu-id="327e5-218">If you are copying a VHD from an Azure VM in a different region, your performance may be slower.</span></span>
>
> <span data-ttu-id="327e5-219">Pour copier une grande quantité de données sur une bande passante limitée, envisagez de [à l’aide du service d’importation/exportation Azure hello données tootransfer tooBlob stockage](../storage-import-export-service.md); ainsi, vous tootransfer vos données en disque dur de livraison lecteurs tooan Azure Centre de données.</span><span class="sxs-lookup"><span data-stu-id="327e5-219">For copying a large amount of data over limited bandwidth, consider [using hello Azure Import/Export service tootransfer data tooBlob Storage](../storage-import-export-service.md); this allows you tootransfer your data by shipping hard disk drives tooan Azure datacenter.</span></span> <span data-ttu-id="327e5-220">Vous pouvez utiliser hello Azure Import/Export service toocopy données tooa compte de stockage standard uniquement.</span><span class="sxs-lookup"><span data-stu-id="327e5-220">You can use hello Azure Import/Export service toocopy data tooa standard storage account only.</span></span> <span data-ttu-id="327e5-221">Une fois les données de salutation dans votre compte de stockage standard, vous pouvez utiliser soit hello [API de copie d’objet Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) ou compte de stockage AzCopy tootransfer hello données tooyour premium.</span><span class="sxs-lookup"><span data-stu-id="327e5-221">Once hello data is in your standard storage account, you can use either hello [Copy Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) or AzCopy tootransfer hello data tooyour premium storage account.</span></span>
>
> <span data-ttu-id="327e5-222">Notez que Microsoft Azure prend uniquement en charge les fichiers de disque dur virtuel de taille fixe.</span><span class="sxs-lookup"><span data-stu-id="327e5-222">Note that Microsoft Azure only supports fixed size VHD files.</span></span> <span data-ttu-id="327e5-223">Les fichiers VHDX ou les disques durs virtuels dynamiques ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="327e5-223">VHDX files or dynamic VHDs are not supported.</span></span> <span data-ttu-id="327e5-224">Si vous avez un disque dur virtuel dynamique, vous pouvez le convertir taille toofixed à l’aide de hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="327e5-224">If you have a dynamic VHD, you can convert it toofixed size using hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.</span></span>
>
>

### <span data-ttu-id="327e5-225"><a name="scenario1"></a>Scénario 1 : « je migre existant tooAzure de machines virtuelles Azure Premium Storage. »</span><span class="sxs-lookup"><span data-stu-id="327e5-225"><a name="scenario1"></a>Scenario 1: "I am migrating existing Azure VMs tooAzure Premium Storage."</span></span>
<span data-ttu-id="327e5-226">Si vous migrez existant de machines virtuelles Azure, stop hello machine virtuelle, préparer les disques durs virtuels par type hello du disque dur virtuel que vous souhaitez et copiez hello VHD avec AzCopy ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="327e5-226">If you are migrating existing Azure VMs, stop hello VM, prepare VHDs per hello type of VHD you want, and then copy hello VHD with AzCopy or PowerShell.</span></span>

<span data-ttu-id="327e5-227">Hello machine virtuelle doit toobe complètement vers le bas toomigrate un état propre.</span><span class="sxs-lookup"><span data-stu-id="327e5-227">hello VM needs toobe completely down toomigrate a clean state.</span></span> <span data-ttu-id="327e5-228">Il y aura un temps d’arrêt jusqu'à la fin de la migration hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-228">There will be a downtime until hello migration completes.</span></span>

#### <a name="step-1-prepare-vhds-for-migration"></a><span data-ttu-id="327e5-229">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="327e5-229">Step 1.</span></span> <span data-ttu-id="327e5-230">Préparer des disques durs virtuels pour la migration</span><span class="sxs-lookup"><span data-stu-id="327e5-230">Prepare VHDs for migration</span></span>
<span data-ttu-id="327e5-231">Si vous migrez existant tooPremium de machines virtuelles Azure Storage, votre disque dur virtuel peut être :</span><span class="sxs-lookup"><span data-stu-id="327e5-231">If you are migrating existing Azure VMs tooPremium Storage, your VHD may be:</span></span>

* <span data-ttu-id="327e5-232">Une image du système d'exploitation généralisée</span><span class="sxs-lookup"><span data-stu-id="327e5-232">A generalized operating system image</span></span>
* <span data-ttu-id="327e5-233">Un disque de système d’exploitation unique</span><span class="sxs-lookup"><span data-stu-id="327e5-233">A unique operating system disk</span></span>
* <span data-ttu-id="327e5-234">Un disque de données</span><span class="sxs-lookup"><span data-stu-id="327e5-234">A data disk</span></span>

<span data-ttu-id="327e5-235">Nous vous présentons ci-dessous 3 scénarios pour la préparation de vos disques durs virtuels.</span><span class="sxs-lookup"><span data-stu-id="327e5-235">Below we walk through these 3 scenarios for preparing your VHD.</span></span>

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a><span data-ttu-id="327e5-236">Utiliser un toocreate de disque dur virtuel du système d’exploitation généralisé plusieurs instances de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="327e5-236">Use a generalized Operating System VHD toocreate multiple VM instances</span></span>
<span data-ttu-id="327e5-237">Si vous téléchargez un disque dur virtuel qui sera utilisé toocreate plusieurs instances de machine virtuelle Azure génériques, vous devez tout d’abord généraliser disque dur virtuel à l’aide d’un utilitaire sysprep.</span><span class="sxs-lookup"><span data-stu-id="327e5-237">If you are uploading a VHD that will be used toocreate multiple generic Azure VM instances, you must first generalize VHD using a sysprep utility.</span></span> <span data-ttu-id="327e5-238">Cela s’applique tooa disque dur virtuel qui est local ou dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-238">This applies tooa VHD that is on-premises or in hello cloud.</span></span> <span data-ttu-id="327e5-239">Sysprep supprime toutes les informations spécifiques à l’ordinateur de hello disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="327e5-239">Sysprep removes any machine-specific information from hello VHD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="327e5-240">Réalisez un instantané ou une sauvegarde de votre machine virtuelle avant la généralisation.</span><span class="sxs-lookup"><span data-stu-id="327e5-240">Take a snapshot or backup your VM before generalizing it.</span></span> <span data-ttu-id="327e5-241">Arrête et désallouer l’instance de machine virtuelle hello en cours d’exécution de sysprep.</span><span class="sxs-lookup"><span data-stu-id="327e5-241">Running sysprep will stop and deallocate hello VM instance.</span></span> <span data-ttu-id="327e5-242">Suivez les étapes ci-dessous toosysprep un disque dur virtuel du système d’exploitation Windows.</span><span class="sxs-lookup"><span data-stu-id="327e5-242">Follow steps below toosysprep a Windows OS VHD.</span></span> <span data-ttu-id="327e5-243">Notez qu’exécutant la commande Sysprep de hello nécessitera que vous tooshut la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-243">Note that running hello Sysprep command will require you tooshut down hello virtual machine.</span></span> <span data-ttu-id="327e5-244">Pour plus d’informations sur Sysprep, consultez [Présentation de Sysprep](http://technet.microsoft.com/library/hh825209.aspx) ou le [Manuel de référence technique Sysprep](http://technet.microsoft.com/library/cc766049.aspx).</span><span class="sxs-lookup"><span data-stu-id="327e5-244">For more information about Sysprep, see [Sysprep Overview](http://technet.microsoft.com/library/hh825209.aspx) or [Sysprep Technical Reference](http://technet.microsoft.com/library/cc766049.aspx).</span></span>
>
>

1. <span data-ttu-id="327e5-245">Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="327e5-245">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="327e5-246">Entrez hello suivant tooopen de commande Sysprep :</span><span class="sxs-lookup"><span data-stu-id="327e5-246">Enter hello following command tooopen Sysprep:</span></span>

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. <span data-ttu-id="327e5-247">Bonjour outil de préparation système, sélectionnez entrer le système Out-of-Box expérience OOBE (), sélectionnez hello Generalize case à cocher, sélectionnez **arrêt**, puis cliquez sur **OK**, comme illustré dans l’image hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="327e5-247">In hello System Preparation Tool, select Enter System Out-of-Box Experience (OOBE), select hello Generalize check box, select **Shutdown**, and then click **OK**, as shown in hello image below.</span></span> <span data-ttu-id="327e5-248">Sysprep est généraliser le système d’exploitation de hello et arrêter le système hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-248">Sysprep will generalize hello operating system and shut down hello system.</span></span>

    ![][1]

<span data-ttu-id="327e5-249">Pour une VM Ubuntu, utiliser sysprep de pointeurs tooachieve hello identiques.</span><span class="sxs-lookup"><span data-stu-id="327e5-249">For an Ubuntu VM, use virt-sysprep tooachieve hello same.</span></span> <span data-ttu-id="327e5-250">Pour plus d’informations, consultez la page [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) .</span><span class="sxs-lookup"><span data-stu-id="327e5-250">See [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) for more details.</span></span> <span data-ttu-id="327e5-251">Voir également certains d’ouvrir la source de hello [logiciel de configuration du serveur Linux](http://www.cyberciti.biz/tips/server-provisioning-software.html) pour d’autres systèmes d’exploitation Linux.</span><span class="sxs-lookup"><span data-stu-id="327e5-251">See also some of hello open source [Linux Server Provisioning software](http://www.cyberciti.biz/tips/server-provisioning-software.html) for other Linux operating systems.</span></span>

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a><span data-ttu-id="327e5-252">Utilisez un toocreate de disque dur virtuel du système d’exploitation unique une seule instance de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="327e5-252">Use a unique Operating System VHD toocreate a single VM instance</span></span>
<span data-ttu-id="327e5-253">Si vous avez une application en cours d’exécution sur hello machine virtuelle qui requiert des données spécifiques de l’ordinateur hello, ne généralisez pas hello disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="327e5-253">If you have an application running on hello VM which requires hello machine specific data, do not generalize hello VHD.</span></span> <span data-ttu-id="327e5-254">Un disque dur virtuel non généralisé peut être utilisé toocreate une instance unique de la machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="327e5-254">A non-generalized VHD can be used toocreate a unique Azure VM instance.</span></span> <span data-ttu-id="327e5-255">Par exemple, si vous avez un contrôleur de domaine sur votre disque dur virtuel, l’exécution de sysprep le rend inefficace comme contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="327e5-255">For example, if you have Domain Controller on your VHD, executing sysprep will make it ineffective as a Domain Controller.</span></span> <span data-ttu-id="327e5-256">Passez en revue les applications hello exécutant votre machine virtuelle et hello l’impact de l’exécution de sysprep sur ces derniers avant la généralisation hello disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="327e5-256">Review hello applications running on your VM and hello impact of running sysprep on them before generalizing hello VHD.</span></span>

##### <a name="register-data-disk-vhd"></a><span data-ttu-id="327e5-257">Enregistrement du disque dur virtuel de données</span><span class="sxs-lookup"><span data-stu-id="327e5-257">Register data disk VHD</span></span>
<span data-ttu-id="327e5-258">Si vous avez migré des disques de données dans Azure toobe, vous devez effectuer que machines virtuelles hello qui utilisent ces disques sont en cours d’arrêt des données.</span><span class="sxs-lookup"><span data-stu-id="327e5-258">If you have data disks in Azure toobe migrated, you must make sure hello VMs that use these data disks are shut down.</span></span>

<span data-ttu-id="327e5-259">Hello les étapes décrites ci-dessous tooAzure de disque dur virtuel toocopy stockage Premium et l’enregistrer comme un disque de données mis en service.</span><span class="sxs-lookup"><span data-stu-id="327e5-259">Follow hello steps described below toocopy VHD tooAzure Premium Storage and register it as a provisioned data disk.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="327e5-260">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="327e5-260">Step 2.</span></span> <span data-ttu-id="327e5-261">Créer destination hello pour votre disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="327e5-261">Create hello destination for your VHD</span></span>
<span data-ttu-id="327e5-262">Créez un compte de stockage pour gérer vos disques durs virtuels.</span><span class="sxs-lookup"><span data-stu-id="327e5-262">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="327e5-263">Prendre en compte les points suivants lors de la planification de l’emplacement de hello toostore vos disques durs virtuels :</span><span class="sxs-lookup"><span data-stu-id="327e5-263">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="327e5-264">cible de Hello compte de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="327e5-264">hello target Premium storage account.</span></span>
* <span data-ttu-id="327e5-265">emplacement du compte de stockage Hello doit être identique en tant que machines virtuelles Azure capable de stockage Premium vous allez créer dans la phase finale de hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-265">hello storage account location must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="327e5-266">Vous pouvez copier le nouveau compte de stockage tooa ou hello toouse de plan même compte de stockage selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="327e5-266">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="327e5-267">Copiez et enregistrez la clé de compte de stockage hello hello destination du compte de stockage pour l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-267">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="327e5-268">Pour les disques de données, vous pouvez choisir tookeep des disques de données dans un compte de stockage standard (par exemple, les disques qui ont refroidissement stockage), mais nous vous recommandons vivement déplacement de toutes les données pour le stockage de production la charge de travail toouse premium.</span><span class="sxs-lookup"><span data-stu-id="327e5-268">For data disks, you can choose tookeep some data disks in a standard storage account (for example, disks that have cooler storage), but we strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <span data-ttu-id="327e5-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Étape 3.</span><span class="sxs-lookup"><span data-stu-id="327e5-269"><a name="copy-vhd-with-azcopy-or-powershell"></a>Step 3.</span></span> <span data-ttu-id="327e5-270">Copie du disque dur virtuel avec AzCopy ou PowerShell</span><span class="sxs-lookup"><span data-stu-id="327e5-270">Copy VHD with AzCopy or PowerShell</span></span>
<span data-ttu-id="327e5-271">Vous devez toofind votre chemin d’accès du conteneur et le stockage tooprocess clé de compte de ces deux options.</span><span class="sxs-lookup"><span data-stu-id="327e5-271">You will need toofind your container path and storage account key tooprocess either of these two options.</span></span> <span data-ttu-id="327e5-272">Vous trouverez le chemin d’accès au conteneur et le compte de stockage dans le **Portail Azure** > **Stockage**.</span><span class="sxs-lookup"><span data-stu-id="327e5-272">Container path and storage account key can be found in **Azure Portal** > **Storage**.</span></span> <span data-ttu-id="327e5-273">URL du conteneur Hello seront comme « https://myaccount.blob.core.windows.net/mycontainer/ ».</span><span class="sxs-lookup"><span data-stu-id="327e5-273">hello container URL will be like "https://myaccount.blob.core.windows.net/mycontainer/".</span></span>

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a><span data-ttu-id="327e5-274">Option 1 : Copie d’un disque dur virtuel avec AzCopy (copie asynchrone)</span><span class="sxs-lookup"><span data-stu-id="327e5-274">Option 1: Copy a VHD with AzCopy (Asynchronous copy)</span></span>
<span data-ttu-id="327e5-275">À l’aide de AzCopy, vous pouvez charger facilement hello VHD sur hello Internet.</span><span class="sxs-lookup"><span data-stu-id="327e5-275">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="327e5-276">Selon la taille de hello Hello disques durs virtuels, cela peut prendre le temps.</span><span class="sxs-lookup"><span data-stu-id="327e5-276">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="327e5-277">N’oubliez pas les limites des entrées/sorties comptes de stockage toocheck hello lors de l’utilisation de cette option.</span><span class="sxs-lookup"><span data-stu-id="327e5-277">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="327e5-278">Pour plus d’informations, consultez [Objectifs de performance et d’évolutivité d’Azure Storage](storage-scalability-targets.md) .</span><span class="sxs-lookup"><span data-stu-id="327e5-278">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="327e5-279">Téléchargez et installez AzCopy à partir d’ici : [version la plus récente d’AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="327e5-279">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="327e5-280">Ouvrez Azure PowerShell et accédez toohello où AzCopy est installé.</span><span class="sxs-lookup"><span data-stu-id="327e5-280">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="327e5-281">Fichier de disque dur virtuel hello toocopy à partir de « Source » de la commande suivante de hello d’utilisation trop « Destination ».</span><span class="sxs-lookup"><span data-stu-id="327e5-281">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="327e5-282">Exemple :</span><span class="sxs-lookup"><span data-stu-id="327e5-282">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    <span data-ttu-id="327e5-283">Voici les descriptions des paramètres hello utilisés Bonjour AzCopy commande :</span><span class="sxs-lookup"><span data-stu-id="327e5-283">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="327e5-284">**/ Source :  *&lt;source&gt;:***  emplacement du dossier de hello ou URL de conteneur de stockage qui contient le disque dur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-284">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="327e5-285">**/ SourceKey :  *&lt;clé de compte source&gt;:***  clé de compte de stockage hello source du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="327e5-285">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="327e5-286">**/ Dest :  *&lt;destination&gt;:***  toocopy de URL de conteneur de stockage hello disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="327e5-286">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="327e5-287">**/ DestKey :  *&lt;clé de compte dest&gt;:***  clé de compte de stockage du compte de stockage de destination hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-287">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="327e5-288">**/ Modèle :  *&lt;nom de fichier&gt;:***  spécifier le nom fichier hello de toocopy de disque dur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-288">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="327e5-289">Pour plus d’informations sur l’utilisation de AzCopy outil, consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="327e5-289">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a><span data-ttu-id="327e5-290">Option 2 : Copie d’un disque dur virtuel avec PowerShell (copie synchronisée)</span><span class="sxs-lookup"><span data-stu-id="327e5-290">Option 2: Copy a VHD with PowerShell (Synchronized copy)</span></span>
<span data-ttu-id="327e5-291">Vous pouvez également copier le fichier de disque dur virtuel de hello à l’aide d’applet de commande PowerShell hello AzureStorageBlobCopy de début.</span><span class="sxs-lookup"><span data-stu-id="327e5-291">You can also copy hello VHD file using hello PowerShell cmdlet Start-AzureStorageBlobCopy.</span></span> <span data-ttu-id="327e5-292">Utilisez hello suivant de commande de Azure PowerShell toocopy disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="327e5-292">Use hello following command on Azure PowerShell toocopy VHD.</span></span> <span data-ttu-id="327e5-293">Remplacer les valeurs hello dans <> avec les valeurs correspondantes à partir de votre compte de stockage source et de destination.</span><span class="sxs-lookup"><span data-stu-id="327e5-293">Replace hello values in <> with corresponding values from your source and destination storage account.</span></span> <span data-ttu-id="327e5-294">toouse cette commande, vous devez disposer d’un conteneur appelé des disques durs virtuels dans votre compte de stockage de destination.</span><span class="sxs-lookup"><span data-stu-id="327e5-294">toouse this command, you must have a container called vhds in your destination storage account.</span></span> <span data-ttu-id="327e5-295">Si le conteneur de hello n’existe pas, créez-le avant d’exécuter la commande hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-295">If hello container doesn't exist, create one before running hello command.</span></span>

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

<span data-ttu-id="327e5-296">Exemple :</span><span class="sxs-lookup"><span data-stu-id="327e5-296">Example:</span></span>

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <span data-ttu-id="327e5-297"><a name="scenario2"></a>Scénario 2 : « je suis migration d’ordinateurs virtuels à partir d’autres plateformes de tooAzure stockage Premium. »</span><span class="sxs-lookup"><span data-stu-id="327e5-297"><a name="scenario2"></a>Scenario 2: "I am migrating VMs from other platforms tooAzure Premium Storage."</span></span>
<span data-ttu-id="327e5-298">Si vous effectuez une migration à partir d’Azure Cloud Storage tooAzure disque dur virtuel, vous devez d’abord exporter répertoire local de tooa de disque dur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-298">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="327e5-299">Chemin d’accès de hello source complet du répertoire local de hello où le disque dur virtuel est stocké pratique et utiliser ensuite AzCopy tooupload il tooAzure stockage.</span><span class="sxs-lookup"><span data-stu-id="327e5-299">Have hello complete source path of hello local directory where VHD is stored handy, and then using AzCopy tooupload it tooAzure Storage.</span></span>

#### <a name="step-1-export-vhd-tooa-local-directory"></a><span data-ttu-id="327e5-300">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="327e5-300">Step 1.</span></span> <span data-ttu-id="327e5-301">Exporter le répertoire local de tooa de disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="327e5-301">Export VHD tooa local directory</span></span>
##### <a name="copy-a-vhd-from-aws"></a><span data-ttu-id="327e5-302">Copie d’un disque dur virtuel depuis AWS</span><span class="sxs-lookup"><span data-stu-id="327e5-302">Copy a VHD from AWS</span></span>
1. <span data-ttu-id="327e5-303">Si vous utilisez AWS, exportez hello EC2 instance tooa disque dur virtuel dans un compartiment Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="327e5-303">If you are using AWS, export hello EC2 instance tooa VHD in an Amazon S3 bucket.</span></span> <span data-ttu-id="327e5-304">Suivez les étapes de hello décrites dans la documentation Amazon pour outil de l’interface de ligne de commande (CLI) d’exportation les Instances d’Amazon EC2 tooinstall hello Amazon EC2 de hello et exécuter le fichier VHD de hello-instance-export-commande Créer une tâche tooexport hello EC2 instance tooa.</span><span class="sxs-lookup"><span data-stu-id="327e5-304">Follow hello steps described in hello Amazon documentation for Exporting Amazon EC2 Instances tooinstall hello Amazon EC2 command-line interface (CLI) tool and run hello create-instance-export-task command tooexport hello EC2 instance tooa VHD file.</span></span> <span data-ttu-id="327e5-305">Être vraiment toouse **VHD** hello disque &#95; IMAGE &#95; Variable FORMAT lors de l’exécution hello **créer-instance-export-tâche** commande.</span><span class="sxs-lookup"><span data-stu-id="327e5-305">Be sure toouse **VHD** for hello DISK&#95;IMAGE&#95;FORMAT variable when running hello **create-instance-export-task** command.</span></span> <span data-ttu-id="327e5-306">Hello fichier de disque dur virtuel exporté est enregistré dans le compartiment hello Amazon S3 que vous désignez pendant le processus.</span><span class="sxs-lookup"><span data-stu-id="327e5-306">hello exported VHD file is saved in hello Amazon S3 bucket you designate during that process.</span></span>

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. <span data-ttu-id="327e5-307">Téléchargez le fichier de disque dur virtuel de hello de compartiment de S3 hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-307">Download hello VHD file from hello S3 bucket.</span></span> <span data-ttu-id="327e5-308">Fichier de disque dur virtuel hello sélectionnez, puis **Actions** > **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="327e5-308">Select hello VHD file, then **Actions** > **Download**.</span></span>

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a><span data-ttu-id="327e5-309">Copie d’un disque dur virtuel à partir d’autres cloud hors Azure</span><span class="sxs-lookup"><span data-stu-id="327e5-309">Copy a VHD from other non-Azure cloud</span></span>
<span data-ttu-id="327e5-310">Si vous effectuez une migration à partir d’Azure Cloud Storage tooAzure disque dur virtuel, vous devez d’abord exporter répertoire local de tooa de disque dur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-310">If you are migrating VHD from non-Azure Cloud Storage tooAzure, you must first export hello VHD tooa local directory.</span></span> <span data-ttu-id="327e5-311">Copiez le chemin d’accès de hello source complet du répertoire local de hello où le disque dur virtuel est stocké.</span><span class="sxs-lookup"><span data-stu-id="327e5-311">Copy hello complete source path of hello local directory where VHD is stored.</span></span>

##### <a name="copy-a-vhd-from-on-premises"></a><span data-ttu-id="327e5-312">Copie d’un disque dur virtuel en local</span><span class="sxs-lookup"><span data-stu-id="327e5-312">Copy a VHD from on-premises</span></span>
<span data-ttu-id="327e5-313">Si vous migrez un disque dur virtuel à partir d’un environnement sur site, vous devez le chemin d’accès de la source complet hello où le disque dur virtuel est stocké.</span><span class="sxs-lookup"><span data-stu-id="327e5-313">If you are migrating VHD from an on-premises environment, you will need hello complete source path where VHD is stored.</span></span> <span data-ttu-id="327e5-314">le chemin d’accès de Hello source peut être un partage de fichier ou emplacement de serveur.</span><span class="sxs-lookup"><span data-stu-id="327e5-314">hello source path could be a server location or file share.</span></span>

#### <a name="step-2-create-hello-destination-for-your-vhd"></a><span data-ttu-id="327e5-315">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="327e5-315">Step 2.</span></span> <span data-ttu-id="327e5-316">Créer destination hello pour votre disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="327e5-316">Create hello destination for your VHD</span></span>
<span data-ttu-id="327e5-317">Créez un compte de stockage pour gérer vos disques durs virtuels.</span><span class="sxs-lookup"><span data-stu-id="327e5-317">Create a storage account for maintaining your VHDs.</span></span> <span data-ttu-id="327e5-318">Prendre en compte les points suivants lors de la planification de l’emplacement de hello toostore vos disques durs virtuels :</span><span class="sxs-lookup"><span data-stu-id="327e5-318">Consider hello following points when planning where toostore your VHDs:</span></span>

* <span data-ttu-id="327e5-319">compte de stockage Hello cible peut être un stockage standard ou premium, selon vos besoins de l’application.</span><span class="sxs-lookup"><span data-stu-id="327e5-319">hello target storage account could be standard or premium storage depending on your application requirement.</span></span>
* <span data-ttu-id="327e5-320">région du compte de stockage Hello doit être identique en tant que machines virtuelles Azure capable de stockage Premium vous allez créer dans la phase finale de hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-320">hello storage account region must be same as Premium Storage capable Azure VMs you will create in hello final stage.</span></span> <span data-ttu-id="327e5-321">Vous pouvez copier le nouveau compte de stockage tooa ou hello toouse de plan même compte de stockage selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="327e5-321">You could copy tooa new storage account, or plan toouse hello same storage account based on your needs.</span></span>
* <span data-ttu-id="327e5-322">Copiez et enregistrez la clé de compte de stockage hello hello destination du compte de stockage pour l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-322">Copy and save hello storage account key of hello destination storage account for hello next stage.</span></span>

<span data-ttu-id="327e5-323">Nous recommandons de vous déplacer toutes les données pour le stockage de production la charge de travail toouse premium.</span><span class="sxs-lookup"><span data-stu-id="327e5-323">We strongly recommend you moving all data for production workload toouse premium storage.</span></span>

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a><span data-ttu-id="327e5-324">Étape 3.</span><span class="sxs-lookup"><span data-stu-id="327e5-324">Step 3.</span></span> <span data-ttu-id="327e5-325">Télécharger le disque dur virtuel de hello tooAzure stockage</span><span class="sxs-lookup"><span data-stu-id="327e5-325">Upload hello VHD tooAzure Storage</span></span>
<span data-ttu-id="327e5-326">Maintenant que vous avez votre disque dur virtuel dans un répertoire local de hello, vous pouvez utiliser AzCopy ou AzurePowerShell tooupload hello .vhd fichier tooAzure stockage.</span><span class="sxs-lookup"><span data-stu-id="327e5-326">Now that you have your VHD in hello local directory, you can use AzCopy or AzurePowerShell tooupload hello .vhd file tooAzure Storage.</span></span> <span data-ttu-id="327e5-327">Les deux options sont fournies ici :</span><span class="sxs-lookup"><span data-stu-id="327e5-327">Both options are provided here:</span></span>

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a><span data-ttu-id="327e5-328">Option 1 : À l’aide de fichier .vhd de Azure PowerShell Add-AzureVhd tooupload hello</span><span class="sxs-lookup"><span data-stu-id="327e5-328">Option 1: Using Azure PowerShell Add-AzureVhd tooupload hello .vhd file</span></span>

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

<span data-ttu-id="327e5-329">Un exemple <Uri>peut être ***« https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd »***.</span><span class="sxs-lookup"><span data-stu-id="327e5-329">An example <Uri> might be ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***.</span></span> <span data-ttu-id="327e5-330">Un exemple <FileInfo>peut être ***« C:\path\to\upload.vhd »***.</span><span class="sxs-lookup"><span data-stu-id="327e5-330">An example <FileInfo> might be ***"C:\path\to\upload.vhd"***.</span></span>

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a><span data-ttu-id="327e5-331">Option 2 : À l’aide de fichier .vhd de AzCopy tooupload hello</span><span class="sxs-lookup"><span data-stu-id="327e5-331">Option 2: Using AzCopy tooupload hello .vhd file</span></span>
<span data-ttu-id="327e5-332">À l’aide de AzCopy, vous pouvez charger facilement hello VHD sur hello Internet.</span><span class="sxs-lookup"><span data-stu-id="327e5-332">Using AzCopy, you can easily upload hello VHD over hello Internet.</span></span> <span data-ttu-id="327e5-333">Selon la taille de hello Hello disques durs virtuels, cela peut prendre le temps.</span><span class="sxs-lookup"><span data-stu-id="327e5-333">Depending on hello size of hello VHDs, this may take time.</span></span> <span data-ttu-id="327e5-334">N’oubliez pas les limites des entrées/sorties comptes de stockage toocheck hello lors de l’utilisation de cette option.</span><span class="sxs-lookup"><span data-stu-id="327e5-334">Remember toocheck hello storage account ingress/egress limits when using this option.</span></span> <span data-ttu-id="327e5-335">Pour plus d’informations, consultez [Objectifs de performance et d’évolutivité d’Azure Storage](storage-scalability-targets.md) .</span><span class="sxs-lookup"><span data-stu-id="327e5-335">See [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) for details.</span></span>

1. <span data-ttu-id="327e5-336">Téléchargez et installez AzCopy à partir d’ici : [version la plus récente d’AzCopy](http://aka.ms/downloadazcopy)</span><span class="sxs-lookup"><span data-stu-id="327e5-336">Download and install AzCopy from here: [Latest version of AzCopy](http://aka.ms/downloadazcopy)</span></span>
2. <span data-ttu-id="327e5-337">Ouvrez Azure PowerShell et accédez toohello où AzCopy est installé.</span><span class="sxs-lookup"><span data-stu-id="327e5-337">Open Azure PowerShell and go toohello folder where AzCopy is installed.</span></span>
3. <span data-ttu-id="327e5-338">Fichier de disque dur virtuel hello toocopy à partir de « Source » de la commande suivante de hello d’utilisation trop « Destination ».</span><span class="sxs-lookup"><span data-stu-id="327e5-338">Use hello following command toocopy hello VHD file from "Source" too"Destination".</span></span>

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    <span data-ttu-id="327e5-339">Exemple :</span><span class="sxs-lookup"><span data-stu-id="327e5-339">Example:</span></span>

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    <span data-ttu-id="327e5-340">Voici les descriptions des paramètres hello utilisés Bonjour AzCopy commande :</span><span class="sxs-lookup"><span data-stu-id="327e5-340">Here are descriptions of hello parameters used in hello AzCopy command:</span></span>

   * <span data-ttu-id="327e5-341">**/ Source :  *&lt;source&gt;:***  emplacement du dossier de hello ou URL de conteneur de stockage qui contient le disque dur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-341">**/Source: *&lt;source&gt;:*** Location of hello folder or storage container URL that contains hello VHD.</span></span>
   * <span data-ttu-id="327e5-342">**/ SourceKey :  *&lt;clé de compte source&gt;:***  clé de compte de stockage hello source du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="327e5-342">**/SourceKey: *&lt;source-account-key&gt;:*** Storage account key of hello source storage account.</span></span>
   * <span data-ttu-id="327e5-343">**/ Dest :  *&lt;destination&gt;:***  toocopy de URL de conteneur de stockage hello disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="327e5-343">**/Dest: *&lt;destination&gt;:*** Storage container URL toocopy hello VHD to.</span></span>
   * <span data-ttu-id="327e5-344">**/ DestKey :  *&lt;clé de compte dest&gt;:***  clé de compte de stockage du compte de stockage de destination hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-344">**/DestKey: *&lt;dest-account-key&gt;:*** Storage account key of hello destination storage account.</span></span>
   * <span data-ttu-id="327e5-345">**/ BlobType : page :** spécifie cette destination hello est un objet blob de pages.</span><span class="sxs-lookup"><span data-stu-id="327e5-345">**/BlobType: page:** Specifies that hello destination is a page blob.</span></span>
   * <span data-ttu-id="327e5-346">**/ Modèle :  *&lt;nom de fichier&gt;:***  spécifier le nom fichier hello de toocopy de disque dur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-346">**/Pattern: *&lt;file-name&gt;:*** Specify hello file name of hello VHD toocopy.</span></span>

<span data-ttu-id="327e5-347">Pour plus d’informations sur l’utilisation de AzCopy outil, consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="327e5-347">For details on using AzCopy tool, see [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

##### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="327e5-348">Autres options de téléchargement d’un disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="327e5-348">Other options for uploading a VHD</span></span>
<span data-ttu-id="327e5-349">Vous pouvez également télécharger un compte de stockage de tooyour de disque dur virtuel à l’aide de hello suivant signifie :</span><span class="sxs-lookup"><span data-stu-id="327e5-349">You can also upload a VHD tooyour storage account using one of hello following means:</span></span>

* [<span data-ttu-id="327e5-350">API de copie d’un objet blob de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="327e5-350">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [<span data-ttu-id="327e5-351">Téléchargement d’objets blob dans Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="327e5-351">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
* [<span data-ttu-id="327e5-352">Référence sur l’API REST du service Import/Export Storage</span><span class="sxs-lookup"><span data-stu-id="327e5-352">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> <span data-ttu-id="327e5-353">Nous recommandons l’utilisation de du service d’importation/exportation si l’estimation du temps de téléchargement est de plus de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="327e5-353">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="327e5-354">Vous pouvez utiliser [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate les temps de hello à partir de l’unité de taille et de transfert de données.</span><span class="sxs-lookup"><span data-stu-id="327e5-354">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span>
>
> <span data-ttu-id="327e5-355">Importation/exportation peut être utilisé le compte de stockage standard toocopy tooa.</span><span class="sxs-lookup"><span data-stu-id="327e5-355">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="327e5-356">Vous devez toocopy de compte de stockage toopremium de stockage standard à l’aide d’un outil tel que AzCopy.</span><span class="sxs-lookup"><span data-stu-id="327e5-356">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>
>
>

## <span data-ttu-id="327e5-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Créer des machines virtuelles Azure à l’aide du stockage Premium</span><span class="sxs-lookup"><span data-stu-id="327e5-357"><a name="create-azure-virtual-machine-using-premium-storage"></a>Create Azure VMs using Premium Storage</span></span>
<span data-ttu-id="327e5-358">Une fois hello disque dur virtuel est un compte de stockage toohello téléchargé ou copié souhaitée, suivez les instructions de hello dans cette hello tooregister de section disque dur virtuel en tant qu’image de système d’exploitation, ou disque de système d’exploitation en fonction de votre scénario et puis créer une instance de la machine virtuelle à partir de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="327e5-358">After hello VHD is uploaded or copied toohello desired storage account, follow hello instructions in this section tooregister hello VHD as an OS image, or OS disk depending on your scenario and then create a VM instance from it.</span></span> <span data-ttu-id="327e5-359">disque de données Hello disque dur virtuel peut être attaché toohello machine virtuelle qui a été créé.</span><span class="sxs-lookup"><span data-stu-id="327e5-359">hello data disk VHD can be attached toohello VM once it is created.</span></span>
<span data-ttu-id="327e5-360">Un exemple de script de migration est fournie à la fin de hello de cette section.</span><span class="sxs-lookup"><span data-stu-id="327e5-360">A sample migration script is provided at hello end of this section.</span></span> <span data-ttu-id="327e5-361">Ce script simple ne correspond pas à tous les scénarios.</span><span class="sxs-lookup"><span data-stu-id="327e5-361">This simple script does not match all scenarios.</span></span> <span data-ttu-id="327e5-362">Vous devrez peut-être tooupdate hello script toomatch avec votre scénario spécifique.</span><span class="sxs-lookup"><span data-stu-id="327e5-362">You may need tooupdate hello script toomatch with your specific scenario.</span></span> <span data-ttu-id="327e5-363">toosee si ce script s’applique tooyour scénario, consultez la section ci-dessous [un exemple de Script de Migration](#a-sample-migration-script).</span><span class="sxs-lookup"><span data-stu-id="327e5-363">toosee if this script applies tooyour scenario, see below [A Sample Migration Script](#a-sample-migration-script).</span></span>

### <a name="checklist"></a><span data-ttu-id="327e5-364">Liste de contrôle</span><span class="sxs-lookup"><span data-stu-id="327e5-364">Checklist</span></span>
1. <span data-ttu-id="327e5-365">Attendez que tous les disques de disque dur virtuel hello copie est terminée.</span><span class="sxs-lookup"><span data-stu-id="327e5-365">Wait until all hello VHD disks copying is complete.</span></span>
2. <span data-ttu-id="327e5-366">Assurez-vous que le stockage Premium est disponible dans la région de hello que vous effectuez la migration.</span><span class="sxs-lookup"><span data-stu-id="327e5-366">Make sure Premium Storage is available in hello region you are migrating to.</span></span>
3. <span data-ttu-id="327e5-367">Décidez nouvelle série VM hello, que vous allez utiliser.</span><span class="sxs-lookup"><span data-stu-id="327e5-367">Decide hello new VM series you will be using.</span></span> <span data-ttu-id="327e5-368">Il doit être un stockage Premium compatibles, et taille de hello doit être en fonction de la disponibilité de hello dans la région de hello et selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="327e5-368">It should be a Premium Storage capable, and hello size should be depending on hello availability in hello region and based on your needs.</span></span>
4. <span data-ttu-id="327e5-369">Décidez de taille virtuelle exacte de hello, que vous allez utiliser.</span><span class="sxs-lookup"><span data-stu-id="327e5-369">Decide hello exact VM size you will use.</span></span> <span data-ttu-id="327e5-370">Taille de machine virtuelle doit toobe toosupport suffisamment grand hello différents disques de données que vous avez.</span><span class="sxs-lookup"><span data-stu-id="327e5-370">VM size needs toobe large enough toosupport hello number of data disks you have.</span></span> <span data-ttu-id="327e5-371">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="327e5-371">E.g.</span></span> <span data-ttu-id="327e5-372">Si vous avez 4 disques de données, hello machine virtuelle doit avoir au moins 2 cœurs.</span><span class="sxs-lookup"><span data-stu-id="327e5-372">if you have 4 data disks, hello VM must have 2 or more cores.</span></span> <span data-ttu-id="327e5-373">Prenez également en considération les besoins en puissance, mémoire et bande passante réseau.</span><span class="sxs-lookup"><span data-stu-id="327e5-373">Also, consider processing power, memory and network bandwidth needs.</span></span>
5. <span data-ttu-id="327e5-374">Créer un compte Premium Storage dans la région cible hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-374">Create a Premium Storage account in hello target region.</span></span> <span data-ttu-id="327e5-375">C’est le compte à utiliser pour hello hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="327e5-375">This is hello account you will use for hello new VM.</span></span>
6. <span data-ttu-id="327e5-376">Des informations VM hello en cours pratiques, y compris les listes de hello des disques et des objets BLOB de disque dur virtuel correspondant.</span><span class="sxs-lookup"><span data-stu-id="327e5-376">Have hello current VM details handy, including hello list of disks and corresponding VHD blobs.</span></span>

<span data-ttu-id="327e5-377">Préparez votre application pour les interruptions de service.</span><span class="sxs-lookup"><span data-stu-id="327e5-377">Prepare your application for downtime.</span></span> <span data-ttu-id="327e5-378">toodo une nouvelle migration, vous avez toostop tout traitement hello dans le système actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-378">toodo a clean migration, you have toostop all hello processing in hello current system.</span></span> <span data-ttu-id="327e5-379">Alors seulement vous pouvez l’obtenir état tooconsistent dont vous pouvez migrer toohello nouvelle plateforme.</span><span class="sxs-lookup"><span data-stu-id="327e5-379">Only then you can get it tooconsistent state which you can migrate toohello new platform.</span></span> <span data-ttu-id="327e5-380">Temps d’arrêt dépend de la quantité hello d’hello disques toomigrate.</span><span class="sxs-lookup"><span data-stu-id="327e5-380">Downtime duration will depend on hello amount of data in hello disks toomigrate.</span></span>

> [!NOTE]
> <span data-ttu-id="327e5-381">Si vous créez un gestionnaire de ressources Azure VM à partir d’un disque spécialisé de disque dur virtuel, consultez trop[ce modèle](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) pour le déploiement de VM Gestionnaire de ressources à l’aide du disque existant.</span><span class="sxs-lookup"><span data-stu-id="327e5-381">If you are creating an Azure Resource Manager VM from a specialized VHD Disk, please refer too[this template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) for deploying Resource Manager VM using existing disk.</span></span>
>
>

### <a name="register-your-vhd"></a><span data-ttu-id="327e5-382">Enregistrez votre disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="327e5-382">Register your VHD</span></span>
<span data-ttu-id="327e5-383">toocreate une machine virtuelle à partir de disque dur virtuel du système d’exploitation ou tooattach un tooa de disque de données nouvelle machine virtuelle, vous devez tout d’abord les enregistrer.</span><span class="sxs-lookup"><span data-stu-id="327e5-383">toocreate a VM from OS VHD or tooattach a data disk tooa new VM, you must first register them.</span></span> <span data-ttu-id="327e5-384">Suivez les étapes ci-dessous en fonction de votre scénario de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="327e5-384">Follow steps below depending on your VHD's scenario.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="327e5-385">Généralisé toocreate de disque dur virtuel du système d’exploitation de plusieurs instances de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="327e5-385">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="327e5-386">Après avoir généralisé image du système d’exploitation du disque dur virtuel est chargé de compte de stockage toohello, inscrire comme une **Image de machine virtuelle Azure** afin que vous pouvez créer une ou plusieurs instances de machine virtuelle à partir de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="327e5-386">After generalized OS image VHD is uploaded toohello storage account, register it as an **Azure VM Image** so that you can create one or more VM instances from it.</span></span> <span data-ttu-id="327e5-387">Utilisez hello suivant tooregister d’applets de commande PowerShell de votre disque dur virtuel comme une image de système d’exploitation de la machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="327e5-387">Use hello following PowerShell cmdlets tooregister your VHD as an Azure VM OS image.</span></span> <span data-ttu-id="327e5-388">Fournir l’URL du conteneur terminée hello où le disque dur virtuel a été copié dans.</span><span class="sxs-lookup"><span data-stu-id="327e5-388">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

<span data-ttu-id="327e5-389">Copiez et enregistrez le nom hello de cette nouvelle Image de machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="327e5-389">Copy and save hello name of this new Azure VM Image.</span></span> <span data-ttu-id="327e5-390">Dans l’exemple hello ci-dessus, il est *OSImageName*.</span><span class="sxs-lookup"><span data-stu-id="327e5-390">In hello example above, it is *OSImageName*.</span></span>

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="327e5-391">Toocreate de disque dur virtuel du système d’exploitation unique une seule instance de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="327e5-391">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="327e5-392">Après hello unique disque dur virtuel de système d’exploitation est téléchargés toohello stockage compte, inscrivez-vous en tant qu’un **disque de système d’exploitation Azure** afin que vous pouvez créer une instance de machine virtuelle à partir de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="327e5-392">After hello unique OS VHD is uploaded toohello storage account, register it as an **Azure OS Disk** so that you can create a VM instance from it.</span></span> <span data-ttu-id="327e5-393">Utilisez ces tooregister d’applets de commande PowerShell de votre disque dur virtuel comme un disque de système d’exploitation Azure.</span><span class="sxs-lookup"><span data-stu-id="327e5-393">Use these PowerShell cmdlets tooregister your VHD as an Azure OS Disk.</span></span> <span data-ttu-id="327e5-394">Fournir l’URL du conteneur terminée hello où le disque dur virtuel a été copié dans.</span><span class="sxs-lookup"><span data-stu-id="327e5-394">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

<span data-ttu-id="327e5-395">Copiez et enregistrez le nom hello de ce nouveau disque de système d’exploitation Azure.</span><span class="sxs-lookup"><span data-stu-id="327e5-395">Copy and save hello name of this new Azure OS Disk.</span></span> <span data-ttu-id="327e5-396">Dans l’exemple hello ci-dessus, il est *OSDisk*.</span><span class="sxs-lookup"><span data-stu-id="327e5-396">In hello example above, it is *OSDisk*.</span></span>

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a><span data-ttu-id="327e5-397">Toobe de disque dur virtuel de disque de données attaché à une ou plusieurs instances de toonew machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="327e5-397">Data disk VHD toobe attached toonew Azure VM instance(s)</span></span>
<span data-ttu-id="327e5-398">Une fois hello disque de données est de disque dur virtuel téléchargé toostorage compte, enregistrer en tant qu’un disque de données Azure afin qu’il puisse être attachée tooyour nouvelle série DS, DSv2 série ou une instance de la machine virtuelle Azure de série GS.</span><span class="sxs-lookup"><span data-stu-id="327e5-398">After hello data disk VHD is uploaded toostorage account, register it as an Azure Data Disk so that it can be attached tooyour new DS Series, DSv2 series or GS Series Azure VM instance.</span></span>

<span data-ttu-id="327e5-399">Utilisez ces tooregister d’applets de commande PowerShell de votre disque dur virtuel en tant qu’un disque de données Azure.</span><span class="sxs-lookup"><span data-stu-id="327e5-399">Use these PowerShell cmdlets tooregister your VHD as an Azure Data Disk.</span></span> <span data-ttu-id="327e5-400">Fournir l’URL du conteneur terminée hello où le disque dur virtuel a été copié dans.</span><span class="sxs-lookup"><span data-stu-id="327e5-400">Provide hello complete container URL where VHD was copied to.</span></span>

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

<span data-ttu-id="327e5-401">Copiez et enregistrez le nom hello de ce nouveau disque de données Azure.</span><span class="sxs-lookup"><span data-stu-id="327e5-401">Copy and save hello name of this new Azure Data Disk.</span></span> <span data-ttu-id="327e5-402">Dans l’exemple hello ci-dessus, il est *DataDisk*.</span><span class="sxs-lookup"><span data-stu-id="327e5-402">In hello example above, it is *DataDisk*.</span></span>

### <a name="create-a-premium-storage-capable-vm"></a><span data-ttu-id="327e5-403">Création d’un compte compatible Premium Storage</span><span class="sxs-lookup"><span data-stu-id="327e5-403">Create a Premium Storage capable VM</span></span>
<span data-ttu-id="327e5-404">Une fois hello image de système d’exploitation ou disque de système d’exploitation sont inscrits, créez une nouvelle série DS, le dsv2 ou la machine virtuelle de série GS.</span><span class="sxs-lookup"><span data-stu-id="327e5-404">Once hello OS image or OS disk are registered, create a new DS-series, DSv2-series or GS-series VM.</span></span> <span data-ttu-id="327e5-405">Vous utiliserez image de système d’exploitation hello ou nom de disque de système d’exploitation que vous avez enregistré.</span><span class="sxs-lookup"><span data-stu-id="327e5-405">You will be using hello operating system image or operating system disk name that you registered.</span></span> <span data-ttu-id="327e5-406">Sélectionnez le type de machine virtuelle hello à partir de la couche de stockage Premium hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-406">Select hello VM type from hello Premium Storage tier.</span></span> <span data-ttu-id="327e5-407">Dans l’exemple ci-dessous, nous utilisons hello *Standard_DS2* taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="327e5-407">In example below, we are using hello *Standard_DS2* VM size.</span></span>

> [!NOTE]
> <span data-ttu-id="327e5-408">Mettre à jour toomake de taille de disque hello qu’elle correspond à votre capacité et les exigences de performances et les tailles de disque Azure hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-408">Update hello disk size toomake sure it matches your capacity and performance requirements and hello available Azure disk sizes.</span></span>
>
>

<span data-ttu-id="327e5-409">Applets de commande PowerShell suivante pour hello étape par étape ci-dessous toocreate hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="327e5-409">Follow hello step by step PowerShell cmdlets below toocreate hello new VM.</span></span> <span data-ttu-id="327e5-410">Tout d’abord, définissez les paramètres communs hello :</span><span class="sxs-lookup"><span data-stu-id="327e5-410">First, set hello common parameters:</span></span>

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

<span data-ttu-id="327e5-411">Commencez par créer un service cloud dans lequel vous hébergerez vos nouvelles machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="327e5-411">First, create a cloud service in which you will be hosting your new VMs.</span></span>

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

<span data-ttu-id="327e5-412">Ensuite, selon votre scénario, créez instance de machine virtuelle Azure hello de hello Image de système d’exploitation ou disque de système d’exploitation que vous avez enregistré.</span><span class="sxs-lookup"><span data-stu-id="327e5-412">Next, depending on your scenario, create hello Azure VM instance from either hello OS Image or OS Disk that you registered.</span></span>

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a><span data-ttu-id="327e5-413">Généralisé toocreate de disque dur virtuel du système d’exploitation de plusieurs instances de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="327e5-413">Generalized Operating System VHD toocreate multiple Azure VM instances</span></span>
<span data-ttu-id="327e5-414">Créer hello un ou plusieurs des instances pour l’ordinateur virtuel Azure de série DS à l’aide de hello **Image du système d’exploitation Azure** que vous avez enregistré.</span><span class="sxs-lookup"><span data-stu-id="327e5-414">Create hello one or more new DS Series Azure VM instances using hello **Azure OS Image** that you registered.</span></span> <span data-ttu-id="327e5-415">Spécifiez ce nom de l’Image de système d’exploitation dans la configuration d’ordinateur virtuel hello lorsque vous créez la nouvelle machine virtuelle comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="327e5-415">Specify this OS Image name in hello VM configuration when creating new VM as shown below.</span></span>

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a><span data-ttu-id="327e5-416">Toocreate de disque dur virtuel du système d’exploitation unique une seule instance de machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="327e5-416">Unique Operating System VHD toocreate a single Azure VM instance</span></span>
<span data-ttu-id="327e5-417">Créer une nouvelle instance de machine virtuelle Azure de série DS à l’aide de hello **disque de système d’exploitation Azure** que vous avez enregistré.</span><span class="sxs-lookup"><span data-stu-id="327e5-417">Create a new DS series Azure VM instance using hello **Azure OS Disk** that you registered.</span></span> <span data-ttu-id="327e5-418">Spécifiez ce nom de disque de système d’exploitation dans la configuration d’ordinateur virtuel hello lors de la création de hello nouvelle machine virtuelle comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="327e5-418">Specify this OS Disk name in hello VM configuration when creating hello new VM as shown below.</span></span>

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

<span data-ttu-id="327e5-419">Spécifiez d’autres informations de machine virtuelle Azure, comme un service cloud, une région, un compte de stockage, un groupe à haute disponibilité et une stratégie de mise en cache.</span><span class="sxs-lookup"><span data-stu-id="327e5-419">Specify other Azure VM information, such as a cloud service, region, storage account, availability set, and caching policy.</span></span> <span data-ttu-id="327e5-420">Notez qu’instance de machine virtuelle hello doit être colocalisé avec le système d’exploitation associé ou les disques de données, le compte de service, région et le stockage cloud hello sélectionné doit être dans hello même emplacement que hello sous-jacent de disques durs virtuels de ces disques.</span><span class="sxs-lookup"><span data-stu-id="327e5-420">Note that hello VM instance must be co-located with associated operating system or data disks, so hello selected cloud service, region and storage account must all be in hello same location as hello underlying VHDs of those disks.</span></span>

### <a name="attach-data-disk"></a><span data-ttu-id="327e5-421">Attacher un disque de données</span><span class="sxs-lookup"><span data-stu-id="327e5-421">Attach data disk</span></span>
<span data-ttu-id="327e5-422">Enfin, si vous avez enregistré données disque VHD, définissez-les toohello nouveau stockage Premium compatibles avec Azure VM.</span><span class="sxs-lookup"><span data-stu-id="327e5-422">Lastly, if you have registered data disk VHDs, attach them toohello new Premium Storage capable Azure VM.</span></span>

<span data-ttu-id="327e5-423">Utiliser la suite PowerShell applet de commande tooattach données disque toohello nouvel ordinateur virtuel et spécifiez hello mise en cache de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="327e5-423">Use following PowerShell cmdlet tooattach data disk toohello new VM and specify hello caching policy.</span></span> <span data-ttu-id="327e5-424">Dans l’exemple ci-dessous hello mise en cache de la stratégie est défini trop*ReadOnly*.</span><span class="sxs-lookup"><span data-stu-id="327e5-424">In example below hello caching policy is set too*ReadOnly*.</span></span>

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> <span data-ttu-id="327e5-425">Il peut y avoir toosupport nécessaire des étapes supplémentaires votre application est ne pas couvert par ce guide.</span><span class="sxs-lookup"><span data-stu-id="327e5-425">There may be additional steps necessary toosupport your application that is not be covered by this guide.</span></span>
>
>

### <a name="checking-and-plan-backup"></a><span data-ttu-id="327e5-426">Vérification et planification de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="327e5-426">Checking and plan backup</span></span>
<span data-ttu-id="327e5-427">Une fois les hello nouvel ordinateur virtuel est en cours d’exécution, l’accès à l’aide de hello même id de connexion et mot de passe est hello d’ordinateur virtuel d’origine et vérifier que tout fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="327e5-427">Once hello new VM is up and running, access it using hello same login id and password is as hello original VM, and verify that everything is working as expected.</span></span> <span data-ttu-id="327e5-428">Tous les paramètres de hello, y compris les volumes de hello répartie, est présents en hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="327e5-428">All hello settings, including hello striped volumes, would be present in hello new VM.</span></span>

<span data-ttu-id="327e5-429">dernière étape de Hello est la planification de sauvegarde et de maintenance tooplan pour hello que nouvelle machine virtuelle en fonction des besoins de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-429">hello last step is tooplan backup and maintenance schedule for hello new VM based on hello application's needs.</span></span>

### <span data-ttu-id="327e5-430"><a name="a-sample-migration-script"></a>Un exemple de script de migration</span><span class="sxs-lookup"><span data-stu-id="327e5-430"><a name="a-sample-migration-script"></a>A sample migration script</span></span>
<span data-ttu-id="327e5-431">Si vous avez plusieurs machines virtuelles toomigrate, automation via des scripts PowerShell s’avérera utile.</span><span class="sxs-lookup"><span data-stu-id="327e5-431">If you have multiple VMs toomigrate, automation through PowerShell scripts will be helpful.</span></span> <span data-ttu-id="327e5-432">Voici un exemple de script qui automatise la migration hello d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="327e5-432">Following is a sample script that automates hello migration of a VM.</span></span> <span data-ttu-id="327e5-433">Notez que script ci-dessous n'est qu’un exemple et il existe quelques hypothèses sur les disques de machine virtuelle en cours hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-433">Note that below script is only an example, and there are few assumptions made about hello current VM disks.</span></span> <span data-ttu-id="327e5-434">Vous devrez peut-être tooupdate hello script toomatch avec votre scénario spécifique.</span><span class="sxs-lookup"><span data-stu-id="327e5-434">You may need tooupdate hello script toomatch with your specific scenario.</span></span>

<span data-ttu-id="327e5-435">les hypothèses Hello sont :</span><span class="sxs-lookup"><span data-stu-id="327e5-435">hello assumptions are:</span></span>

* <span data-ttu-id="327e5-436">Vous créez des machines virtuelles Azure classiques.</span><span class="sxs-lookup"><span data-stu-id="327e5-436">You are creating classic Azure VMs.</span></span>
* <span data-ttu-id="327e5-437">Vos disques de système d’exploitation source et disques de données source sont sur le même compte de stockage et le même conteneur.</span><span class="sxs-lookup"><span data-stu-id="327e5-437">Your source OS Disks and source Data Disks are in same storage account and same container.</span></span> <span data-ttu-id="327e5-438">Si vos disques de système d’exploitation et les disques de données ne sont pas dans hello même placer, vous pouvez utiliser AzCopy ou Azure PowerShell toocopy disques durs virtuels sur les comptes de stockage et les conteneurs.</span><span class="sxs-lookup"><span data-stu-id="327e5-438">If your OS Disks and Data Disks are not in hello same place, you can use AzCopy or Azure PowerShell toocopy VHDs over storage accounts and containers.</span></span> <span data-ttu-id="327e5-439">Consultez l’étape précédente de toohello : [disque dur virtuel de la copie avec AzCopy ou PowerShell](#copy-vhd-with-azcopy-or-powershell).</span><span class="sxs-lookup"><span data-stu-id="327e5-439">Refer toohello previous step: [Copy VHD with AzCopy or PowerShell](#copy-vhd-with-azcopy-or-powershell).</span></span> <span data-ttu-id="327e5-440">Modification de cette toomeet script votre scénario est un autre choix, mais nous recommandons d’utiliser AzCopy ou PowerShell, car il est plus facile et plus rapide.</span><span class="sxs-lookup"><span data-stu-id="327e5-440">Editing this script toomeet your scenario is another choice, but we recommend using AzCopy or PowerShell since it is easier and faster.</span></span>

<span data-ttu-id="327e5-441">script d’automatisation Hello est fourni ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="327e5-441">hello automation script is provided below.</span></span> <span data-ttu-id="327e5-442">Remplacer du texte avec vos informations et mettre à jour de hello script toomatch avec votre scénario spécifique.</span><span class="sxs-lookup"><span data-stu-id="327e5-442">Replace text with your information and update hello script toomatch with your specific scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="327e5-443">À l’aide de script existant de hello ne conserve pas la configuration du réseau de votre ordinateur virtuel source hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-443">Using hello existing script does not preserve hello network configuration of your source VM.</span></span> <span data-ttu-id="327e5-444">Vous aurez besoin des paramètres de mise en réseau toore-config hello sur vos ordinateurs virtuels migrés.</span><span class="sxs-lookup"><span data-stu-id="327e5-444">You will need toore-config hello networking settings on your migrated VMs.</span></span>
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
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


    #Check hello Azure PowerShell module version
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
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
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
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
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
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <span data-ttu-id="327e5-445"><a name="optimization"></a>Optimisation</span><span class="sxs-lookup"><span data-stu-id="327e5-445"><a name="optimization"></a>Optimization</span></span>
<span data-ttu-id="327e5-446">Votre configuration actuelle de la machine virtuelle peut être personnalisée en particulier les toowork correctement avec les disques Standard.</span><span class="sxs-lookup"><span data-stu-id="327e5-446">Your current VM configuration may be customized specifically toowork well with Standard disks.</span></span> <span data-ttu-id="327e5-447">Par exemple, tooincrease hello des performances à l’aide de disques dans un volume agrégé par bandes.</span><span class="sxs-lookup"><span data-stu-id="327e5-447">For instance, tooincrease hello performance by using many disks in a striped volume.</span></span> <span data-ttu-id="327e5-448">Par exemple, au lieu d’utiliser les 4 disques séparément sur un stockage Premium, vous pouvez être en mesure de toooptimize hello en ayant un seul disque.</span><span class="sxs-lookup"><span data-stu-id="327e5-448">For example, instead of using 4 disks separately on Premium Storage, you may be able toooptimize hello cost by having a single disk.</span></span> <span data-ttu-id="327e5-449">Optimisations, comme cette toobe besoin géré sur un cas par cas et nécessitent des étapes personnalisées après la migration de hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-449">Optimizations like this need toobe handled on a case by case basis and require custom steps after hello migration.</span></span> <span data-ttu-id="327e5-450">En outre, notez que ce processus ne fonctionne pas bien pour les bases de données et les applications qui dépendent de disposition du disque hello définie dans le programme d’installation hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-450">Also, note that this process may not well work for databases and applications that depend on hello disk layout defined in hello setup.</span></span>

##### <a name="preparation"></a><span data-ttu-id="327e5-451">Préparation</span><span class="sxs-lookup"><span data-stu-id="327e5-451">Preparation</span></span>
1. <span data-ttu-id="327e5-452">Hello complète Migration Simple, comme décrit dans hello à la section précédente.</span><span class="sxs-lookup"><span data-stu-id="327e5-452">Complete hello Simple Migration as described in hello earlier section.</span></span> <span data-ttu-id="327e5-453">Les optimisations se fera sur hello nouvel ordinateur virtuel après la migration de hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-453">Optimizations will be performed on hello new VM after hello migration.</span></span>
2. <span data-ttu-id="327e5-454">Définir les nouvelles tailles de disque hello nécessaires à la configuration de hello optimisé.</span><span class="sxs-lookup"><span data-stu-id="327e5-454">Define hello new disk sizes needed for hello optimized configuration.</span></span>
3. <span data-ttu-id="327e5-455">Déterminer le mappage de hello spécifications en cours/volumes de disques toohello nouveau disque.</span><span class="sxs-lookup"><span data-stu-id="327e5-455">Determine mapping of hello current disks/volumes toohello new disk specifications.</span></span>

##### <a name="execution-steps"></a><span data-ttu-id="327e5-456">Étapes d'exécution</span><span class="sxs-lookup"><span data-stu-id="327e5-456">Execution steps</span></span>
1. <span data-ttu-id="327e5-457">Créer des nouveaux disques hello avec des tailles appropriées de hello sur hello VM de stockage Premium.</span><span class="sxs-lookup"><span data-stu-id="327e5-457">Create hello new disks with hello right sizes on hello Premium Storage VM.</span></span>
2. <span data-ttu-id="327e5-458">Connexion toohello machine virtuelle et copie hello données de hello actuel toohello nouveau disque du volume qui mappe le volume de toothat.</span><span class="sxs-lookup"><span data-stu-id="327e5-458">Login toohello VM and copy hello data from hello current volume toohello new disk that maps toothat volume.</span></span> <span data-ttu-id="327e5-459">Cela pour tous les volumes en cours hello nécessitant toomap tooa nouveau disque.</span><span class="sxs-lookup"><span data-stu-id="327e5-459">Do this for all hello current volumes that need toomap tooa new disk.</span></span>
3. <span data-ttu-id="327e5-460">Ensuite, modifiez hello application paramètres tooswitch toohello nouveaux disques et détacher des anciens volumes de hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-460">Next, change hello application settings tooswitch toohello new disks, and detach hello old volumes.</span></span>

<span data-ttu-id="327e5-461">Pour le paramétrage d’application hello pour de meilleures performances de disque, consultez trop[optimisation des performances des applications](storage-premium-storage-performance.md#optimizing-application-performance).</span><span class="sxs-lookup"><span data-stu-id="327e5-461">For tuning hello application for better disk performance, please refer too[Optimizing Application Performance](storage-premium-storage-performance.md#optimizing-application-performance).</span></span>

### <a name="application-migrations"></a><span data-ttu-id="327e5-462">Migrations des applications</span><span class="sxs-lookup"><span data-stu-id="327e5-462">Application migrations</span></span>
<span data-ttu-id="327e5-463">Bases de données et d’autres applications complexes peuvent nécessiter des étapes spéciales, comme défini par le fournisseur d’application hello pour la migration de hello.</span><span class="sxs-lookup"><span data-stu-id="327e5-463">Databases and other complex applications may require special steps as defined by hello application provider for hello migration.</span></span> <span data-ttu-id="327e5-464">Consultez la documentation de l’application toorespective.</span><span class="sxs-lookup"><span data-stu-id="327e5-464">Please refer toorespective application documentation.</span></span> <span data-ttu-id="327e5-465">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="327e5-465">E.g.</span></span> <span data-ttu-id="327e5-466">la migration des bases de données se fait généralement via des étapes de sauvegarde et de restauration.</span><span class="sxs-lookup"><span data-stu-id="327e5-466">typically databases can be migrated through backup and restore.</span></span>

## <a name="next-steps"></a><span data-ttu-id="327e5-467">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="327e5-467">Next steps</span></span>
<span data-ttu-id="327e5-468">Consultez hello suivant des ressources pour des scénarios spécifiques pour la migration des ordinateurs virtuels :</span><span class="sxs-lookup"><span data-stu-id="327e5-468">See hello following resources for specific scenarios for migrating virtual machines:</span></span>

* [<span data-ttu-id="327e5-469">Migrer des machines virtuelles Azure entre les comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="327e5-469">Migrate Azure Virtual Machines between Storage Accounts</span></span>](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [<span data-ttu-id="327e5-470">Créez et téléchargez un tooAzure le disque dur virtuel de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="327e5-470">Create and upload a Windows Server VHD tooAzure.</span></span>](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="327e5-471">Création et téléchargement d’un disque dur virtuel qui contient hello système d’exploitation Linux</span><span class="sxs-lookup"><span data-stu-id="327e5-471">Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System</span></span>](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="327e5-472">Migration d’ordinateurs virtuels à partir d’Amazon AWS tooMicrosoft Azure</span><span class="sxs-lookup"><span data-stu-id="327e5-472">Migrating Virtual Machines from Amazon AWS tooMicrosoft Azure</span></span>](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

<span data-ttu-id="327e5-473">Consultez également hello suivant toolearn ressources plus d’informations sur le stockage Azure et les Machines virtuelles Azure :</span><span class="sxs-lookup"><span data-stu-id="327e5-473">Also, see hello following resources toolearn more about Azure Storage and Azure Virtual Machines:</span></span>

* [<span data-ttu-id="327e5-474">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="327e5-474">Azure Storage</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="327e5-475">Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="327e5-475">Azure Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="327e5-476">Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="327e5-476">Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads</span></span>](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
