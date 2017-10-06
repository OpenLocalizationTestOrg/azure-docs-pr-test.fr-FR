---
title: "aaaFind de tronçon suivant avec Azure réseau observateur du prochain saut - Azure CLI 1.0 | Documents Microsoft"
description: "Cet article décrit comment vous pouvez trouver quel hello de type de tronçon suivant est et à l’aide des adresses ip de tronçon suivant à l’aide de CLI d’Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 54124c051021413695d70ba93c370605abc6ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a>Savoir quel type de tronçon suivant hello est à l’aide de capacité de tronçon suivant hello dans l’Observateur réseau de Azure à l’aide d’Azure CLI 1.0

> [!div class="op_single_selector"]
> - [Portail Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [API REST Azure](network-watcher-check-next-hop-rest.md)

Tronçon suivant est une fonctionnalité de l’Observateur réseau qui offre la possibilité de hello obtenir le type de tronçon suivant hello et l’adresse IP basée sur une machine virtuelle spécifiée. Cette fonctionnalité est utile pour déterminer si le trafic en laissant une machine virtuelle traverse une passerelle, internet ou des réseaux virtuels tooget tooits destination.

Cet article utilise l’interface Azure CLI 1.0 interplateforme, disponible pour Windows, Mac et Linux.

## <a name="before-you-begin"></a>Avant de commencer

Dans ce scénario, vous allez utiliser hello le type de tronçon suivant CLI d’Azure toofind hello et l’adresse IP.

Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau. scénario de Hello suppose également qu’un groupe de ressources avec un ordinateur virtuel valide existe toobe utilisé.

## <a name="scenario"></a>Scénario

scénario de Hello abordée dans cet article utilise le saut suivant, une fonctionnalité de l’Observateur réseau qui recherche le type de tronçon suivant hello et une adresse IP pour une ressource. toolearn en savoir plus sur le tronçon suivant, visitez [vue d’ensemble du tronçon suivant](network-watcher-next-hop-overview.md).


## <a name="get-next-hop"></a>Obtenir le tronçon suivant

Nous appelons hello du tronçon suivant hello tooget `azure netowrk watcher next-hop` applet de commande. Nous transmettons le groupe de ressources de l’Observateur réseau hello applet de commande hello hello NetworkWatcher, l’ordinateur virtuel Id, adresse IP source et adresse IP de destination. Dans cet exemple, adresse IP de destination hello est tooa machine virtuelle dans un autre réseau virtuel. Il existe une passerelle de réseau virtuel entre des réseaux virtuels deux hello. 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
Si hello machine virtuelle possède plusieurs cartes réseau et le transfert IP est activé sur aucun des hello cartes réseau, puis hello paramètre de carte réseau (-i-l’id de la carte réseau) doit être spécifié. Sinon, il est facultatif.

## <a name="review-results"></a>Passer en revue les résultats

Lorsque vous avez terminé, les résultats de hello sont fournies. adresse IP du tronçon suivant Hello est retournée, ainsi que de type hello de ressource, qu'il s’agit.

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

Hello liste suivante présente les valeurs de tronçon suivant actuellement disponibles hello :

**Type de tronçon suivant**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Aucun

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment tooreview vos paramètres de groupe de sécurité réseau par programme en vous rendant sur [NSG audit avec l’Observateur réseau](network-watcher-nsg-auditing-powershell.md)
