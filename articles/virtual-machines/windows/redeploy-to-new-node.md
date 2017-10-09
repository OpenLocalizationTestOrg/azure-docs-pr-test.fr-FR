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
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a>Redéployer toonew de machine virtuelle Windows Azure nœud
Si vous avez été confronté à des difficultés dans la résolution des problèmes de bureau à distance (RDP) connexion ou une application accéder à tooWindows Azure machine virtuelle (VM), hello machine virtuelle peut être utile de redéploiement. Lorsque vous redéployez un ordinateur virtuel, il déplace hello VM tooa nouveau nœud au sein de hello infrastructure Azure et puis l’alimente sur, en conservant toutes vos options de configuration et les ressources associées. Cet article vous montre comment tooredeploy une machine virtuelle à l’aide d’Azure PowerShell ou hello portail Azure.

> [!NOTE]
> Une fois que vous redéployez un ordinateur virtuel, disque temporaire de hello est perdu et les adresses IP dynamiques associés à interface réseau virtuelle sont mis à jour. 


## <a name="using-azure-powershell"></a>Utilisation de Microsoft Azure PowerShell
Assurez-vous que vous avez hello dernière version PowerShell Azure 1.x installés sur votre ordinateur. Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

exemple Hello déploie hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Étapes suivantes
Si vous rencontrez des problèmes de connexion tooyour machine virtuelle, vous trouverez une aide spécifique sur [dépannage des connexions RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [détaillée des étapes de dépannage de RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Vous pouvez également lire des informations sur les [problèmes de dépannage des applications](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) si vous ne pouvez pas accéder à une application exécutée sur votre machine virtuelle.

