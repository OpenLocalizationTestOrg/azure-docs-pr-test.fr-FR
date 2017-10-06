---
title: "aaaAzure exemple de Script CLI - équilibre la charge de plusieurs sites Web avec hello CLI d’Azure | Documents Microsoft"
description: "Exemple de Script CLI Azure - équilibre la charge de plusieurs sites Web toohello même machine virtuelle"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a>Équilibrer la charge de plusieurs sites web

Cet exemple de script crée un réseau virtuel avec deux machines virtuelles qui sont membres d’un groupe à haute disponibilité. Un équilibreur de charge dirige le trafic pour les deux machines virtuelles de toohello deux des adresses IP. Après l’exécution du script hello, vous pouvez déployer toohello logiciel de serveur web machines virtuelles et héberger plusieurs sites web, chacune avec sa propre adresse IP.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant les commandes toocreate un groupe de ressources du réseau virtuel, équilibreur de charge et toutes les ressources. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Crée un réseau virtuel et un sous-réseau Azure. |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Crée une adresse IP publique avec une adresse IP statique et un nom DNS associé. |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) | Crée un équilibreur de charge Azure. |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Crée une sonde d’équilibreur de charge. Une sonde d’équilibrage de charge est utilisé toomonitor chaque machine virtuelle dans le jeu d’équilibrage de charge de hello. Si toutes les machines virtuelles devient inaccessible, le trafic n’est pas routé toohello machine virtuelle. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Crée une règle d’équilibeur de charge. Dans cet exemple, une règle est créée pour le port 80. Comme le trafic HTTP arrive au niveau de l’équilibrage de charge hello, il est routé tooport 80 une des machines virtuelles de hello dans le jeu d’équilibrage de charge de hello. |
| [az network lb frontend-ip create](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | Créer une adresse IP de serveur frontal pour hello équilibrage de charge. |
| [az network lb address-pool create](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | Crée un pool d’adresses principal. |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | Crée une carte réseau virtuelle et l’attache toohello des réseaux virtuels et le sous-réseau. |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Crée un groupe à haute disponibilité. Haute disponibilité garantit la disponibilité des applications en répartissant les machines virtuelles de hello sur ressources physiques telles qu’en cas de défaillance, ensemble hello n’est pas terminée. |
| [az network nic ip-config create](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | Crée une configuration IP. Vous devez avoir hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic fonctionnalité est activée pour votre abonnement. Qu’une seule configuration peut être désignée comme configuration IP principale de hello par carte réseau, à l’aide de hello--Vérifiez principal indicateur. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Crée la machine virtuelle de hello et connecte une carte réseau de toohello, du réseau virtuel, sous-réseau et groupe de sécurité réseau. Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification d’administration.  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Supprime un groupe de ressources, y compris toutes les ressources imbriquées. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Vous trouverez des exemples de script CLI mise en réseau supplémentaires dans hello [documentation de vue d’ensemble de la mise en réseau Azure](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
