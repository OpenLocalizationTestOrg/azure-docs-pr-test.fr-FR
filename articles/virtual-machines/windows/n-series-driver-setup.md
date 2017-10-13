---
title: "Configuration du pilote série N Azure pour Windows | Microsoft Docs"
description: "Procédure de configuration des pilotes GPU NVIDIA pour les machines virtuelles série N exécutant Windows dans Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3950c34-9406-48ae-bcd9-c0418607b37d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/07/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b480d10df777a2757c073ff77e1845d33d63163a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a>Configuration des pilotes GPU NVIDIA pour les machines virtuelles série N exécutant Windows Server
Pour tirer parti des fonctionnalités GPU des machines virtuelles série N Azure exécutant Windows Server 2016 ou Windows Server 2012 R2, installez des pilotes graphiques NVIDIA. Cet article vous offre des étapes de configuration de pilote lorsque vous avez déployé une machine virtuelle de série N. Des informations de configuration du pilote sont également disponibles pour [les machines virtuelles Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Pour obtenir les spécifications de base, les capacités de stockage et les informations relatives aux disques, consultez [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Tailles de machine virtuelle Windows GPU). 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a>Installation du pilote

1. Connectez-vous à chaque machine virtuelle série N à l’aide du Bureau à distance.

2. Téléchargez, extrayez et installez le pilote pris en charge pour votre système d’exploitation Windows.

Sur les machines virtuelles NV Azure, le redémarrage est nécessaire après l’installation du pilote. Sur les machines virtuelles NC, le redémarrage n’est pas nécessaire.

## <a name="verify-driver-installation"></a>Vérification de l’installation du pilote

Vous pouvez vérifier l’installation du pilote dans le Gestionnaire de périphériques. L’exemple suivant illustre une configuration réussie de la carte Tesla K80 sur une machine virtuelle NC Azure.

![Propriétés du pilote GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

Pour interroger l’état de l’appareil GPU, exécutez l’utilitaire de ligne de commande [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) installé avec le pilote.

1. Ouvrez une invite de commandes et apportez vos modifications dans le répertoire **C:\Program Files\NVIDIA Corporation\NVSMI**.

2. Exécutez **nvidia-smi**. Si le pilote est installé, vous verrez un résultat du type suivant. **GPU-Util** affiche **0 %** sauf si vous exécutez actuellement une charge de travail GPU sur la machine virtuelle.

![État de l’appareil NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a>Réseau RDMA pour les machines virtuelles NC24r

La connectivité réseau RDMA peut être activée sur des machines virtuelles NC24r déployées dans le même groupe à haute disponibilité. L’extension HpcVmDrivers doit être ajoutée pour installer les pilotes d’appareils réseau Windows nécessaires à la connectivité RDMA. Pour ajouter l’extension de machine virtuelle sur une machine virtuelle NC24r, utilisez les applets de commande [Azure PowerShell](/powershell/azure/overview) pour Azure Resource Manager.

> [!NOTE]
> Actuellement, seul Windows Server 2012 R2 prend en charge le réseau RDMA sur des machines virtuelles NC24r.
> 

Pour installer la dernière version 1.1 de l’extension HpcVMDrivers sur une machine virtuelle existante prenant en charge RDMA et nommée myVM dans la région États-Unis de l'Ouest :
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  Pour plus d’informations, consultez [Extensions et fonctionnalités de machine virtuelle pour Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Le réseau RDMA prend en charge le trafic MPI (Message Passing Interface) pour les applications exécutées avec [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) ou Intel MPI 5.x. 


## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur les GPU NVIDIA sur les machines virtuelles série N, consultez :
    * [NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (pour les machines virtuelles NC Azure)
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (pour les machines virtuelles NV Azure)

* Les développeurs qui créent des applications avec accélération GPU pour les GPU Tesla NVIDIA peuvent également télécharger et installer le kit d’outils 8 CUDA pour [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) ou [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe). Pour plus d’informations, consultez le [Guide d’installation de CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).


