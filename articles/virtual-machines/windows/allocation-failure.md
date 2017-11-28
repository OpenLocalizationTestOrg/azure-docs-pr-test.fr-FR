---
title: "échecs d’allocation de machine virtuelle Windows aaaTroubleshooting | Documents Microsoft"
description: "Résoudre les problèmes d’allocation pendant la création, le redémarrage ou le redimensionnement de machines virtuelles Windows dans Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resource-manager,azure-service-management
ms.assetid: bb939e23-77fc-4948-96f7-5037761c30e8
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: cjiang
ms.openlocfilehash: d0cc75ac60d952d8e4310cebc37654dc4f80857f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-windows-vms-in-azure"></a><span data-ttu-id="e09c3-103">Résoudre les problèmes d’allocation pendant la création, le redémarrage ou le redimensionnement de machines virtuelles Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="e09c3-103">Troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure</span></span>
<span data-ttu-id="e09c3-104">Lorsque vous créez une machine virtuelle, redémarrez arrêté de machines virtuelles (désallouées) ou redimensionnez une machine virtuelle, Microsoft Azure alloue des ressources de calcul tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="e09c3-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources tooyour subscription.</span></span> <span data-ttu-id="e09c3-105">Vous pouvez parfois recevoir des erreurs lorsque vous effectuez ces opérations--avant même que vous atteigniez les limites d’abonnement Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e09c3-105">You may occasionally receive errors when performing these operations -- even before you reach hello Azure subscription limits.</span></span> <span data-ttu-id="e09c3-106">Cet article explique les causes hello de certaines hello courants d’échecs d’allocation et suggère des corrections possibles.</span><span class="sxs-lookup"><span data-stu-id="e09c3-106">This article explains hello causes of some of hello common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="e09c3-107">Hello informations peuvent également être utiles lorsque vous planifiez le déploiement de hello de vos services.</span><span class="sxs-lookup"><span data-stu-id="e09c3-107">hello information may also be useful when you plan hello deployment of your services.</span></span> <span data-ttu-id="e09c3-108">Vous pouvez également [résoudre les problèmes d’allocation pendant la création, le redémarrage ou le redimensionnement de machines virtuelles Linux dans Azure](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e09c3-108">You can also [troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

