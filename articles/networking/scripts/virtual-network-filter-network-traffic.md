---
title: "Exemple de script Azure CLI - Filtrer le trafic réseau de machine virtuelle | Microsoft Docs"
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
ms.openlocfilehash: 68ee013cff4e0be15af30239e0314f779f50177a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a>Filtrer le trafic réseau de machine virtuelle entrant et sortant

Cet exemple de script permet de créer un réseau virtuel avec des sous-réseaux frontaux et principaux. Le trafic réseau entrant vers le sous-réseau frontal est limité à HTTP, HTTPS et SSH, tandis que le trafic sortant vers Internet à partir du sous-réseau principal n’est pas autorisé. Après avoir exécuté le script, vous disposerez d’une machine virtuelle avec deux cartes réseau. Chacune est connectée à un sous-réseau différent.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filtrer le trafic réseau de machine virtuelle")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise les commandes suivantes pour créer un groupe de ressources, un réseau virtuel et les groupes de sécurité réseau. Chaque commande de la table renvoie à une documentation spécifique.

| Commande | Remarques |
|---|---|
| [az group create](/cli/azure/group#create) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [az network vnet create](/cli/azure/network/vnet#create) | Crée un réseau virtuel et un sous-réseau frontal Azure. |
| [az network subnet create](/cli/azure/network/vnet/subnet#create) | Crée un sous-réseau principal. |
| [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) | Associe les groupes de sécurité réseau à des sous-réseaux. |
| [az network public-ip create](/cli/azure/network/public-ip#create) | Crée une adresse IP publique pour accéder à la machine virtuelle à partir d’Internet. |
| [az network nic create](/cli/azure/network/nic#create) | Crée des interfaces réseau virtuelles et les attache aux sous-réseaux frontaux et principaux du réseau virtuel. |
| [az network nsg create](/cli/azure/network/nsg#create) | Crée des groupes de sécurité réseau (NSG) associés aux sous-réseaux frontaux et principaux. |
| [az network nsg rule create](/cli/azure/network/nsg/rule#create) |Crée des règles NSG qui autorisent ou bloquent des ports spécifiques sur des sous-réseaux donnés. |
| [az vm create](/cli/azure/vm#create) | Crée des machines virtuelles et associe une carte d’interface réseau à chacune d’elles. Cette commande spécifie également l’image de machine virtuelle à utiliser ainsi que les informations d’identification d’administration. |
| [az group delete](/cli/azure/group#delete) | Supprime un groupe de ressources, ainsi que toutes ses ressources. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](/cli/azure/overview).

Vous pouvez trouver des exemples supplémentaires de scripts CLI de mise en réseau dans la [documentation Vue d’ensemble de la mise en réseau Azure](../cli-samples.md).