---
title: aaaAbout de calcul intensif machines virtuelles avec Linux | Documents Microsoft
description: "Obtenir des informations générales et les considérations sur l’utilisation de tailles de calcul intensif H-series et A8, A9, A10 et A11 hello pour les machines virtuelles Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 16cf6e2d-f401-4b22-af8c-9a337179f5f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 37636840a3f809ac19354a5a7993257216f675f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a><span data-ttu-id="236ab-103">About H-series and compute-intensive A-series VMs for Linux (À propos des machines virtuelles de série H ou de calcul intensif de série A pour Linux)</span><span class="sxs-lookup"><span data-stu-id="236ab-103">About H-series and compute-intensive A-series VMs for Linux</span></span>
<span data-ttu-id="236ab-104">Ici des informations générales et des considérations relatives à l’aide de hello plus récente de Azure H-series hello antérieures tailles A8, A9, A10 et A11, également appelé *intensives* instances.</span><span class="sxs-lookup"><span data-stu-id="236ab-104">Here is background information and some considerations for using hello newer Azure H-series and hello earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="236ab-105">Cet article se concentre sur l’utilisation de ces tailles pour les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="236ab-105">This article focuses on using these sizes for Linux VMs.</span></span> <span data-ttu-id="236ab-106">Vous pouvez également les utiliser pour des [machines virtuelles Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="236ab-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="236ab-107">Pour plus d’informations sur les spécifications de base, les capacités de stockage et les disques, consultez l’article [Tailles de machines virtuelles](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="236ab-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a><span data-ttu-id="236ab-108">Accéder à toohello réseau RDMA</span><span class="sxs-lookup"><span data-stu-id="236ab-108">Access toohello RDMA network</span></span>
<span data-ttu-id="236ab-109">Vous pouvez créer des clusters d’ordinateurs virtuels Linux prenant en charge RDMA qui exécutent une Hello suivant des distributions Linux HPC prises en charge et un avantage de tootake implémentation MPI prise en charge du réseau RDMA Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="236ab-109">You can create clusters of RDMA-capable Linux VMs that run one of hello following supported Linux HPC distributions and a supported MPI implementation tootake advantage of hello Azure RDMA network.</span></span> <span data-ttu-id="236ab-110">Consultez [configurer une application MPI de Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) pour les options de déploiement et les étapes de configuration d’exemple.</span><span class="sxs-lookup"><span data-stu-id="236ab-110">See [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span></span>

* <span data-ttu-id="236ab-111">**Distributions** - vous devez déployer des machines virtuelles à partir de prenant en charge RDMA SUSE Linux Enterprise Server (SLES) ou des images dans HPC de base CentOS les logiciels non autorisés Wave (anciennement OpenLogic) hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="236ab-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="236ab-112">Hello images Marketplace suivantes prennent en charge la connectivité RDMA :</span><span class="sxs-lookup"><span data-stu-id="236ab-112">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="236ab-113">SLES 12 SP1 pour HPC, SLES 12 SP1 pour HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="236ab-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="236ab-114">HPC basé sur CentOS 7.1, HPC basé sur CentOS 6.5</span><span class="sxs-lookup"><span data-stu-id="236ab-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="236ab-115">Pour les machines virtuelles de la série H, nous vous recommandons une image SLES 12 SP1 pour HPC ou une image HPC basée sur CentOS 7.1.</span><span class="sxs-lookup"><span data-stu-id="236ab-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span></span>
        >
        > <span data-ttu-id="236ab-116">Sur les images de HPC de base CentOS hello, les mises à jour du noyau sont désactivées dans hello **yum** fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="236ab-116">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="236ab-117">Il s’agit, car les pilotes Linux RDMA hello sont distribuées sous la forme d’un package RPM et mises à jour de pilote peuvent ne pas fonctionnent si le noyau de hello est mise à jour.</span><span class="sxs-lookup"><span data-stu-id="236ab-117">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="236ab-118">**MPI** - Intel MPI Library 5.x</span><span class="sxs-lookup"><span data-stu-id="236ab-118">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="236ab-119">En fonction de l’image de Marketplace hello choisie, installation de licence, distinct, ou la configuration de Intel MPI peut être nécessaire, comme suit :</span><span class="sxs-lookup"><span data-stu-id="236ab-119">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="236ab-120">**SLES 12 SP1 pour l’image HPC** -les packages Intel MPI sont distribués sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="236ab-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="236ab-121">Installer en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="236ab-121">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="236ab-122">**Images HPC basées sur CentOS** : Intel MPI 5.1 est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="236ab-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="236ab-123">Configuration système supplémentaire est nécessaire toorun des travaux MPI sur des machines virtuelles en cluster.</span><span class="sxs-lookup"><span data-stu-id="236ab-123">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="236ab-124">Par exemple, sur un cluster de machines virtuelles, vous devez tooestablish approbation hello parmi les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="236ab-124">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="236ab-125">Pour les paramètres par défaut, consultez [configurer une application MPI de Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="236ab-125">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="considerations-for-hpc-pack-and-linux"></a><span data-ttu-id="236ab-126">Considérations relatives à HPC Pack et Linux</span><span class="sxs-lookup"><span data-stu-id="236ab-126">Considerations for HPC Pack and Linux</span></span>
<span data-ttu-id="236ab-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuit HPC cluster et le travail de solution de gestion de Microsoft, fournit une option pour vous instances de calcul intensif hello toouse avec Linux.</span><span class="sxs-lookup"><span data-stu-id="236ab-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="236ab-128">Hello dernières versions de HPC Pack prend en charge plusieurs distributions Linux toorun sur nœuds déployés dans des machines virtuelles de Azure, gérés par un nœud principal de Windows Server.</span><span class="sxs-lookup"><span data-stu-id="236ab-128">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="236ab-129">Avec les nœuds de calcul Linux prenant en charge RDMA Intel MPI en cours d’exécution, HPC Pack peut planifier et exécuter des applications Linux MPI réseau RDMA accès hello.</span><span class="sxs-lookup"><span data-stu-id="236ab-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="236ab-130">tooget démarré, consultez [prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="236ab-130">tooget started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="network-topology-considerations"></a><span data-ttu-id="236ab-131">Considérations sur la topologie réseau</span><span class="sxs-lookup"><span data-stu-id="236ab-131">Network topology considerations</span></span>
* <span data-ttu-id="236ab-132">Sur des machines virtuelles Linux compatibles RDMA dans Azure, Eth1 est réservé au trafic réseau RDMA.</span><span class="sxs-lookup"><span data-stu-id="236ab-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="236ab-133">Ne modifiez pas les paramètres Eth1 ou toute information dans le fichier de configuration hello faisant référence toothis réseau.</span><span class="sxs-lookup"><span data-stu-id="236ab-133">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="236ab-134">Eth0 est réservé au trafic réseau Azure normal.</span><span class="sxs-lookup"><span data-stu-id="236ab-134">Eth0 is reserved for regular Azure network traffic.</span></span>
* <span data-ttu-id="236ab-135">Dans Azure, IP over Infiniband (IB) n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="236ab-135">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="236ab-136">Seul RDMA over IB est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="236ab-136">Only RDMA over IB is supported.</span></span>



## <a name="next-steps"></a><span data-ttu-id="236ab-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="236ab-137">Next steps</span></span>
* <span data-ttu-id="236ab-138">Pour plus d’informations sur la disponibilité et la tarification des tailles de calcul intensif hello, consultez [Machines virtuelles tarification](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="236ab-138">For details about availability and pricing of hello compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span>
* <span data-ttu-id="236ab-139">Pour plus d’informations sur les capacités de stockage et sur les disques, consultez [Tailles de machines virtuelles](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="236ab-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="236ab-140">tooget a démarré le déploiement et l’utilisation de tailles de calcul intensif avec le RDMA sur Linux, consultez [configurer une application MPI de Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="236ab-140">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

