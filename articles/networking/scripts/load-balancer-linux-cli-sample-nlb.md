---
title: "Exemple de Script CLI - charge équilibrer le trafic tooVMs pour la haute disponibilité d’aaaAzure | Documents Microsoft"
description: "Exemple de Script CLI Azure - charge équilibrer le trafic tooVMs pour la haute disponibilité"
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
ms.openlocfilehash: 0954b5c261512724dfb9c6e7be123c9d45624f4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a>Charger tooVMs le trafic de solde pour la haute disponibilité

Cet exemple de script crée tous les éléments nécessaires toorun plusieurs machines virtuelles de Ubuntu configurés dans une haute disponibilité et de charge équilibrée de configuration. Après l’exécution du script hello, vous aurez trois machines virtuelles, tooan jointe à haute disponibilité Azure et accessible via un équilibrage de charge Azure. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant de commandes toocreate un groupe de ressources, machine virtuelle, haute disponibilité, équilibrage de charge et toutes les ressources. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Crée un réseau virtuel et un sous-réseau Azure. |
| [az network public-ip create](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Crée une adresse IP publique avec une adresse IP statique et un nom DNS associé. |
| [az network lb create](https://docs.microsoft.com/cli/azure/network/lb#create) | Crée un équilibreur de charge Azure. |
| [az network lb probe create](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Crée une sonde d’équilibreur de charge. Une sonde d’équilibrage de charge est utilisé toomonitor chaque machine virtuelle dans le jeu d’équilibrage de charge de hello. Si toutes les machines virtuelles devient inaccessible, le trafic n’est pas routé toohello machine virtuelle. |
| [az network lb rule create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Crée une règle d’équilibeur de charge. Dans cet exemple, une règle est créée pour le port 80. Comme le trafic HTTP arrive au niveau de l’équilibrage de charge hello, il est routé tooport 80 une des machines virtuelles de hello dans le jeu de hello équilibrage de charge. |
| [az network lb inbound-nat-rule create](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | Crée une règle de traduction d’adresses réseau (NAT) pour l’équilibreur de charge.  Les règles NAT de mappent un port de port de tooa d’équilibrage de charge de hello sur une machine virtuelle. Dans cet exemple, une règle NAT est créée pour SSH trafic tooeach machine virtuelle dans le jeu d’équilibrage de charge de hello.  |
| [az network nsg create](https://docs.microsoft.com/cli/azure/network/nsg#create) | Crée un groupe de sécurité réseau (NSG), qui est une limite de sécurité entre l’ordinateur virtuel pour internet et hello hello. |
| [az network nsg rule create](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Crée un tooallow de règle de groupe de sécurité réseau le trafic entrant. Dans cet exemple, le port 22 est ouvert pour le trafic SSH. |
| [az network nic create](https://docs.microsoft.com/cli/azure/network/nic#create) | Crée une carte réseau virtuelle et attache les réseaux virtuels toohello, du sous-réseau et groupe de sécurité réseau. |
| [az vm availability-set create](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Crée un groupe à haute disponibilité. Haute disponibilité garantit la disponibilité des applications en répartissant les machines virtuelles de hello sur ressources physiques telles qu’en cas de défaillance, ensemble hello n’est pas terminée. |
| [az vm create](/cli/azure/vm#create) | Crée la machine virtuelle de hello et connecte une carte réseau de toohello, du réseau virtuel, sous-réseau et groupe de sécurité réseau. Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification d’administration.  |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Supprime un groupe de ressources, y compris toutes les ressources imbriquées. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Vous trouverez des exemples supplémentaires de script CLI de mise en réseau Azure Bonjour [documentation de la mise en réseau Azure](../cli-samples.md).
