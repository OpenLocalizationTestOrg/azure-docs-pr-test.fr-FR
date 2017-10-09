---
title: machines virtuelles aaaRedeploy Windows Azure | Documents Microsoft
description: "Comment Windows tooredeploy virtual machines dans Azure toomitigate RDP problèmes de connexion."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: genlin
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: 0ee456ee-4595-4a14-8916-72c9110fc8bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 903d9d5bf241075931ee4b746690c553d808a58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a><span data-ttu-id="7eb24-103">Redéployer toonew de machine virtuelle Windows Azure nœud</span><span class="sxs-lookup"><span data-stu-id="7eb24-103">Redeploy Windows virtual machine toonew Azure node</span></span>
<span data-ttu-id="7eb24-104">Si vous avez été confronté à des difficultés dans la résolution des problèmes de bureau à distance (RDP) connexion ou une application accéder à tooWindows Azure machine virtuelle (VM), hello machine virtuelle peut être utile de redéploiement.</span><span class="sxs-lookup"><span data-stu-id="7eb24-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access tooWindows-based Azure virtual machine (VM), redeploying hello VM may help.</span></span> <span data-ttu-id="7eb24-105">Lorsque vous redéployez un ordinateur virtuel, il déplace hello VM tooa nouveau nœud au sein de hello infrastructure Azure et puis l’alimente sur, en conservant toutes vos options de configuration et les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="7eb24-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="7eb24-106">Cet article vous montre comment tooredeploy une machine virtuelle à l’aide d’Azure PowerShell ou hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7eb24-106">This article shows you how tooredeploy a VM using Azure PowerShell or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="7eb24-107">Une fois que vous redéployez un ordinateur virtuel, disque temporaire de hello est perdu et les adresses IP dynamiques associés à interface réseau virtuelle sont mis à jour.</span><span class="sxs-lookup"><span data-stu-id="7eb24-107">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 


## <a name="using-azure-powershell"></a><span data-ttu-id="7eb24-108">Utilisation de Microsoft Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7eb24-108">Using Azure PowerShell</span></span>
<span data-ttu-id="7eb24-109">Assurez-vous que vous avez hello dernière version PowerShell Azure 1.x installés sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7eb24-109">Make sure you have hello latest Azure PowerShell 1.x installed on your machine.</span></span> <span data-ttu-id="7eb24-110">Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7eb24-110">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="7eb24-111">exemple Hello déploie hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="7eb24-111">hello following example deploys hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="7eb24-112">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7eb24-112">Next steps</span></span>
<span data-ttu-id="7eb24-113">Si vous rencontrez des problèmes de connexion tooyour machine virtuelle, vous trouverez une aide spécifique sur [dépannage des connexions RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [détaillée des étapes de dépannage de RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7eb24-113">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="7eb24-114">Vous pouvez également lire des informations sur les [problèmes de dépannage des applications](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) si vous ne pouvez pas accéder à une application exécutée sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7eb24-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

