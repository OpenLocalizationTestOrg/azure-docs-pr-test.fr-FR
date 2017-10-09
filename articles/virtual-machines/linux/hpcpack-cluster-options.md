---
title: options de cluster HPC Pack aaaLinux dans le cloud de hello | Documents Microsoft
description: "En savoir plus sur les options avec Microsoft HPC Pack toocreate et gérer un Linux intensif cluster (HPC) Bonjour Azure cloud"
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
ms.openlocfilehash: 60d093b466f44a0391815842c421c328e8c7a0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a><span data-ttu-id="ff8b2-103">Des options avec HPC Pack toocreate et de gérer un cluster HPC dans Azure pour les charges de travail Linux</span><span class="sxs-lookup"><span data-stu-id="ff8b2-103">Options with HPC Pack toocreate and manage an HPC cluster in Azure for Linux workloads</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="ff8b2-104">Cet article se concentre sur les options toouse HPC Pack toorun Linux les charges de travail.</span><span class="sxs-lookup"><span data-stu-id="ff8b2-104">This article focuses on options toouse HPC Pack toorun Linux workloads.</span></span> <span data-ttu-id="ff8b2-105">Il existe également des options d’exécution [de charges de travail Windows HPC avec HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff8b2-105">There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="ff8b2-106">Configuration d’un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="ff8b2-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="ff8b2-107">Modèles Azure</span><span class="sxs-lookup"><span data-stu-id="ff8b2-107">Azure templates</span></span>
* <span data-ttu-id="ff8b2-108">(GitHub) [Modèles de cluster HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="ff8b2-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="ff8b2-109">(Place de marché) [Cluster HPC Pack pour les charges de travail Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span><span class="sxs-lookup"><span data-stu-id="ff8b2-109">(Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span></span>
* <span data-ttu-id="ff8b2-110">(Démarrage rapide) [Créer un cluster HPC avec des nœuds de calcul Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span><span class="sxs-lookup"><span data-stu-id="ff8b2-110">(Quickstart) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span></span>

### <a name="powershell-deployment-script"></a><span data-ttu-id="ff8b2-111">Script de déploiement PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff8b2-111">PowerShell deployment script</span></span>
* [<span data-ttu-id="ff8b2-112">Créer un cluster HPC de Linux avec hello script de déploiement IaaS de HPC Pack</span><span class="sxs-lookup"><span data-stu-id="ff8b2-112">Create a Linux HPC cluster with hello HPC Pack IaaS deployment script</span></span>](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="ff8b2-113">Didacticiels</span><span class="sxs-lookup"><span data-stu-id="ff8b2-113">Tutorials</span></span>
* [<span data-ttu-id="ff8b2-114">Didacticiel : Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="ff8b2-114">Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="ff8b2-115">Didacticiel : Exécution de NAMD avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="ff8b2-115">Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="ff8b2-116">Didacticiel : Exécuter OpenFOAM avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure</span><span class="sxs-lookup"><span data-stu-id="ff8b2-116">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="ff8b2-117">Didacticiel : Exécuter STAR-CCM+ avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure</span><span class="sxs-lookup"><span data-stu-id="ff8b2-117">Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="ff8b2-118">Gestion de cluster</span><span class="sxs-lookup"><span data-stu-id="ff8b2-118">Cluster management</span></span>
* [<span data-ttu-id="ff8b2-119">Envoyer un cluster HPC Pack travaux tooan dans Azure</span><span class="sxs-lookup"><span data-stu-id="ff8b2-119">Submit jobs tooan HPC Pack cluster in Azure</span></span>](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="ff8b2-120">Gestion des travaux dans HPC Pack</span><span class="sxs-lookup"><span data-stu-id="ff8b2-120">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="ff8b2-121">Créer des clusters RDMA pour des charges de travail MPI</span><span class="sxs-lookup"><span data-stu-id="ff8b2-121">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="ff8b2-122">Didacticiel : Exécuter OpenFOAM avec Microsoft HPC Pack sur un cluster Linux RDMA dans Azure</span><span class="sxs-lookup"><span data-stu-id="ff8b2-122">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="ff8b2-123">Configurer une application MPI de Linux RDMA cluster toorun</span><span class="sxs-lookup"><span data-stu-id="ff8b2-123">Set up a Linux RDMA cluster toorun MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

