---
title: Options de cluster HPC Pack Linux dans le cloud | Microsoft Docs
description: "Découvrez les options de Microsoft HPC Pack pour créer et gérer un cluster HPC (High Performance Computing) Linux dans le cloud Azure"
services: virtual-machines-linux,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 616006d29149f7f47b03bd127cf3c83ad63a5c39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="options-with-hpc-pack-to-create-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a><span data-ttu-id="7f227-103">Options de HPC Pack pour créer et gérer un cluster HPC dans Azure pour des charges de travail Linux</span><span class="sxs-lookup"><span data-stu-id="7f227-103">Options with HPC Pack to create and manage an HPC cluster in Azure for Linux workloads</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="7f227-104">Cet article traite des options d’utilisation de HPC Pack pour exécuter des charges de travail Linux.</span><span class="sxs-lookup"><span data-stu-id="7f227-104">This article focuses on options to use HPC Pack to run Linux workloads.</span></span> <span data-ttu-id="7f227-105">Il existe également des options d’exécution [de charges de travail Windows HPC avec HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7f227-105">There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="7f227-106">Configuration d’un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="7f227-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="7f227-107">Modèles Azure</span><span class="sxs-lookup"><span data-stu-id="7f227-107">Azure templates</span></span>
* <span data-ttu-id="7f227-108">(GitHub) [Modèles de cluster HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="7f227-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="7f227-109">(Place de marché) [Cluster HPC Pack pour les charges de travail Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span><span class="sxs-lookup"><span data-stu-id="7f227-109">(Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span></span>
* <span data-ttu-id="7f227-110">(Démarrage rapide) [Créer un cluster HPC avec des nœuds de calcul Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span><span class="sxs-lookup"><span data-stu-id="7f227-110">(Quickstart) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span></span>

### <a name="powershell-deployment-script"></a><span data-ttu-id="7f227-111">Script de déploiement PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f227-111">PowerShell deployment script</span></span>
* [<span data-ttu-id="7f227-112">Créer un cluster HPC Linux avec le script de déploiement HPC Pack IaaS</span><span class="sxs-lookup"><span data-stu-id="7f227-112">Create a Linux HPC cluster with the HPC Pack IaaS deployment script</span></span>](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="7f227-113">Didacticiels</span><span class="sxs-lookup"><span data-stu-id="7f227-113">Tutorials</span></span>
* [<span data-ttu-id="7f227-114">Didacticiel : Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="7f227-114">Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="7f227-115">Didacticiel : Exécution de NAMD avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="7f227-115">Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="7f227-116">Didacticiel : Exécuter OpenFOAM avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure</span><span class="sxs-lookup"><span data-stu-id="7f227-116">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="7f227-117">Didacticiel : Exécuter STAR-CCM+ avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure</span><span class="sxs-lookup"><span data-stu-id="7f227-117">Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="7f227-118">Gestion de cluster</span><span class="sxs-lookup"><span data-stu-id="7f227-118">Cluster management</span></span>
* [<span data-ttu-id="7f227-119">Envoyer des travaux à un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="7f227-119">Submit jobs to an HPC Pack cluster in Azure</span></span>](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="7f227-120">Gestion des travaux dans HPC Pack</span><span class="sxs-lookup"><span data-stu-id="7f227-120">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="7f227-121">Créer des clusters RDMA pour des charges de travail MPI</span><span class="sxs-lookup"><span data-stu-id="7f227-121">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="7f227-122">Didacticiel : Exécuter OpenFOAM avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure</span><span class="sxs-lookup"><span data-stu-id="7f227-122">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="7f227-123">Configuration d’un cluster Linux RDMA pour exécuter des applications MPI</span><span class="sxs-lookup"><span data-stu-id="7f227-123">Set up a Linux RDMA cluster to run MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

