---
title: Tailles des machines virtuelles Windows Azure - HPC | Microsoft Docs
description: "Répertorie les différentes tailles disponibles pour les machines virtuelles de calcul haute performance Windows dans Azure."
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
ms.openlocfilehash: a0596d134e9c26877848f93d72f35bfd2c957570
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="79700-103">Tailles de machines virtuelles de calcul haute performance</span><span class="sxs-lookup"><span data-stu-id="79700-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="79700-104">Instances prenant en charge RDMA</span><span class="sxs-lookup"><span data-stu-id="79700-104">RDMA-capable instances</span></span>
<span data-ttu-id="79700-105">Un sous-ensemble d’instances nécessitant beaucoup de ressources système (H16r, H16mr, A8 et A9) offre une interface réseau pour la connectivité par accès direct à la mémoire à distance (RDMA).</span><span class="sxs-lookup"><span data-stu-id="79700-105">A subset of the compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="79700-106">Cette interface s’ajoute à l’interface réseau Azure standard disponible pour d’autres tailles de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="79700-106">This interface is in addition to the standard Azure network interface available to other VM sizes.</span></span> 
  
<span data-ttu-id="79700-107">Cette interface permet aux instances prenant en charge RDMA de communiquer sur un réseau InfiniBand, opérant à des vitesses FDR pour les machines virtuelles H16r et H16mr, et à des vitesses QDR pour les machines virtuelles A8 et A9.</span><span class="sxs-lookup"><span data-stu-id="79700-107">This interface allows the RDMA-capable instances to communicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="79700-108">Ces fonctionnalités RDMA peuvent améliorer l’extensibilité et les performances des applications MPI (Message Passing Interface).</span><span class="sxs-lookup"><span data-stu-id="79700-108">These RDMA capabilities can boost the scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="79700-109">Voici la configuration requise pour que les machines virtuelles Windows prenant en charge RDMA puissent accéder au réseau RDMA Azure :</span><span class="sxs-lookup"><span data-stu-id="79700-109">Following are requirements for RDMA-capable Windows VMs to access the Azure RDMA network:</span></span> 

* <span data-ttu-id="79700-110">**Système d’exploitation**</span><span class="sxs-lookup"><span data-stu-id="79700-110">**Operating system**</span></span>
  
  <span data-ttu-id="79700-111">Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="79700-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="79700-112">Actuellement, Windows Server 2016 ne prend pas en charge la connectivité RDMA dans Azure.</span><span class="sxs-lookup"><span data-stu-id="79700-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="79700-113">**Groupe à haute disponibilité ou service cloud** : déployez les machines virtuelles prenant en charge RDMA dans le même groupe à haute disponibilité (si vous utilisez le modèle de déploiement Azure Resource Manager) ou le même service cloud (si vous utilisez le modèle de déploiement Classic).</span><span class="sxs-lookup"><span data-stu-id="79700-113">**Availability set or cloud service** – Deploy the RDMA-capable VMs in the same availability set (when you use the Azure Resource Manager deployment model) or the same cloud service (when you use the classic deployment model).</span></span> <span data-ttu-id="79700-114">Si vous utilisez Azure Batch, les machines virtuelles prenant en charge RDMA doivent être dans le même pool.</span><span class="sxs-lookup"><span data-stu-id="79700-114">If you use Azure Batch, the RDMA-capable VMs must be in the same pool.</span></span>

* <span data-ttu-id="79700-115">**MPI** : Microsoft MPI (MS-MPI) 2012 R2 ou version ultérieure, bibliothèque Intel MPI 5.x</span><span class="sxs-lookup"><span data-stu-id="79700-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="79700-116">Les implémentations MPI prises en charge utilisent l’interface Microsoft Network Direct pour la communication entre les instances.</span><span class="sxs-lookup"><span data-stu-id="79700-116">Supported MPI implementations use the Microsoft Network Direct interface to communicate between instances.</span></span> 

