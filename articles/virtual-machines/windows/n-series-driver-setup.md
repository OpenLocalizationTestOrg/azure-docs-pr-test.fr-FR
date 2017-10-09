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
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="8c094-103">Configuration des pilotes GPU NVIDIA pour les machines virtuelles série N exécutant Windows Server</span><span class="sxs-lookup"><span data-stu-id="8c094-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="8c094-104">avantage tootake hello GPU des fonctionnalités de N-series Azure machines virtuelles exécutant Windows Server 2016 ou Windows Server 2012 R2, installez pris en charge les pilotes de graphiques NVIDIA.</span><span class="sxs-lookup"><span data-stu-id="8c094-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="8c094-105">Cet article vous offre des étapes de configuration de pilote lorsque vous avez déployé une machine virtuelle de série N.</span><span class="sxs-lookup"><span data-stu-id="8c094-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="8c094-106">Des informations de configuration du pilote sont également disponibles pour [les machines virtuelles Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8c094-106">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="8c094-107">Pour obtenir les spécifications de base, les capacités de stockage et les informations relatives aux disques, consultez [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Tailles de machine virtuelle Windows GPU).</span><span class="sxs-lookup"><span data-stu-id="8c094-107">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a><span data-ttu-id="8c094-108">Installation du pilote</span><span class="sxs-lookup"><span data-stu-id="8c094-108">Driver installation</span></span>

1. <span data-ttu-id="8c094-109">Se connecter à un bureau à distance tooeach N-series VM.</span><span class="sxs-lookup"><span data-stu-id="8c094-109">Connect by Remote Desktop tooeach N-series VM.</span></span>

2. <span data-ttu-id="8c094-110">Télécharger, extraire et installer le pilote hello pris en charge votre système d’exploitation Windows.</span><span class="sxs-lookup"><span data-stu-id="8c094-110">Download, extract, and install hello supported driver for your Windows operating system.</span></span>

<span data-ttu-id="8c094-111">Sur les machines virtuelles NV Azure, le redémarrage est nécessaire après l’installation du pilote.</span><span class="sxs-lookup"><span data-stu-id="8c094-111">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="8c094-112">Sur les machines virtuelles NC, le redémarrage n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8c094-112">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="8c094-113">Vérification de l’installation du pilote</span><span class="sxs-lookup"><span data-stu-id="8c094-113">Verify driver installation</span></span>

<span data-ttu-id="8c094-114">Vous pouvez vérifier l’installation du pilote dans le Gestionnaire de périphériques.</span><span class="sxs-lookup"><span data-stu-id="8c094-114">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="8c094-115">Hello suivant montre une configuration réussie de la carte de hello Tesla K80 sur une machine virtuelle de Azure NC.</span><span class="sxs-lookup"><span data-stu-id="8c094-115">hello following example shows successful configuration of hello Tesla K80 card on an Azure NC VM.</span></span>

![Propriétés du pilote GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="8c094-117">tooquery hello état du périphérique GPU, exécutez hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) utilitaire de ligne de commande installé avec le pilote de hello.</span><span class="sxs-lookup"><span data-stu-id="8c094-117">tooquery hello GPU device state, run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span>

1. <span data-ttu-id="8c094-118">Ouvrez une invite de commandes et modifiez toohello **C:\Program Files\NVIDIA Corporation\NVSMI** active.</span><span class="sxs-lookup"><span data-stu-id="8c094-118">Open a command prompt and change toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="8c094-119">Exécutez **nvidia-smi**.</span><span class="sxs-lookup"><span data-stu-id="8c094-119">Run **nvidia-smi**.</span></span> <span data-ttu-id="8c094-120">Si le pilote de hello est installé toobelow similaire de sortie s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8c094-120">If hello driver is installed you will see output similar toobelow.</span></span> <span data-ttu-id="8c094-121">Notez que **GPU-Util** montre **0 %** , sauf si vous exécutez une charge de travail GPU sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8c094-121">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on hello VM.</span></span>

![État de l’appareil NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="8c094-123">Réseau RDMA pour les machines virtuelles NC24r</span><span class="sxs-lookup"><span data-stu-id="8c094-123">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="8c094-124">Connectivité réseau RDMA peut être activée sur les ordinateurs virtuels de NC24r déployés dans hello même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="8c094-124">RDMA network connectivity can be enabled on NC24r VMs deployed in hello same availability set.</span></span> <span data-ttu-id="8c094-125">Hello extension HpcVmDrivers doit être ajouté tooinstall des pilotes de périphérique de réseau de Windows qui permettent la connectivité RDMA.</span><span class="sxs-lookup"><span data-stu-id="8c094-125">hello HpcVmDrivers extension must be added tooinstall Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="8c094-126">tooadd hello VM extension tooan NC24r VM, utilisez [Azure PowerShell](/powershell/azure/overview) applets de commande pour le Gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="8c094-126">tooadd hello VM extension tooan NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="8c094-127">Actuellement, uniquement à Windows Server 2012 R2 prend en charge réseau RDMA hello sur des machines virtuelles NC24r.</span><span class="sxs-lookup"><span data-stu-id="8c094-127">Currently, only Windows Server 2012 R2 supports hello RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="8c094-128">tooinstall hello dernière version 1.1 extension HpcVMDrivers sur un ordinateur prenant en charge RDMA virtuel existant nommé myVM dans la région ouest des États-Unis hello :</span><span class="sxs-lookup"><span data-stu-id="8c094-128">tooinstall hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in hello West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="8c094-129">Pour plus d’informations, consultez [Extensions et fonctionnalités de machine virtuelle pour Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8c094-129">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="8c094-130">réseau RDMA Hello prend en charge le trafic de l’Interface MPI (Message Passing) pour les applications en cours d’exécution avec [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) ou Intel MPI 5.x.</span><span class="sxs-lookup"><span data-stu-id="8c094-130">hello RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="8c094-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8c094-131">Next steps</span></span>

* <span data-ttu-id="8c094-132">Pour plus d’informations sur hello NVIDIA GPU sur hello machines virtuelles de série N, consultez :</span><span class="sxs-lookup"><span data-stu-id="8c094-132">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="8c094-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (pour les machines virtuelles NC Azure)</span><span class="sxs-lookup"><span data-stu-id="8c094-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="8c094-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (pour les machines virtuelles NV Azure)</span><span class="sxs-lookup"><span data-stu-id="8c094-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="8c094-135">Les développeurs qui créent des applications accélération GPU hello NVIDIA Tesla GPU peuvent également télécharger et installer hello CUDA Toolkit 8 pour [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) ou [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span><span class="sxs-lookup"><span data-stu-id="8c094-135">Developers building GPU-accelerated applications for hello NVIDIA Tesla GPUs can also download and install hello CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="8c094-136">Pour plus d’informations, consultez hello [Guide d’Installation CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span><span class="sxs-lookup"><span data-stu-id="8c094-136">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


