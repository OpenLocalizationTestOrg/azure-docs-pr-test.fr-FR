---
title: "exemple de script CLI aaaAzure - acheminer le trafic via un matériel de réseau virtuel | Documents Microsoft"
description: "Exemple de script Azure CLI - Acheminer le trafic via une appliance virtuelle réseau de pare-feu."
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
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a>Acheminer le trafic via une appliance virtuelle réseau

Cet exemple de script permet de créer un réseau virtuel avec des sous-réseaux frontaux et principaux. Il crée également un ordinateur virtuel IP le trafic tooroute activé entre deux sous-réseaux de hello. Après avoir exécuté le script de hello, vous pouvez déployer un logiciel réseau, telle qu’une application de pare-feu, toohello machine virtuelle.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>Exemple de script


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

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
| [az network subnet create](/cli/azure/network/vnet/subnet#create) | Crée des sous-réseaux principaux et DMZ. |
| [az network public-ip create](/cli/azure/network/public-ip#create) | Crée un Bonjour de tooaccess adresse IP publique machine virtuelle à partir de hello Internet. |
| [az network nic create](/cli/azure/network/nic#create) | Crée une interface réseau virtuelle et active le transfert IP pour celle-ci. |
| [az network nsg create](/cli/azure/network/nsg#create) | Crée un groupe de sécurité réseau (NSG). |
| [az network nsg rule create](/cli/azure/network/nsg/rule#create) | Crée des règles de groupe de sécurité réseau qui autorise les ports HTTP et HTTPS entrant toohello machine virtuelle. |
| [az network vnet subnet update](/cli/azure/network/vnet/subnet#update)| Associe hello des groupes de sécurité réseau et toosubnets des tables de routage. |
| [az network route-table create](/cli/azure/network/route-table#create)| Crée une table de routage pour tous les itinéraires. |
| [az network route-table route create](/cli/azure/network/route-table/route#create)| Crée des itinéraires tooroute un trafic entre les sous-réseaux et hello Internet via hello machine virtuelle. |
| [az vm create](/cli/azure/vm#create) | Crée une machine virtuelle et attache hello NIC tooit. Cette commande spécifie également hello machine virtuelle image toouse et les informations d’identification administratives. |
| [az group delete](/cli/azure/group#delete) | Supprime un groupe de ressources, ainsi que toutes ses ressources. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](/cli/azure/overview).

Vous trouverez des exemples de script CLI mise en réseau supplémentaires dans hello [documentation de vue d’ensemble de la mise en réseau Azure](../cli-samples.md)