* <span data-ttu-id="79700-117">**Espace d’adressage réseau RDMA** : le réseau RDMA dans Azure réserve l’espace d’adressage 172.16.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="79700-117">**RDMA network address space** - The RDMA network in Azure reserves the address space 172.16.0.0/16.</span></span> <span data-ttu-id="79700-118">Si vous exécutez des applications MPI sur des instances déployées dans un réseau virtuel Azure, assurez-vous que l’espace d’adressage du réseau virtuel ne chevauche pas le réseau RDMA.</span><span class="sxs-lookup"><span data-stu-id="79700-118">To run MPI applications on instances deployed in an Azure virtual network, make sure that the virtual network address space does not overlap the RDMA network.</span></span>

* <span data-ttu-id="79700-119">**Extension de machine virtuelle HpcVmDrivers** : sur des machines virtuelles prenant en charge RDMA, vous devez ajouter l’extension HpcVmDrivers pour installer les pilotes d’appareils réseau Windows nécessaires à la connectivité RDMA.</span><span class="sxs-lookup"><span data-stu-id="79700-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add the HpcVmDrivers extension to install Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="79700-120">(Dans certains déploiements des instances A8 et A9, l’extension HpcVmDrivers est ajoutée automatiquement.) Pour ajouter l’extension de machine virtuelle sur une machine virtuelle, vous pouvez utiliser les cmdlets [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="79700-120">(In certain deployments of A8 and A9 instances, the HpcVmDrivers extension is added automatically.) To add the VM extension to a VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="79700-121">La commande suivante installe la dernière version 1.1 de l’extension HpcVMDrivers sur une machine virtuelle existante prenant en charge RDMA et nommée *myVM* déployée dans le groupe de ressources nommé *myResourceGroup* dans la région *Ouest des États-Unis* :</span><span class="sxs-lookup"><span data-stu-id="79700-121">The following command installs the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in the resource group named *myResourceGroup* in the *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="79700-122">Pour plus d’informations, consultez [Extensions et fonctionnalités de la machine virtuelle](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="79700-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="79700-123">Vous pouvez également utiliser les extensions pour les machines virtuelles déployées dans le [modèle de déploiement classique](classic/manage-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="79700-123">You can also work with extensions for VMs deployed in the [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="79700-124">Utilisation de HPC Pack</span><span class="sxs-lookup"><span data-stu-id="79700-124">Using HPC Pack</span></span>

<span data-ttu-id="79700-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), solution gratuite de gestion des travaux et des clusters HPC de Microsoft, vous offre un moyen de créer un cluster de calcul dans Azure pour exécuter des applications MPI basées sur Windows et d’autres charges de travail HPC.</span><span class="sxs-lookup"><span data-stu-id="79700-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you to create a compute cluster in Azure to run Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="79700-126">HPC Pack 2012 R2 et les versions ultérieures incluent un environnement d’exécution pour MS-MPI qui utilise le réseau RDMA Azure en cas de déploiement sur des machines virtuelles prenant en charge RDMA.</span><span class="sxs-lookup"><span data-stu-id="79700-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses the Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="79700-127">Autres tailles</span><span class="sxs-lookup"><span data-stu-id="79700-127">Other sizes</span></span>
- [<span data-ttu-id="79700-128">Usage général</span><span class="sxs-lookup"><span data-stu-id="79700-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="79700-129">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="79700-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="79700-130">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="79700-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="79700-131">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="79700-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="79700-132">Optimisé pour le GPU</span><span class="sxs-lookup"><span data-stu-id="79700-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="79700-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="79700-133">Next steps</span></span>

- <span data-ttu-id="79700-134">Pour obtenir les listes de vérification à mettre en œuvre afin d’utiliser les instances nécessitant beaucoup de ressources système avec HPC Pack sur Windows Server, consultez [Configuration d’un cluster RDMA Windows avec HPC Pack pour exécuter des applications MPI](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="79700-134">For checklists to use the compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack to run MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="79700-135">Pour utiliser des instances nécessitant beaucoup de ressources système lors de l’exécution d’applications MPI avec Azure Batch, consultez [Utiliser les tâches multi-instances pour exécuter des applications MPI (Message Passing Interface) dans Azure Batch](../../batch/batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="79700-135">To use compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks to run Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="79700-136">Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.</span><span class="sxs-lookup"><span data-stu-id="79700-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




