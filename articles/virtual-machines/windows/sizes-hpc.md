---
title: tailles de machine virtuelle Windows aaaAzure - HPC | Documents Microsoft
description: "Répertorie les tailles disponibles pour Windows informatiques hautes performances machines virtuelles dans Azure hello différentes."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 092bc32cfe048f439ad833911bef4ed17eda7977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="c4af9-103">Tailles de machines virtuelles de calcul haute performance</span><span class="sxs-lookup"><span data-stu-id="c4af9-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="c4af9-104">Instances prenant en charge RDMA</span><span class="sxs-lookup"><span data-stu-id="c4af9-104">RDMA-capable instances</span></span>
<span data-ttu-id="c4af9-105">Un sous-ensemble des instances de calcul intensif hello (H16r, H16mr, A8 et A9) dotés d’une interface de réseau pour la connectivité d’accès (RDMA) direct à la mémoire à distance.</span><span class="sxs-lookup"><span data-stu-id="c4af9-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="c4af9-106">Cette interface est en plus des tailles de machine virtuelle toohello tooother disponibles de l’interface réseau Azure standard.</span><span class="sxs-lookup"><span data-stu-id="c4af9-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="c4af9-107">Cette interface permet hello prenant en charge RDMA instances toocommunicate sur un réseau InfiniBand, fonctionnant à des vitesses de Verification pour les ordinateurs virtuels H16r et H16mr et taux QDR pour les machines virtuelles A8 et A9.</span><span class="sxs-lookup"><span data-stu-id="c4af9-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="c4af9-108">Ces fonctions RDMA peuvent optimiser les performances des applications MPI (Message Passing Interface) et l’extensibilité de hello.</span><span class="sxs-lookup"><span data-stu-id="c4af9-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="c4af9-109">Voici la configuration requise pour les machines virtuelles Windows prenant en charge RDMA tooaccess hello réseau RDMA Azure :</span><span class="sxs-lookup"><span data-stu-id="c4af9-109">Following are requirements for RDMA-capable Windows VMs tooaccess hello Azure RDMA network:</span></span> 

* <span data-ttu-id="c4af9-110">**Système d’exploitation**</span><span class="sxs-lookup"><span data-stu-id="c4af9-110">**Operating system**</span></span>
  
  <span data-ttu-id="c4af9-111">Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="c4af9-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="c4af9-112">Actuellement, Windows Server 2016 ne prend pas en charge la connectivité RDMA dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c4af9-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="c4af9-113">**Disponibilité ou de service de cloud computing** : déployer des machines virtuelles hello prenant en charge RDMA dans hello même groupe à haute disponibilité (lorsque vous utilisez le modèle de déploiement du Gestionnaire de ressources Azure hello) ou hello même service cloud (lorsque vous utilisez le modèle de déploiement classique hello).</span><span class="sxs-lookup"><span data-stu-id="c4af9-113">**Availability set or cloud service** – Deploy hello RDMA-capable VMs in hello same availability set (when you use hello Azure Resource Manager deployment model) or hello same cloud service (when you use hello classic deployment model).</span></span> <span data-ttu-id="c4af9-114">Si vous utilisez Azure Batch, hello prenant en charge RDMA machines virtuelles doit être Bonjour même pool.</span><span class="sxs-lookup"><span data-stu-id="c4af9-114">If you use Azure Batch, hello RDMA-capable VMs must be in hello same pool.</span></span>

* <span data-ttu-id="c4af9-115">**MPI** : Microsoft MPI (MS-MPI) 2012 R2 ou version ultérieure, bibliothèque Intel MPI 5.x</span><span class="sxs-lookup"><span data-stu-id="c4af9-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="c4af9-116">Implémentations MPI prises en charge utilisent hello toocommunicate d’interface Microsoft Network Direct entre des instances.</span><span class="sxs-lookup"><span data-stu-id="c4af9-116">Supported MPI implementations use hello Microsoft Network Direct interface toocommunicate between instances.</span></span> 

