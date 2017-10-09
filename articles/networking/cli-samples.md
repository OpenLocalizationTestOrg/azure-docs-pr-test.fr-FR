---
title: "aaaAzure CLI échantillons | Documents Microsoft"
description: "Exemples d’interface de ligne de commande Azure"
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: kumud
ms.openlocfilehash: 8001b7e72480cfd0122325f7fb81c32aaad072d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-networking"></a>Exemples d’interface de ligne de commande Azure pour la mise en réseau

Hello tableau suivant inclut des liens toobash scripts créés à l’aide de hello CLI d’Azure.

| | |
|-|-|
|**Connectivité entre les ressources Azure**||
| [Créer un réseau virtuel pour les applications multiniveau](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | Crée un réseau virtuel avec des sous-réseaux frontaux et principaux. Sous-réseau de trafic toohello frontal est limitée tooHTTP et SSH, lors du trafic toohello sous-réseau principal est limitée tooMySQL, port 3306. |
| [Homologuer deux réseaux virtuels](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | Crée et connecte deux réseaux virtuels Bonjour même région. |
| [Acheminer le trafic via une appliance virtuelle réseau](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | Crée un réseau virtuel avec les sous-réseaux des serveurs frontaux et principaux et un ordinateur virtuel qui tooroute en mesure de trafic entre les sous-réseaux de hello deux. |
| [Filtrer le trafic réseau de machine virtuelle entrant et sortant](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | Crée un réseau virtuel avec des sous-réseaux frontaux et principaux. Le trafic du réseau entrant toohello le sous-réseau frontal est limitée tooHTTP, SSH et HTTPS. Le trafic sortant toohello Internet à partir du sous-réseau principal de hello n’est pas autorisée. |
|**Équilibrage de charge et direction de trafic**||
| [Charger tooVMs le trafic de solde pour la haute disponibilité](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | Crée plusieurs machines virtuelles dans une configuration haute disponibilité avec équilibrage de charge. |
| [Équilibrer la charge de plusieurs sites web sur des machines virtuelles](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | Crée deux machines virtuelles avec plusieurs configurations IP, tooan jointe à haute disponibilité Azure, accessible via un équilibrage de charge Azure. |
| [Diriger le trafic dans plusieurs régions pour une haute disponibilité des applications](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  Crée deux plans App Service, deux applications web, un profil Traffic Manager et deux points de terminaison Traffic Manager. |
| | |
