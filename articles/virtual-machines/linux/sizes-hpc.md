---
title: "tailles d’aaaAzure Linux VM - HPC | Documents Microsoft"
description: "Répertorie les tailles disponibles pour Linux haute performance computing de machines virtuelles dans Azure hello différentes."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 0b02ee592902ff8097a71898faea1ac17a947d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a><span data-ttu-id="3dd1b-103">Tailles de machine virtuelle Linux pour calcul haute performance</span><span class="sxs-lookup"><span data-stu-id="3dd1b-103">High performance compute Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="3dd1b-104">Instances prenant en charge RDMA</span><span class="sxs-lookup"><span data-stu-id="3dd1b-104">RDMA-capable instances</span></span>
<span data-ttu-id="3dd1b-105">Un sous-ensemble des instances de calcul intensif hello (H16r, H16mr, A8 et A9) dotés d’une interface de réseau pour la connectivité d’accès (RDMA) direct à la mémoire à distance.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="3dd1b-106">Cette interface est en plus des tailles de machine virtuelle toohello tooother disponibles de l’interface réseau Azure standard.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="3dd1b-107">Cette interface permet hello prenant en charge RDMA instances toocommunicate sur un réseau InfiniBand, fonctionnant à des vitesses de Verification pour les ordinateurs virtuels H16r et H16mr et taux QDR pour les machines virtuelles A8 et A9.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="3dd1b-108">Ces fonctions RDMA peuvent optimiser les performances des applications MPI (Message Passing Interface) et l’extensibilité de hello.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="3dd1b-109">Voici la configuration requise pour les machines virtuelles Linux prenant en charge RDMA tooaccess hello réseau RDMA Azure :</span><span class="sxs-lookup"><span data-stu-id="3dd1b-109">Following are requirements for RDMA-capable Linux VMs tooaccess hello Azure RDMA network:</span></span>
 
* <span data-ttu-id="3dd1b-110">**Distributions** - vous devez déployer des machines virtuelles à partir de prenant en charge RDMA SUSE Linux Enterprise Server (SLES) ou des images dans HPC de base CentOS les logiciels non autorisés Wave (anciennement OpenLogic) hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-110">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="3dd1b-111">Hello images Marketplace suivantes prennent en charge la connectivité RDMA :</span><span class="sxs-lookup"><span data-stu-id="3dd1b-111">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="3dd1b-112">SLES 12 SP1 pour HPC ou SLES 12 SP1 pour HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="3dd1b-112">SLES 12 SP1 for HPC, or SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="3dd1b-113">HP basé sur CentOS 7.3, HP basé sur CentOS 7.1, HP basé sur CentOS 6.8 ou HP basé sur CentOS 6.5</span><span class="sxs-lookup"><span data-stu-id="3dd1b-113">CentOS-based 7.3 HPC, CentOS-based 7.1 HPC, CentOS-based 6.8 HPC, or CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="3dd1b-114">Pour les machines virtuelles de la série H, nous vous recommandons une image SLES 12 SP1 pour HPC ou une image HPC basée sur CentOS 7.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-114">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 or later HPC image.</span></span>
        >
        > <span data-ttu-id="3dd1b-115">Sur les images de HPC de base CentOS hello, les mises à jour du noyau sont désactivées dans hello **yum** fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-115">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="3dd1b-116">Il s’agit, car les pilotes Linux RDMA hello sont distribuées sous la forme d’un package RPM et mises à jour de pilote peuvent ne pas fonctionnent si le noyau de hello est mise à jour.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-116">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="3dd1b-117">**MPI** - Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="3dd1b-117">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="3dd1b-118">En fonction de l’image de Marketplace hello choisie, installation de licence, distinct, ou la configuration de Intel MPI peut être nécessaire, comme suit :</span><span class="sxs-lookup"><span data-stu-id="3dd1b-118">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="3dd1b-119">**SLES 12 SP1 pour l’image HPC** -les packages Intel MPI sont distribués sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-119">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="3dd1b-120">Installer en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3dd1b-120">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="3dd1b-121">**Images HPC basées sur CentOS** : Intel MPI 5.1 est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-121">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="3dd1b-122">Configuration système supplémentaire est nécessaire toorun des travaux MPI sur des machines virtuelles en cluster.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-122">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="3dd1b-123">Par exemple, sur un cluster de machines virtuelles, vous devez tooestablish approbation hello parmi les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-123">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="3dd1b-124">Pour les paramètres par défaut, consultez [configurer une application MPI de Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3dd1b-124">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

### <a name="network-topology-considerations"></a><span data-ttu-id="3dd1b-125">Considérations sur la topologie réseau</span><span class="sxs-lookup"><span data-stu-id="3dd1b-125">Network topology considerations</span></span>
* <span data-ttu-id="3dd1b-126">Sur des machines virtuelles Linux compatibles RDMA dans Azure, Eth1 est réservé au trafic réseau RDMA.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-126">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="3dd1b-127">Ne modifiez pas les paramètres Eth1 ou toute information dans le fichier de configuration hello faisant référence toothis réseau.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-127">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="3dd1b-128">Eth0 est réservé au trafic réseau Azure normal.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-128">Eth0 is reserved for regular Azure network traffic.</span></span>

* <span data-ttu-id="3dd1b-129">Dans Azure, IP over Infiniband (IB) n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-129">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="3dd1b-130">Seul RDMA over IB est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-130">Only RDMA over IB is supported.</span></span>

## <a name="using-hpc-pack"></a><span data-ttu-id="3dd1b-131">Utilisation de HPC Pack</span><span class="sxs-lookup"><span data-stu-id="3dd1b-131">Using HPC Pack</span></span>
<span data-ttu-id="3dd1b-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuit HPC cluster et le travail de solution de gestion de Microsoft, est une option pour vous, les instances de calcul intensif hello toouse avec Linux.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="3dd1b-133">Hello dernières versions de HPC Pack prend en charge plusieurs distributions Linux toorun sur nœuds déployés dans des machines virtuelles de Azure, gérés par un nœud principal de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-133">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="3dd1b-134">Avec les nœuds de calcul Linux prenant en charge RDMA Intel MPI en cours d’exécution, HPC Pack peut planifier et exécuter des applications Linux MPI réseau RDMA accès hello.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-134">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="3dd1b-135">Consultez [Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3dd1b-135">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="other-sizes"></a><span data-ttu-id="3dd1b-136">Autres tailles</span><span class="sxs-lookup"><span data-stu-id="3dd1b-136">Other sizes</span></span>
- [<span data-ttu-id="3dd1b-137">Usage général</span><span class="sxs-lookup"><span data-stu-id="3dd1b-137">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="3dd1b-138">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="3dd1b-138">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="3dd1b-139">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="3dd1b-139">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="3dd1b-140">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="3dd1b-140">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="3dd1b-141">GPU</span><span class="sxs-lookup"><span data-stu-id="3dd1b-141">GPU</span></span>](../windows/sizes-gpu.md)


## <a name="next-steps"></a><span data-ttu-id="3dd1b-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3dd1b-142">Next steps</span></span>

- <span data-ttu-id="3dd1b-143">tooget a démarré le déploiement et l’utilisation de tailles de calcul intensif avec le RDMA sur Linux, consultez [configurer une application MPI de Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3dd1b-143">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="3dd1b-144">Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.</span><span class="sxs-lookup"><span data-stu-id="3dd1b-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