* <span data-ttu-id="c4af9-117">**Espace d’adressage réseau RDMA** -réseau RDMA de hello dans Azure réserve hello adresse espace 172.16.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="c4af9-117">**RDMA network address space** - hello RDMA network in Azure reserves hello address space 172.16.0.0/16.</span></span> <span data-ttu-id="c4af9-118">toorun des applications MPI sur des instances déployées dans un réseau virtuel Azure, assurez-vous qu’espace d’adressage de réseau virtuel de hello ne chevauche pas le réseau RDMA de hello.</span><span class="sxs-lookup"><span data-stu-id="c4af9-118">toorun MPI applications on instances deployed in an Azure virtual network, make sure that hello virtual network address space does not overlap hello RDMA network.</span></span>

* <span data-ttu-id="c4af9-119">**Extension HpcVmDrivers VM** -sur les ordinateurs virtuels prenant en charge RDMA, vous devez ajouter hello HpcVmDrivers extension tooinstall Windows pilotes de périphérique réseau pour la connectivité RDMA.</span><span class="sxs-lookup"><span data-stu-id="c4af9-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add hello HpcVmDrivers extension tooinstall Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="c4af9-120">(Dans certains déploiements des instances A8 et A9, hello extension HpcVmDrivers est ajouté automatiquement.) tooadd hello VM extension tooa machine virtuelle, vous pouvez utiliser [Azure PowerShell](/powershell/azure/overview) applets de commande.</span><span class="sxs-lookup"><span data-stu-id="c4af9-120">(In certain deployments of A8 and A9 instances, hello HpcVmDrivers extension is added automatically.) tooadd hello VM extension tooa VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="c4af9-121">Hello suivant de commande installe hello dernière extension HpcVMDrivers de version 1.1 sur une machine virtuelle existante prenant en charge RDMA nommée *myVM* déployé dans un groupe de ressources hello nommé *myResourceGroup* Bonjour  *Ouest des États-Unis* région :</span><span class="sxs-lookup"><span data-stu-id="c4af9-121">hello following command installs hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in hello resource group named *myResourceGroup* in hello *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="c4af9-122">Pour plus d’informations, consultez [Extensions et fonctionnalités de la machine virtuelle](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c4af9-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="c4af9-123">Vous pouvez également travailler avec les extensions pour les ordinateurs virtuels déployés dans hello [modèle de déploiement classique](classic/manage-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="c4af9-123">You can also work with extensions for VMs deployed in hello [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="c4af9-124">Utilisation de HPC Pack</span><span class="sxs-lookup"><span data-stu-id="c4af9-124">Using HPC Pack</span></span>

<span data-ttu-id="c4af9-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuit HPC cluster et le travail de solution de gestion de Microsoft, il est possible de toocreate un cluster de calcul dans les applications MPI de basés sur Windows Azure toorun et d’autres charges de travail HPC.</span><span class="sxs-lookup"><span data-stu-id="c4af9-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toocreate a compute cluster in Azure toorun Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="c4af9-126">HPC Pack 2012 R2 et versions ultérieures incluent un environnement d’exécution pour MS-MPI qui utilise le réseau RDMA Azure hello déployés sur des machines virtuelles prenant en charge RDMA.</span><span class="sxs-lookup"><span data-stu-id="c4af9-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses hello Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="c4af9-127">Autres tailles</span><span class="sxs-lookup"><span data-stu-id="c4af9-127">Other sizes</span></span>
- [<span data-ttu-id="c4af9-128">Usage général</span><span class="sxs-lookup"><span data-stu-id="c4af9-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="c4af9-129">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="c4af9-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="c4af9-130">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="c4af9-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="c4af9-131">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="c4af9-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="c4af9-132">Optimisé pour le GPU</span><span class="sxs-lookup"><span data-stu-id="c4af9-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="c4af9-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c4af9-133">Next steps</span></span>

- <span data-ttu-id="c4af9-134">Pour les instances de calcul intensif hello des listes de contrôle toouse avec HPC Pack sur Windows Server, consultez [configuration d’un cluster Windows RDMA avec des applications MPI HPC Pack toorun](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c4af9-134">For checklists toouse hello compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack toorun MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="c4af9-135">instances de calcul intensif toouse lors de l’exécution des applications MPI avec Azure Batch, consultez [multi-instance utilisez tâches toorun les applications d’Interface MPI (Message Passing) dans Azure Batch](../../batch/batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="c4af9-135">toouse compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="c4af9-136">Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.</span><span class="sxs-lookup"><span data-stu-id="c4af9-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




