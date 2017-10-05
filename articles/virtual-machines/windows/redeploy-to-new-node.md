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
# <a name="redeploy-windows-virtual-machine-to-new-azure-node"></a>Redéployer des machines virtuelles Windows dans un nouveau nœud Azure
Si vous avez été confronté à des difficultés pour la résolution des problèmes de connexion de Bureau à distance ou l’accès des applications à une machine virtuelle Azure basée sur Windows, le redéploiement de la machine virtuelle peut vous aider. Lorsque vous redéployez une machine virtuelle, celle-ci est déplacée vers un nouveau nœud au sein de l’infrastructure Azure, puis remise sous tension, conservant tous vos options de configuration et ressources associées. Cet article vous montre comment redéployer une machine virtuelle à l’aide d’Azure PowerShell ou du portail Azure.

> [!NOTE]
> Une fois que vous redéployez une machine virtuelle, le disque temporaire est perdu et les adresses IP dynamiques associées à l’interface réseau virtuelle sont mises à jour. 


## <a name="using-azure-powershell"></a>Utilisation de Microsoft Azure PowerShell
Assurez-vous que vous avez installé la dernière version d’Azure PowerShell 1.x. Pour plus d’informations, consultez la rubrique [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).

L’exemple suivant déploie la machine virtuelle nommée `myVM` dans le groupe de ressources nommé `myResourceGroup` :

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Étapes suivantes
Si vous rencontrez des problèmes de connexion à votre machine virtuelle, vous pouvez rechercher une aide spécifique sur la [résolution des problèmes de connexion Bureau à distance](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou sur les [étapes de dépannage détaillées des connexions Bureau à distance](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Vous pouvez également lire des informations sur les [problèmes de dépannage des applications](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) si vous ne pouvez pas accéder à une application exécutée sur votre machine virtuelle.

