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
# <a name="high-performance-compute-vm-sizes"></a>Tailles de machines virtuelles de calcul haute performance

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>Instances prenant en charge RDMA
Un sous-ensemble des instances de calcul intensif hello (H16r, H16mr, A8 et A9) dotés d’une interface de réseau pour la connectivité d’accès (RDMA) direct à la mémoire à distance. Cette interface est en plus des tailles de machine virtuelle toohello tooother disponibles de l’interface réseau Azure standard. 
  
Cette interface permet hello prenant en charge RDMA instances toocommunicate sur un réseau InfiniBand, fonctionnant à des vitesses de Verification pour les ordinateurs virtuels H16r et H16mr et taux QDR pour les machines virtuelles A8 et A9. Ces fonctions RDMA peuvent optimiser les performances des applications MPI (Message Passing Interface) et l’extensibilité de hello.

Voici la configuration requise pour les machines virtuelles Windows prenant en charge RDMA tooaccess hello réseau RDMA Azure : 

* **Système d’exploitation**
  
  Windows Server 2012 R2, Windows Server 2012
  
  > [!NOTE]
  > Actuellement, Windows Server 2016 ne prend pas en charge la connectivité RDMA dans Azure.
  >

* **Disponibilité ou de service de cloud computing** : déployer des machines virtuelles hello prenant en charge RDMA dans hello même groupe à haute disponibilité (lorsque vous utilisez le modèle de déploiement du Gestionnaire de ressources Azure hello) ou hello même service cloud (lorsque vous utilisez le modèle de déploiement classique hello). Si vous utilisez Azure Batch, hello prenant en charge RDMA machines virtuelles doit être Bonjour même pool.

* **MPI** : Microsoft MPI (MS-MPI) 2012 R2 ou version ultérieure, bibliothèque Intel MPI 5.x

  Implémentations MPI prises en charge utilisent hello toocommunicate d’interface Microsoft Network Direct entre des instances. 

* **Espace d’adressage réseau RDMA** -réseau RDMA de hello dans Azure réserve hello adresse espace 172.16.0.0/16. toorun des applications MPI sur des instances déployées dans un réseau virtuel Azure, assurez-vous qu’espace d’adressage de réseau virtuel de hello ne chevauche pas le réseau RDMA de hello.

* **Extension HpcVmDrivers VM** -sur les ordinateurs virtuels prenant en charge RDMA, vous devez ajouter hello HpcVmDrivers extension tooinstall Windows pilotes de périphérique réseau pour la connectivité RDMA. (Dans certains déploiements des instances A8 et A9, hello extension HpcVmDrivers est ajouté automatiquement.) tooadd hello VM extension tooa machine virtuelle, vous pouvez utiliser [Azure PowerShell](/powershell/azure/overview) applets de commande. 

  
  Hello suivant de commande installe hello dernière extension HpcVMDrivers de version 1.1 sur une machine virtuelle existante prenant en charge RDMA nommée *myVM* déployé dans un groupe de ressources hello nommé *myResourceGroup* Bonjour  *Ouest des États-Unis* région :

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  Pour plus d’informations, consultez [Extensions et fonctionnalités de la machine virtuelle](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Vous pouvez également travailler avec les extensions pour les ordinateurs virtuels déployés dans hello [modèle de déploiement classique](classic/manage-extensions.md).


## <a name="using-hpc-pack"></a>Utilisation de HPC Pack

[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuit HPC cluster et le travail de solution de gestion de Microsoft, il est possible de toocreate un cluster de calcul dans les applications MPI de basés sur Windows Azure toorun et d’autres charges de travail HPC. HPC Pack 2012 R2 et versions ultérieures incluent un environnement d’exécution pour MS-MPI qui utilise le réseau RDMA Azure hello déployés sur des machines virtuelles prenant en charge RDMA.




## <a name="other-sizes"></a>Autres tailles
- [Usage général](sizes-general.md)
- [Optimisé pour le calcul](sizes-compute.md)
- [Mémoire optimisée](../virtual-machines-windows-sizes-memory.md)
- [Optimisé pour le stockage](../virtual-machines-windows-sizes-storage.md)
- [Optimisé pour le GPU](sizes-gpu.md)

## <a name="next-steps"></a>Étapes suivantes

- Pour les instances de calcul intensif hello des listes de contrôle toouse avec HPC Pack sur Windows Server, consultez [configuration d’un cluster Windows RDMA avec des applications MPI HPC Pack toorun](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

- instances de calcul intensif toouse lors de l’exécution des applications MPI avec Azure Batch, consultez [multi-instance utilisez tâches toorun les applications d’Interface MPI (Message Passing) dans Azure Batch](../../batch/batch-mpi.md).

- Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.




