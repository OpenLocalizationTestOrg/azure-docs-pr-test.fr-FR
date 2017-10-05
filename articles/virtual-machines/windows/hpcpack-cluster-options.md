---
title: Options de cluster Windows HPC Pack dans le cloud | Microsoft Docs
description: "Découvrez les options de Microsoft HPC Pack pour créer et gérer un cluster HPC (High Performance Computing) Windows dans le cloud Azure"
services: virtual-machines-windows,cloud-services,batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 96a5520d8440af7d8a880c2675a5d4eb4121e9ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="options-with-hpc-pack-to-create-and-manage-a-windows-hpc-cluster-in-azure"></a><span data-ttu-id="aee33-103">Options HPC Pack pour créer et gérer un cluster HPC (calcul haute performance) Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="aee33-103">Options with HPC Pack to create and manage a Windows HPC cluster in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="aee33-104">Cet article traite des options de création de clusters HPC Pack pour exécuter des charges de travail Windows.</span><span class="sxs-lookup"><span data-stu-id="aee33-104">This article focuses on options to create HPC Pack clusters to run Windows workloads.</span></span> <span data-ttu-id="aee33-105">Il existe également des options de création de clusters HPC Pack pour l’exécution de [charges de travail HPC Linux](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aee33-105">There are also options for creating HPC Pack clusters to run [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="aee33-106">Configuration d’un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="aee33-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="aee33-107">Modèles Azure</span><span class="sxs-lookup"><span data-stu-id="aee33-107">Azure templates</span></span>
* <span data-ttu-id="aee33-108">(GitHub) [Modèles de cluster HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="aee33-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="aee33-109">(Marketplace) [Cluster HPC Pack pour les charges de travail Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span><span class="sxs-lookup"><span data-stu-id="aee33-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span></span>
* <span data-ttu-id="aee33-110">(Marketplace) [Cluster HPC Pack pour les charges de travail Excel](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span><span class="sxs-lookup"><span data-stu-id="aee33-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span></span>
* <span data-ttu-id="aee33-111">(Démarrage rapide) [Création d’un cluster HPC](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="aee33-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="aee33-112">(Démarrage rapide) [Création d’un cluster HPC avec une image de nœud de calcul personnalisée](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="aee33-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="aee33-113">Images d’ordinateur virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="aee33-113">Azure VM images</span></span>
* [<span data-ttu-id="aee33-114">Nœud principal de HPC Pack 2016 sur Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="aee33-114">HPC Pack 2016 head node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="aee33-115">Nœud de calcul de HPC Pack 2016 sur Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="aee33-115">HPC Pack 2016 compute node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="aee33-116">Nœud principal de HPC Pack 2016 sur Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="aee33-116">HPC Pack 2016 head node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="aee33-117">Nœud de calcul de HPC Pack 2016 sur Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="aee33-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="aee33-118">Nœud principal de HPC Pack 2012 R2 sur Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="aee33-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [<span data-ttu-id="aee33-119">Nœud de calcul de HPC Pack 2012 R2 sur Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="aee33-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [<span data-ttu-id="aee33-120">Nœud de calcul de HPC Pack avec Excel sur Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="aee33-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a><span data-ttu-id="aee33-121">Script de déploiement PowerShell</span><span class="sxs-lookup"><span data-stu-id="aee33-121">PowerShell deployment script</span></span>
* [<span data-ttu-id="aee33-122">Créer un cluster HPC avec le script de déploiement HPC Pack IaaS</span><span class="sxs-lookup"><span data-stu-id="aee33-122">Create an HPC cluster with the HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="aee33-123">Didacticiels</span><span class="sxs-lookup"><span data-stu-id="aee33-123">Tutorials</span></span>
* [<span data-ttu-id="aee33-124">Didacticiel : déployer un cluster HPC Pack 2016 dans Azure</span><span class="sxs-lookup"><span data-stu-id="aee33-124">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span></span>](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="aee33-125">Didacticiel : prise en main d’un cluster HPC Pack dans Azure pour exécuter des charges de travail Excel et SOA</span><span class="sxs-lookup"><span data-stu-id="aee33-125">Tutorial: Get started with an HPC Pack cluster in Azure to run Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-the-azure-portal"></a><span data-ttu-id="aee33-126">Déploiement manuel avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="aee33-126">Manual deployment with the Azure portal</span></span>
* [<span data-ttu-id="aee33-127">Configurer le nœud principal d’un cluster HPC Pack dans une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="aee33-127">Set up the head node of an HPC Pack cluster in an Azure VM</span></span>](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="aee33-128">Gestion de cluster</span><span class="sxs-lookup"><span data-stu-id="aee33-128">Cluster management</span></span>
* [<span data-ttu-id="aee33-129">Gérer des nœuds de calcul dans un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="aee33-129">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="aee33-130">Agrandir et réduire les ressources de calcul Azure dans un cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="aee33-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="aee33-131">Envoyer des travaux à un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="aee33-131">Submit jobs to an HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="aee33-132">Gestion des travaux dans HPC Pack</span><span class="sxs-lookup"><span data-stu-id="aee33-132">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)
* [<span data-ttu-id="aee33-133">Gérer un cluster HPC Pack dans Azure avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aee33-133">Manage an HPC Pack cluster in Azure with Azure Active Directory</span></span>](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-to-an-hpc-pack-cluster"></a><span data-ttu-id="aee33-134">Ajouter des nœuds de rôle de travail à un cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="aee33-134">Add worker role nodes to an HPC Pack cluster</span></span>
* [<span data-ttu-id="aee33-135">Intégration à des instances de travail Azure avec HPC Pack</span><span class="sxs-lookup"><span data-stu-id="aee33-135">Burst to Azure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="aee33-136">Didacticiel : configurer un cluster hybride avec HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="aee33-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [<span data-ttu-id="aee33-137">Ajouter des nœuds « en rafale » Azure à un nœud principal HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="aee33-137">Add Azure "burst" nodes to an HPC Pack head node in Azure</span></span>](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a><span data-ttu-id="aee33-138">Bénéficiez d'une intégration avec Azure Batch</span><span class="sxs-lookup"><span data-stu-id="aee33-138">Integrate with Azure Batch</span></span>
* [<span data-ttu-id="aee33-139">Intégration à Azure Batch avec HPC Pack</span><span class="sxs-lookup"><span data-stu-id="aee33-139">Burst to Azure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="aee33-140">Créer des clusters RDMA pour des charges de travail MPI</span><span class="sxs-lookup"><span data-stu-id="aee33-140">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="aee33-141">Configuration d’un cluster Windows RDMA avec HPC Pack pour exécuter des applications MPI</span><span class="sxs-lookup"><span data-stu-id="aee33-141">Set up a Windows RDMA cluster with HPC Pack to run MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

