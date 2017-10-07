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
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a>About H-series and compute-intensive A-series VMs for Linux (À propos des machines virtuelles de série H ou de calcul intensif de série A pour Linux)
Ici des informations générales et des considérations relatives à l’aide de hello plus récente de Azure H-series hello antérieures tailles A8, A9, A10 et A11, également appelé *intensives* instances. Cet article se concentre sur l’utilisation de ces tailles pour les machines virtuelles Linux. Vous pouvez également les utiliser pour des [machines virtuelles Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Pour plus d’informations sur les spécifications de base, les capacités de stockage et les disques, consultez l’article [Tailles de machines virtuelles](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a>Accéder à toohello réseau RDMA
Vous pouvez créer des clusters d’ordinateurs virtuels Linux prenant en charge RDMA qui exécutent une Hello suivant des distributions Linux HPC prises en charge et un avantage de tootake implémentation MPI prise en charge du réseau RDMA Azure de hello. Consultez [configurer une application MPI de Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) pour les options de déploiement et les étapes de configuration d’exemple.

* **Distributions** - vous devez déployer des machines virtuelles à partir de prenant en charge RDMA SUSE Linux Enterprise Server (SLES) ou des images dans HPC de base CentOS les logiciels non autorisés Wave (anciennement OpenLogic) hello Azure Marketplace. Hello images Marketplace suivantes prennent en charge la connectivité RDMA :
  
    * SLES 12 SP1 pour HPC, SLES 12 SP1 pour HPC (Premium)
    
    * HPC basé sur CentOS 7.1, HPC basé sur CentOS 6.5  
 
        > [!NOTE]
        > Pour les machines virtuelles de la série H, nous vous recommandons une image SLES 12 SP1 pour HPC ou une image HPC basée sur CentOS 7.1.
        >
        > Sur les images de HPC de base CentOS hello, les mises à jour du noyau sont désactivées dans hello **yum** fichier de configuration. Il s’agit, car les pilotes Linux RDMA hello sont distribuées sous la forme d’un package RPM et mises à jour de pilote peuvent ne pas fonctionnent si le noyau de hello est mise à jour.
        > 
        > 
* **MPI** - Intel MPI Library 5.x
  
    En fonction de l’image de Marketplace hello choisie, installation de licence, distinct, ou la configuration de Intel MPI peut être nécessaire, comme suit : 
  
  * **SLES 12 SP1 pour l’image HPC** -les packages Intel MPI sont distribués sur hello machine virtuelle. Installer en exécutant hello de commande suivante :

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * **Images HPC basées sur CentOS** : Intel MPI 5.1 est déjà installé.  
    
    Configuration système supplémentaire est nécessaire toorun des travaux MPI sur des machines virtuelles en cluster. Par exemple, sur un cluster de machines virtuelles, vous devez tooestablish approbation hello parmi les nœuds de calcul. Pour les paramètres par défaut, consultez [configurer une application MPI de Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="considerations-for-hpc-pack-and-linux"></a>Considérations relatives à HPC Pack et Linux
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), gratuit HPC cluster et le travail de solution de gestion de Microsoft, fournit une option pour vous instances de calcul intensif hello toouse avec Linux. Hello dernières versions de HPC Pack prend en charge plusieurs distributions Linux toorun sur nœuds déployés dans des machines virtuelles de Azure, gérés par un nœud principal de Windows Server. Avec les nœuds de calcul Linux prenant en charge RDMA Intel MPI en cours d’exécution, HPC Pack peut planifier et exécuter des applications Linux MPI réseau RDMA accès hello. tooget démarré, consultez [prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="network-topology-considerations"></a>Considérations sur la topologie réseau
* Sur des machines virtuelles Linux compatibles RDMA dans Azure, Eth1 est réservé au trafic réseau RDMA. Ne modifiez pas les paramètres Eth1 ou toute information dans le fichier de configuration hello faisant référence toothis réseau. Eth0 est réservé au trafic réseau Azure normal.
* Dans Azure, IP over Infiniband (IB) n’est pas pris en charge. Seul RDMA over IB est pris en charge.



## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur la disponibilité et la tarification des tailles de calcul intensif hello, consultez [Machines virtuelles tarification](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).
* Pour plus d’informations sur les capacités de stockage et sur les disques, consultez [Tailles de machines virtuelles](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* tooget a démarré le déploiement et l’utilisation de tailles de calcul intensif avec le RDMA sur Linux, consultez [configurer une application MPI de Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

