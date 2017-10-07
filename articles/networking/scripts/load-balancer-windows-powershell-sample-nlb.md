---
title: "Exemple de Script PowerShell - charge équilibrer le trafic tooVMs pour la haute disponibilité d’aaaAzure | Documents Microsoft"
description: "Exemple de PowerShell Script Azure - charge équilibrer le trafic tooVMs pour la haute disponibilité"
services: load-balancer
documentationcenter: load-balancer
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 332c39e1aad071ca6f7ce420ccc1f423ef647d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a>Charger tooVMs le trafic de solde pour la haute disponibilité

Cet exemple de script crée tous les éléments nécessaires toorun plusieurs machines virtuelles de Windows configurés dans une haute disponibilité et de charge équilibrée de configuration. Après l’exécution du script hello, vous aurez trois machines virtuelles, tooan jointe à haute disponibilité Azure et accessible via un équilibrage de charge Azure.

Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Quick Create VM")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant de commandes toocreate un groupe de ressources, machine virtuelle, haute disponibilité, équilibrage de charge et toutes les ressources. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Crée une configuration de sous-réseau. Cette configuration est utilisée avec le processus de création du réseau virtuel hello. |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Crée un réseau virtuel et un sous-réseau Azure. |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)  | Crée une adresse IP publique avec une adresse IP statique et un nom DNS associé. |
| [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer)  | Crée un équilibreur de charge Azure. |
| [New-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | Crée une sonde d’équilibreur de charge. Une sonde d’équilibrage de charge est utilisé toomonitor chaque machine virtuelle dans le jeu d’équilibrage de charge de hello. Si toutes les machines virtuelles devient inaccessible, le trafic n’est pas routé toohello machine virtuelle. |
| [New-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | Crée une règle d’équilibreur de charge. Dans cet exemple, une règle est créée pour le port 80. Comme le trafic HTTP arrive au niveau de l’équilibrage de charge hello, il est routé tooport 80 une des machines virtuelles de hello dans le jeu d’équilibrage de charge de hello. |
| [New-AzureRmLoadBalancerInboundNatRuleConfig](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | Crée une règle de traduction d’adresses réseau (NAT) pour l’équilibreur de charge.  Les règles NAT de mappent un port de port de tooa d’équilibrage de charge de hello sur une machine virtuelle. Dans cet exemple, une règle NAT est créée pour SSH trafic tooeach machine virtuelle dans le jeu d’équilibrage de charge de hello.  |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Crée un groupe de sécurité réseau (NSG), qui est une limite de sécurité entre l’ordinateur virtuel pour internet et hello hello. |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | Crée un tooallow de règle de groupe de sécurité réseau le trafic entrant. Dans cet exemple, le port 22 est ouvert pour le trafic SSH. |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Crée une carte réseau virtuelle et attache les réseaux virtuels toohello, du sous-réseau et groupe de sécurité réseau. |
| [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) | Crée un groupe à haute disponibilité. Haute disponibilité garantit la disponibilité des applications en répartissant les machines virtuelles de hello sur ressources physiques telles qu’en cas de défaillance, ensemble hello n’est pas terminée. |
| [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Crée une configuration de machine virtuelle. Cette configuration inclut des informations telles que le nom de la machine virtuelle, le système d’exploitation et les informations d’identification d’administration. configuration de Hello est utilisée lors de la création de la machine virtuelle. |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)  | Crée la machine virtuelle de hello et connecte une carte réseau de toohello, du réseau virtuel, sous-réseau et groupe de sécurité réseau. Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification d’administration.  |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Supprime un groupe de ressources, y compris toutes les ressources imbriquées. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Vous trouverez des exemples de script PowerShell mise en réseau supplémentaires dans hello [documentation de vue d’ensemble de la mise en réseau Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
