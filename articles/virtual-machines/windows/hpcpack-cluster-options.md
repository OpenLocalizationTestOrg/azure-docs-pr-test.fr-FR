---
title: options de cloud de hello du cluster aaaWindows HPC Pack | Documents Microsoft
description: "En savoir plus sur les options avec Microsoft HPC Pack toocreate et gérer un Windows informatiques hautes performances cluster (HPC) Bonjour Azure cloud"
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
ms.openlocfilehash: 6158d9dd0cecda38b14f85a2b2080163f18e8cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a><span data-ttu-id="2704f-103">Des options avec HPC Pack toocreate et gérer un cluster Windows HPC dans Azure</span><span class="sxs-lookup"><span data-stu-id="2704f-103">Options with HPC Pack toocreate and manage a Windows HPC cluster in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="2704f-104">Cet article concentre sur les options toocreate HPC Pack clusters Windows toorun des charges de travail.</span><span class="sxs-lookup"><span data-stu-id="2704f-104">This article focuses on options toocreate HPC Pack clusters toorun Windows workloads.</span></span> <span data-ttu-id="2704f-105">Il existe également des options pour les clusters de création HPC Pack toorun [les charges de travail Linux HPC](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2704f-105">There are also options for creating HPC Pack clusters toorun [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="2704f-106">Configuration d’un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="2704f-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="2704f-107">Modèles Azure</span><span class="sxs-lookup"><span data-stu-id="2704f-107">Azure templates</span></span>
* <span data-ttu-id="2704f-108">(GitHub) [Modèles de cluster HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="2704f-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="2704f-109">(Marketplace) [Cluster HPC Pack pour les charges de travail Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span><span class="sxs-lookup"><span data-stu-id="2704f-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span></span>
* <span data-ttu-id="2704f-110">(Marketplace) [Cluster HPC Pack pour les charges de travail Excel](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span><span class="sxs-lookup"><span data-stu-id="2704f-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span></span>
* <span data-ttu-id="2704f-111">(Démarrage rapide) [Création d’un cluster HPC](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="2704f-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="2704f-112">(Démarrage rapide) [Création d’un cluster HPC avec une image de nœud de calcul personnalisée](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="2704f-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="2704f-113">Images d’ordinateur virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="2704f-113">Azure VM images</span></span>
* [<span data-ttu-id="2704f-114">Nœud principal de HPC Pack 2016 sur Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2704f-114">HPC Pack 2016 head node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="2704f-115">Nœud de calcul de HPC Pack 2016 sur Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2704f-115">HPC Pack 2016 compute node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="2704f-116">Nœud principal de HPC Pack 2016 sur Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="2704f-116">HPC Pack 2016 head node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="2704f-117">Nœud de calcul de HPC Pack 2016 sur Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="2704f-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="2704f-118">Nœud principal de HPC Pack 2012 R2 sur Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="2704f-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [<span data-ttu-id="2704f-119">Nœud de calcul de HPC Pack 2012 R2 sur Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="2704f-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [<span data-ttu-id="2704f-120">Nœud de calcul de HPC Pack avec Excel sur Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="2704f-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a><span data-ttu-id="2704f-121">Script de déploiement PowerShell</span><span class="sxs-lookup"><span data-stu-id="2704f-121">PowerShell deployment script</span></span>
* [<span data-ttu-id="2704f-122">Créer un cluster HPC avec hello script de déploiement IaaS de HPC Pack</span><span class="sxs-lookup"><span data-stu-id="2704f-122">Create an HPC cluster with hello HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="2704f-123">Didacticiels</span><span class="sxs-lookup"><span data-stu-id="2704f-123">Tutorials</span></span>
* [<span data-ttu-id="2704f-124">Didacticiel : déployer un cluster HPC Pack 2016 dans Azure</span><span class="sxs-lookup"><span data-stu-id="2704f-124">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span></span>](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2704f-125">Didacticiel : Prise en main avec un cluster HPC Pack dans Azure toorun Excel et les charges de travail SOA</span><span class="sxs-lookup"><span data-stu-id="2704f-125">Tutorial: Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a><span data-ttu-id="2704f-126">Déploiement manuel avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="2704f-126">Manual deployment with hello Azure portal</span></span>
* [<span data-ttu-id="2704f-127">Configurer le nœud principal de hello d’un cluster HPC Pack dans une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="2704f-127">Set up hello head node of an HPC Pack cluster in an Azure VM</span></span>](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="2704f-128">Gestion de cluster</span><span class="sxs-lookup"><span data-stu-id="2704f-128">Cluster management</span></span>
* [<span data-ttu-id="2704f-129">Gérer des nœuds de calcul dans un cluster HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="2704f-129">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="2704f-130">Agrandir et réduire les ressources de calcul Azure dans un cluster HPC Pack</span><span class="sxs-lookup"><span data-stu-id="2704f-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="2704f-131">Envoyer un cluster HPC Pack travaux tooan dans Azure</span><span class="sxs-lookup"><span data-stu-id="2704f-131">Submit jobs tooan HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2704f-132">Gestion des travaux dans HPC Pack</span><span class="sxs-lookup"><span data-stu-id="2704f-132">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)
* [<span data-ttu-id="2704f-133">Gérer un cluster HPC Pack dans Azure avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2704f-133">Manage an HPC Pack cluster in Azure with Azure Active Directory</span></span>](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a><span data-ttu-id="2704f-134">Ajouter le cluster HPC Pack tooan travail rôle nœuds</span><span class="sxs-lookup"><span data-stu-id="2704f-134">Add worker role nodes tooan HPC Pack cluster</span></span>
* [<span data-ttu-id="2704f-135">Croissance des instances de travail tooAzure avec HPC Pack</span><span class="sxs-lookup"><span data-stu-id="2704f-135">Burst tooAzure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="2704f-136">Didacticiel : configurer un cluster hybride avec HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="2704f-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [<span data-ttu-id="2704f-137">Ajouter Azure « de « croissance nœuds tooan nœud principal HPC Pack dans Azure</span><span class="sxs-lookup"><span data-stu-id="2704f-137">Add Azure "burst" nodes tooan HPC Pack head node in Azure</span></span>](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a><span data-ttu-id="2704f-138">Bénéficiez d'une intégration avec Azure Batch</span><span class="sxs-lookup"><span data-stu-id="2704f-138">Integrate with Azure Batch</span></span>
* [<span data-ttu-id="2704f-139">Croissance tooAzure lot avec HPC Pack</span><span class="sxs-lookup"><span data-stu-id="2704f-139">Burst tooAzure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="2704f-140">Créer des clusters RDMA pour des charges de travail MPI</span><span class="sxs-lookup"><span data-stu-id="2704f-140">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="2704f-141">Configuration d’un cluster Windows RDMA avec des applications MPI HPC Pack toorun</span><span class="sxs-lookup"><span data-stu-id="2704f-141">Set up a Windows RDMA cluster with HPC Pack toorun MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

