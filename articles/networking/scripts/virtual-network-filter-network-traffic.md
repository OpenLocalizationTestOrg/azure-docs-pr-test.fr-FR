---
title: "exemple de script CLI aaaAzure - le trafic réseau de machine virtuelle de filtre | Documents Microsoft"
description: "Exemple de script Azure CLI - Filtrer le trafic réseau de machine virtuelle entrant et sortant"
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: c2f14e54bc96c99420b4300d1c24a457ac8c948c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a>Filtrer le trafic réseau de machine virtuelle entrant et sortant

Cet exemple de script permet de créer un réseau virtuel avec des sous-réseaux frontaux et principaux. Le trafic du réseau entrant toohello le sous-réseau frontal est limitée tooHTTP, HTTPS et SSH, pendant sortant du trafic toohello Internet à partir du sous-réseau de hello principal n’est pas autorisée. Après avoir exécuté le script de hello, vous aurez une machine virtuelle avec deux cartes réseau. Chaque carte réseau est connectée tooa autre sous-réseau.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant de commandes toocreate un groupe de ressources, de réseau virtuel et de groupes de sécurité réseau. Chaque commande dans la table de hello lie documentation toocommand spécifique.

| Commande | Remarques |
|---|---|
| [az group create](/cli/azure/group#create) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [az network vnet create](/cli/azure/network/vnet#create) | Crée un réseau virtuel et un sous-réseau frontal Azure. |
| [az network subnet create](/cli/azure/network/vnet/subnet#create) | Crée un sous-réseau principal. |
| [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) | Associe les groupes de sécurité réseau toosubnets. |
| [az network public-ip create](/cli/azure/network/public-ip#create) | Crée un Bonjour de tooaccess adresse IP publique machine virtuelle à partir de hello Internet. |
| [az network nic create](/cli/azure/network/nic#create) | Crée des interfaces réseau virtuelles et les attacher à des sous-réseaux du réseau virtuel toohello frontaux et principaux. |
| [az network nsg create](/cli/azure/network/nsg#create) | Crée des groupes de sécurité réseau (NSG) qui sont des sous-réseaux frontaux et principaux toohello associé. |
| [az network nsg rule create](/cli/azure/network/nsg/rule#create) |Crée des règles de groupe de sécurité réseau autoriser ou bloquent des sous-réseaux toospecific de ports spécifiques. |
| [az vm create](/cli/azure/vm#create) | Crée des machines virtuelles et attache un tooeach de carte réseau virtuelle. Cette commande spécifie également hello machine virtuelle image toouse et les informations d’identification administratives. |
| [az group delete](/cli/azure/group#delete) | Supprime un groupe de ressources, ainsi que toutes ses ressources. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](/cli/azure/overview).

Vous trouverez des exemples de script CLI mise en réseau supplémentaires dans hello [documentation de vue d’ensemble de la mise en réseau Azure](../cli-samples.md)
