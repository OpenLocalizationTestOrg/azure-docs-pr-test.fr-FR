---
title: Tailles des machines virtuelles Linux Azure - GPU | Microsoft Docs
description: "Répertorie les différentes tailles de GPU optimisées disponibles pour les machines virtuelles Linux dans Azure."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 5c9bf89feba519147b07f2810fe4da882664e89e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="gpu-linux-vm-sizes"></a><span data-ttu-id="6f626-103">Tailles de machine virtuelle Linux GPU</span><span class="sxs-lookup"><span data-stu-id="6f626-103">GPU Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

<span data-ttu-id="6f626-104">Pour les étapes d’installation et de vérification des pilotes, consultez l’article sur l’[installation de pilotes de la série N pour Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="6f626-104">For driver installation and verification steps, see [N-series driver setup for Linux](n-series-driver-setup.md).</span></span>

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* <span data-ttu-id="6f626-105">Nous ne recommandons pas l’installation d’un serveur spécifique ou d’autres systèmes qui utilisent le pilote nouveau sur les machines virtuelles Ubuntu NC.</span><span class="sxs-lookup"><span data-stu-id="6f626-105">We don't recommend installing X server or other systems that use the nouveau driver on Ubuntu NC VMs.</span></span> <span data-ttu-id="6f626-106">Avant d’installer les pilotes GPU NVIDIA, vous devez désactiver le pilote nouveau.</span><span class="sxs-lookup"><span data-stu-id="6f626-106">Before installing NVIDIA GPU drivers, you need to disable the nouveau driver.</span></span>  

## <a name="other-sizes"></a><span data-ttu-id="6f626-107">Autres tailles</span><span class="sxs-lookup"><span data-stu-id="6f626-107">Other sizes</span></span>
- [<span data-ttu-id="6f626-108">Usage général</span><span class="sxs-lookup"><span data-stu-id="6f626-108">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="6f626-109">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="6f626-109">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="6f626-110">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="6f626-110">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="6f626-111">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="6f626-111">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="6f626-112">Calcul haute performance</span><span class="sxs-lookup"><span data-stu-id="6f626-112">High performance compute</span></span>](sizes-hpc.md)

## <a name="next-steps"></a><span data-ttu-id="6f626-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6f626-113">Next steps</span></span>
<span data-ttu-id="6f626-114">Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.</span><span class="sxs-lookup"><span data-stu-id="6f626-114">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>