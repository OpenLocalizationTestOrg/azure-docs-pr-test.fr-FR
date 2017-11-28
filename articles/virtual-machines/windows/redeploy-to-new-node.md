---
title: "Redéployer des machines virtuelles Windows dans Azure | Microsoft Docs"
description: "Comment redéployer des machines virtuelles Windows dans Azure pour atténuer les problèmes de connexion RDP."
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
ms.openlocfilehash: a607d0747f64ee6b224d300113905f54e003aef0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="redeploy-windows-virtual-machine-to-new-azure-node"></a><span data-ttu-id="b12d1-103">Redéployer des machines virtuelles Windows dans un nouveau nœud Azure</span><span class="sxs-lookup"><span data-stu-id="b12d1-103">Redeploy Windows virtual machine to new Azure node</span></span>
<span data-ttu-id="b12d1-104">Si vous avez été confronté à des difficultés pour la résolution des problèmes de connexion de Bureau à distance ou l’accès des applications à une machine virtuelle Azure basée sur Windows, le redéploiement de la machine virtuelle peut vous aider.</span><span class="sxs-lookup"><span data-stu-id="b12d1-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access to Windows-based Azure virtual machine (VM), redeploying the VM may help.</span></span> <span data-ttu-id="b12d1-105">Lorsque vous redéployez une machine virtuelle, celle-ci est déplacée vers un nouveau nœud au sein de l’infrastructure Azure, puis remise sous tension, conservant tous vos options de configuration et ressources associées.</span><span class="sxs-lookup"><span data-stu-id="b12d1-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="b12d1-106">Cet article vous montre comment redéployer une machine virtuelle à l’aide d’Azure PowerShell ou du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b12d1-106">This article shows you how to redeploy a VM using Azure PowerShell or the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="b12d1-107">Une fois que vous redéployez une machine virtuelle, le disque temporaire est perdu et les adresses IP dynamiques associées à l’interface réseau virtuelle sont mises à jour.</span><span class="sxs-lookup"><span data-stu-id="b12d1-107">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 


## <a name="using-azure-powershell"></a><span data-ttu-id="b12d1-108">Utilisation de Microsoft Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b12d1-108">Using Azure PowerShell</span></span>
<span data-ttu-id="b12d1-109">Assurez-vous que vous avez installé la dernière version d’Azure PowerShell 1.x.</span><span class="sxs-lookup"><span data-stu-id="b12d1-109">Make sure you have the latest Azure PowerShell 1.x installed on your machine.</span></span> <span data-ttu-id="b12d1-110">Pour plus d’informations, consultez la rubrique [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b12d1-110">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="b12d1-111">L’exemple suivant déploie la machine virtuelle nommée `myVM` dans le groupe de ressources nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="b12d1-111">The following example deploys the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="b12d1-112">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b12d1-112">Next steps</span></span>
<span data-ttu-id="b12d1-113">Si vous rencontrez des problèmes de connexion à votre machine virtuelle, vous pouvez rechercher une aide spécifique sur la [résolution des problèmes de connexion Bureau à distance](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou sur les [étapes de dépannage détaillées des connexions Bureau à distance](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b12d1-113">If you are having issues connecting to your VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="b12d1-114">Vous pouvez également lire des informations sur les [problèmes de dépannage des applications](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) si vous ne pouvez pas accéder à une application exécutée sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b12d1-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

