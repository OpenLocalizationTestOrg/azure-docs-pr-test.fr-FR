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
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a>Des options avec HPC Pack toocreate et gérer un cluster Windows HPC dans Azure
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

Cet article concentre sur les options toocreate HPC Pack clusters Windows toorun des charges de travail. Il existe également des options pour les clusters de création HPC Pack toorun [les charges de travail Linux HPC](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>Configuration d’un cluster HPC Pack dans Azure
### <a name="azure-templates"></a>Modèles Azure
* (GitHub) [Modèles de cluster HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016)
* (Marketplace) [Cluster HPC Pack pour les charges de travail Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)
* (Marketplace) [Cluster HPC Pack pour les charges de travail Excel](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)
* (Démarrage rapide) [Création d’un cluster HPC](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)
* (Démarrage rapide) [Création d’un cluster HPC avec une image de nœud de calcul personnalisée](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)

### <a name="azure-vm-images"></a>Images d’ordinateur virtuel Azure
* [Nœud principal de HPC Pack 2016 sur Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [Nœud de calcul de HPC Pack 2016 sur Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [Nœud principal de HPC Pack 2016 sur Windows Server 2012 R2](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [Nœud de calcul de HPC Pack 2016 sur Windows Server 2012 R2](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [Nœud principal de HPC Pack 2012 R2 sur Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [Nœud de calcul de HPC Pack 2012 R2 sur Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [Nœud de calcul de HPC Pack avec Excel sur Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a>Script de déploiement PowerShell
* [Créer un cluster HPC avec hello script de déploiement IaaS de HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a>Didacticiels
* [Didacticiel : déployer un cluster HPC Pack 2016 dans Azure](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Didacticiel : Prise en main avec un cluster HPC Pack dans Azure toorun Excel et les charges de travail SOA](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a>Déploiement manuel avec hello portail Azure
* [Configurer le nœud principal de hello d’un cluster HPC Pack dans une machine virtuelle Azure](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a>Gestion de cluster
* [Gérer des nœuds de calcul dans un cluster HPC Pack dans Azure](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Agrandir et réduire les ressources de calcul Azure dans un cluster HPC Pack](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Envoyer un cluster HPC Pack travaux tooan dans Azure](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Gestion des travaux dans HPC Pack](https://technet.microsoft.com/library/jj899585.aspx)
* [Gérer un cluster HPC Pack dans Azure avec Azure Active Directory](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a>Ajouter le cluster HPC Pack tooan travail rôle nœuds
* [Croissance des instances de travail tooAzure avec HPC Pack](https://technet.microsoft.com/library/gg481749.aspx)
* [Didacticiel : configurer un cluster hybride avec HPC Pack dans Azure](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [Ajouter Azure « de « croissance nœuds tooan nœud principal HPC Pack dans Azure](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a>Bénéficiez d'une intégration avec Azure Batch
* [Croissance tooAzure lot avec HPC Pack](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>Créer des clusters RDMA pour des charges de travail MPI
* [Configuration d’un cluster Windows RDMA avec des applications MPI HPC Pack toorun](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

