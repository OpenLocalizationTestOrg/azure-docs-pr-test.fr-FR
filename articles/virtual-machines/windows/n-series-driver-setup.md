---
title: configuration du pilote aaaAzure N-series pour Windows | Documents Microsoft
description: "Comment tooset les pilotes NVIDIA GPU pour les machines virtuelles de série N Windows en cours d’exécution dans Azure"
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
ms.openlocfilehash: 2acce57d4f9eb1d02bf3bc0303bcb9690475698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a>Configuration des pilotes GPU NVIDIA pour les machines virtuelles série N exécutant Windows Server
avantage tootake hello GPU des fonctionnalités de N-series Azure machines virtuelles exécutant Windows Server 2016 ou Windows Server 2012 R2, installez pris en charge les pilotes de graphiques NVIDIA. Cet article vous offre des étapes de configuration de pilote lorsque vous avez déployé une machine virtuelle de série N. Des informations de configuration du pilote sont également disponibles pour [les machines virtuelles Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Pour obtenir les spécifications de base, les capacités de stockage et les informations relatives aux disques, consultez [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Tailles de machine virtuelle Windows GPU). 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a>Installation du pilote

1. Se connecter à un bureau à distance tooeach N-series VM.

2. Télécharger, extraire et installer le pilote hello pris en charge votre système d’exploitation Windows.

Sur les machines virtuelles NV Azure, le redémarrage est nécessaire après l’installation du pilote. Sur les machines virtuelles NC, le redémarrage n’est pas nécessaire.

## <a name="verify-driver-installation"></a>Vérification de l’installation du pilote

Vous pouvez vérifier l’installation du pilote dans le Gestionnaire de périphériques. Hello suivant montre une configuration réussie de la carte de hello Tesla K80 sur une machine virtuelle de Azure NC.

![Propriétés du pilote GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

tooquery hello état du périphérique GPU, exécutez hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) utilitaire de ligne de commande installé avec le pilote de hello.

1. Ouvrez une invite de commandes et modifiez toohello **C:\Program Files\NVIDIA Corporation\NVSMI** active.

2. Exécutez **nvidia-smi**. Si le pilote de hello est installé toobelow similaire de sortie s’affiche. Notez que **GPU-Util** montre **0 %** , sauf si vous exécutez une charge de travail GPU sur hello machine virtuelle.

![État de l’appareil NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a>Réseau RDMA pour les machines virtuelles NC24r

Connectivité réseau RDMA peut être activée sur les ordinateurs virtuels de NC24r déployés dans hello même groupe à haute disponibilité. Hello extension HpcVmDrivers doit être ajouté tooinstall des pilotes de périphérique de réseau de Windows qui permettent la connectivité RDMA. tooadd hello VM extension tooan NC24r VM, utilisez [Azure PowerShell](/powershell/azure/overview) applets de commande pour le Gestionnaire de ressources Azure.

> [!NOTE]
> Actuellement, uniquement à Windows Server 2012 R2 prend en charge réseau RDMA hello sur des machines virtuelles NC24r.
> 

tooinstall hello dernière version 1.1 extension HpcVMDrivers sur un ordinateur prenant en charge RDMA virtuel existant nommé myVM dans la région ouest des États-Unis hello :
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  Pour plus d’informations, consultez [Extensions et fonctionnalités de machine virtuelle pour Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

réseau RDMA Hello prend en charge le trafic de l’Interface MPI (Message Passing) pour les applications en cours d’exécution avec [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) ou Intel MPI 5.x. 


## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur hello NVIDIA GPU sur hello machines virtuelles de série N, consultez :
    * [NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (pour les machines virtuelles NC Azure)
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (pour les machines virtuelles NV Azure)

* Les développeurs qui créent des applications accélération GPU hello NVIDIA Tesla GPU peuvent également télécharger et installer hello CUDA Toolkit 8 pour [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) ou [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe). Pour plus d’informations, consultez hello [Guide d’Installation CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).


