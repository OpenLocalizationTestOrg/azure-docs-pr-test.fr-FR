---
title: "aaaAzure exemple de Script CLI - créer deux machines virtuelles avec un groupe de sécurité réseau interne et externe | Documents Microsoft"
description: "Exemple de script Azure CLI - Créer deux machines virtuelles avec un groupe de sécurité réseau interne et un groupe de sécurité réseau externe"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: f04e62d09575bee34ac4aeee949736b34000c337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a>Sécuriser le trafic réseau entre les machines virtuelles

Ce script crée deux machines virtuelles et sécurise tooboth de trafic entrant. Un ordinateur virtuel est accessible sur hello internet et a un groupe de sécurité réseau (NSG) configuré tooallow trafic sur le port 3389 et le port 80. machine virtuelle de la deuxième Hello n’est pas accessible sur internet de hello, et a une tooonly de groupe de sécurité réseau configuré autoriser le trafic à partir de la première machine virtuelle de hello. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-windows-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’ordinateur virtuel, et toutes les ressources associées. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [az network vnet create](https://docs.microsoft.com/cli/azure/network/vnet#create) | Crée un réseau virtuel et un sous-réseau Azure. |
| [az network vnet subnet create](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | Crée un sous-réseau. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Crée la machine virtuelle de hello et connecte une carte réseau de toohello, du réseau virtuel, sous-réseau et groupe de sécurité réseau. Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification administratives.  |
| [az network nsg rule update](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | Met à jour une règle de groupe de sécurité réseau. Dans cet exemple, la règle de principaux de hello est toopass mis à jour par le trafic uniquement à partir de sous-réseau frontal de hello. |
| [az network nsg rule list](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | Renvoie les informations relatives à une règle de groupe de sécurité réseau. Dans cet exemple, le nom de la règle hello est stocké dans une variable pour une utilisation ultérieure dans le script de hello. |
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Supprime un groupe de ressources, y compris toutes les ressources imbriquées. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de Windows Azure VM](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
