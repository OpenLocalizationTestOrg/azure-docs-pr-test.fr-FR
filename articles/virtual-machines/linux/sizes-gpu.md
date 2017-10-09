---
title: "tailles d’aaaAzure Linux VM - GPU | Documents Microsoft"
description: "Répertorie les tailles GPU optimisé hello différents disponibles pour les ordinateurs virtuels Linux dans Azure."
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
ms.openlocfilehash: e98f720499be37df4048aeb513aa4f6b187b7335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="gpu-linux-vm-sizes"></a><span data-ttu-id="d4187-103">Tailles de machine virtuelle Linux GPU</span><span class="sxs-lookup"><span data-stu-id="d4187-103">GPU Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-gpu](../../../includes/virtual-machines-common-sizes-gpu.md)]


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

<span data-ttu-id="d4187-104">Pour les étapes d’installation et de vérification des pilotes, consultez l’article sur l’[installation de pilotes de la série N pour Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="d4187-104">For driver installation and verification steps, see [N-series driver setup for Linux](n-series-driver-setup.md).</span></span>

[!INCLUDE [virtual-machines-n-series-considerations](../../../includes/virtual-machines-n-series-considerations.md)]

* <span data-ttu-id="d4187-105">Nous ne vous recommandons d’installer X server ou d’autres systèmes qui utilisent le pilote de nouveau hello sur des machines virtuelles de NC Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="d4187-105">We don't recommend installing X server or other systems that use hello nouveau driver on Ubuntu NC VMs.</span></span> <span data-ttu-id="d4187-106">Avant d’installer les pilotes NVIDIA GPU, vous avez besoin d’un pilote de nouveau toodisable hello.</span><span class="sxs-lookup"><span data-stu-id="d4187-106">Before installing NVIDIA GPU drivers, you need toodisable hello nouveau driver.</span></span>  

## <a name="other-sizes"></a><span data-ttu-id="d4187-107">Autres tailles</span><span class="sxs-lookup"><span data-stu-id="d4187-107">Other sizes</span></span>
- [<span data-ttu-id="d4187-108">Usage général</span><span class="sxs-lookup"><span data-stu-id="d4187-108">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="d4187-109">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="d4187-109">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="d4187-110">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="d4187-110">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="d4187-111">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="d4187-111">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="d4187-112">Calcul haute performance</span><span class="sxs-lookup"><span data-stu-id="d4187-112">High performance compute</span></span>](sizes-hpc.md)

## <a name="next-steps"></a><span data-ttu-id="d4187-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d4187-113">Next steps</span></span>
<span data-ttu-id="d4187-114">Lisez-en davantage sur les [Unités de calcul Azure (ACU)](acu.md) pour découvrir comment comparer les performances de calcul entre les références Azure.</span><span class="sxs-lookup"><span data-stu-id="d4187-114">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>