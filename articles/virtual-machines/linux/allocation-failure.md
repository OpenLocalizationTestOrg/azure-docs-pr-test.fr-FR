---
title: "Résolution des problèmes d’allocation de machines virtuelles Linux | Microsoft Docs"
description: "Résoudre les problèmes d’allocation pendant la création, le redémarrage ou le redimensionnement d’une machine virtuelle Linux dans Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resourece-manager,azure-service-management
ms.assetid: 1ef41144-6dd6-4a56-b180-9d8b3d05eae7
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cjiang
ms.openlocfilehash: c65ede134971c034006781e058c05a82ffb68a19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-linux-vms-in-azure"></a><span data-ttu-id="0bba4-103">Résoudre les problèmes d’allocation pendant la création, le redémarrage ou le redimensionnement de machines virtuelles Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="0bba4-103">Troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure</span></span>
<span data-ttu-id="0bba4-104">Quand vous créez une machine virtuelle, redémarrez des machines virtuelles ayant été arrêtées (désallouées) ou redimensionnez une machine virtuelle, Microsoft Azure alloue des ressources de calcul à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="0bba4-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources to your subscription.</span></span> <span data-ttu-id="0bba4-105">Vous pouvez parfois recevoir des erreurs lorsque vous effectuez ces opérations, avant même d’avoir atteint les limites de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="0bba4-105">You may occasionally receive errors when performing these operations -- even before you reach the Azure subscription limits.</span></span> <span data-ttu-id="0bba4-106">Cet article explique les causes de certains échecs d’allocation courants et propose des solutions possibles.</span><span class="sxs-lookup"><span data-stu-id="0bba4-106">This article explains the causes of some of the common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="0bba4-107">Les informations qu’il contient peuvent également vous être utiles dans le cadre de la planification du déploiement de vos services.</span><span class="sxs-lookup"><span data-stu-id="0bba4-107">The information may also be useful when you plan the deployment of your services.</span></span> <span data-ttu-id="0bba4-108">Vous pouvez également [résoudre les problèmes d’allocation pendant la création, le redémarrage ou le redimensionnement de machines virtuelles Linux dans Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0bba4-108">You can also [troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

