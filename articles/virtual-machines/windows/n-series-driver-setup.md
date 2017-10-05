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
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="6f8b3-103">Configuration des pilotes GPU NVIDIA pour les machines virtuelles série N exécutant Windows Server</span><span class="sxs-lookup"><span data-stu-id="6f8b3-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="6f8b3-104">Pour tirer parti des fonctionnalités GPU des machines virtuelles série N Azure exécutant Windows Server 2016 ou Windows Server 2012 R2, installez des pilotes graphiques NVIDIA.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-104">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="6f8b3-105">Cet article vous offre des étapes de configuration de pilote lorsque vous avez déployé une machine virtuelle de série N.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="6f8b3-106">Des informations de configuration du pilote sont également disponibles pour [les machines virtuelles Linux](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6f8b3-106">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="6f8b3-107">Pour obtenir les spécifications de base, les capacités de stockage et les informations relatives aux disques, consultez [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Tailles de machine virtuelle Windows GPU).</span><span class="sxs-lookup"><span data-stu-id="6f8b3-107">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a><span data-ttu-id="6f8b3-108">Installation du pilote</span><span class="sxs-lookup"><span data-stu-id="6f8b3-108">Driver installation</span></span>

1. <span data-ttu-id="6f8b3-109">Connectez-vous à chaque machine virtuelle série N à l’aide du Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-109">Connect by Remote Desktop to each N-series VM.</span></span>

2. <span data-ttu-id="6f8b3-110">Téléchargez, extrayez et installez le pilote pris en charge pour votre système d’exploitation Windows.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-110">Download, extract, and install the supported driver for your Windows operating system.</span></span>

<span data-ttu-id="6f8b3-111">Sur les machines virtuelles NV Azure, le redémarrage est nécessaire après l’installation du pilote.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-111">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="6f8b3-112">Sur les machines virtuelles NC, le redémarrage n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-112">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="6f8b3-113">Vérification de l’installation du pilote</span><span class="sxs-lookup"><span data-stu-id="6f8b3-113">Verify driver installation</span></span>

<span data-ttu-id="6f8b3-114">Vous pouvez vérifier l’installation du pilote dans le Gestionnaire de périphériques.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-114">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="6f8b3-115">L’exemple suivant illustre une configuration réussie de la carte Tesla K80 sur une machine virtuelle NC Azure.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-115">The following example shows successful configuration of the Tesla K80 card on an Azure NC VM.</span></span>

![Propriétés du pilote GPU](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="6f8b3-117">Pour interroger l’état de l’appareil GPU, exécutez l’utilitaire de ligne de commande [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) installé avec le pilote.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-117">To query the GPU device state, run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span>

1. <span data-ttu-id="6f8b3-118">Ouvrez une invite de commandes et apportez vos modifications dans le répertoire **C:\Program Files\NVIDIA Corporation\NVSMI**.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-118">Open a command prompt and change to the **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="6f8b3-119">Exécutez **nvidia-smi**.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-119">Run **nvidia-smi**.</span></span> <span data-ttu-id="6f8b3-120">Si le pilote est installé, vous verrez un résultat du type suivant.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-120">If the driver is installed you will see output similar to below.</span></span> <span data-ttu-id="6f8b3-121">**GPU-Util** affiche **0 %** sauf si vous exécutez actuellement une charge de travail GPU sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-121">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on the VM.</span></span>

![État de l’appareil NVIDIA](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="6f8b3-123">Réseau RDMA pour les machines virtuelles NC24r</span><span class="sxs-lookup"><span data-stu-id="6f8b3-123">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="6f8b3-124">La connectivité réseau RDMA peut être activée sur des machines virtuelles NC24r déployées dans le même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-124">RDMA network connectivity can be enabled on NC24r VMs deployed in the same availability set.</span></span> <span data-ttu-id="6f8b3-125">L’extension HpcVmDrivers doit être ajoutée pour installer les pilotes d’appareils réseau Windows nécessaires à la connectivité RDMA.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-125">The HpcVmDrivers extension must be added to install Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="6f8b3-126">Pour ajouter l’extension de machine virtuelle sur une machine virtuelle NC24r, utilisez les applets de commande [Azure PowerShell](/powershell/azure/overview) pour Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-126">To add the VM extension to an NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="6f8b3-127">Actuellement, seul Windows Server 2012 R2 prend en charge le réseau RDMA sur des machines virtuelles NC24r.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-127">Currently, only Windows Server 2012 R2 supports the RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="6f8b3-128">Pour installer la dernière version 1.1 de l’extension HpcVMDrivers sur une machine virtuelle existante prenant en charge RDMA et nommée myVM dans la région États-Unis de l'Ouest :</span><span class="sxs-lookup"><span data-stu-id="6f8b3-128">To install the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in the West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="6f8b3-129">Pour plus d’informations, consultez [Extensions et fonctionnalités de machine virtuelle pour Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6f8b3-129">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="6f8b3-130">Le réseau RDMA prend en charge le trafic MPI (Message Passing Interface) pour les applications exécutées avec [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) ou Intel MPI 5.x.</span><span class="sxs-lookup"><span data-stu-id="6f8b3-130">The RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="6f8b3-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6f8b3-131">Next steps</span></span>

* <span data-ttu-id="6f8b3-132">Pour plus d’informations sur les GPU NVIDIA sur les machines virtuelles série N, consultez :</span><span class="sxs-lookup"><span data-stu-id="6f8b3-132">For more information about the NVIDIA GPUs on the N-series VMs, see:</span></span>
    * <span data-ttu-id="6f8b3-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (pour les machines virtuelles NC Azure)</span><span class="sxs-lookup"><span data-stu-id="6f8b3-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="6f8b3-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (pour les machines virtuelles NV Azure)</span><span class="sxs-lookup"><span data-stu-id="6f8b3-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="6f8b3-135">Les développeurs qui créent des applications avec accélération GPU pour les GPU Tesla NVIDIA peuvent également télécharger et installer le kit d’outils 8 CUDA pour [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) ou [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span><span class="sxs-lookup"><span data-stu-id="6f8b3-135">Developers building GPU-accelerated applications for the NVIDIA Tesla GPUs can also download and install the CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="6f8b3-136">Pour plus d’informations, consultez le [Guide d’installation de CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span><span class="sxs-lookup"><span data-stu-id="6f8b3-136">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


