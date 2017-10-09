---
title: aaaOverview des configurations hautement disponibles avec les passerelles VPN Azure | Documents Microsoft
description: "Cet article fournit une vue d’ensemble des options de configuration haute disponibilité à l’aide de passerelles VPN Azure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/24/2016
ms.author: yushwang
ms.openlocfilehash: 316293b9ac79645bf9bb9e89fbc4aa8f3eacd209
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="highly-available-cross-premises-and-vnet-to-vnet-connectivity"></a>Configuration haute disponibilité pour la connectivité entre les réseaux locaux et la connectivité entre deux réseaux virtuels
Cet article fournit une vue d’ensemble des options de configuration haute disponibilité dont vous pouvez tirer parti pour la connectivité entre vos réseaux locaux et la connectivité entre deux réseaux virtuels en utilisant des passerelles VPN Azure.

## <a name = "activestandby"></a>À propos de la redondance de passerelle VPN Azure
Chaque passerelle VPN Azure comprend deux instances dans une configuration de type actif / passif. Pour toute une maintenance planifiée ou une interruption non planifiée qui se produit de l’instance active toohello, instance de secours hello serait prendre automatiquement (basculement) et reprendre hello S2S VPN ou des connexions de réseau virtuel à réseau virtuel. passage de Hello entraîne une brève interruption. Pour une maintenance planifiée, la connectivité de hello doit être restaurée dans les 10 secondes too15. Pour les problèmes non planifiés, récupération de la connexion hello sera plus longue, sur 1 too1 minute et demi minutes dans le pire des cas hello. Pour les VPN P2S client connexions toohello passerelle, les connexions P2S hello va être déconnectées et hello utilisateurs doivent tooreconnect à partir d’ordinateurs de client hello.

![Actif / passif](./media/vpn-gateway-highlyavailable/active-standby.png)

## <a name="highly-available-cross-premises-connectivity"></a>Connectivité haute disponibilité entre les réseaux locaux
tooprovide meilleure disponibilité pour votre croisée des connexions locaux, deux options sont disponibles :

* Utilisation de plusieurs périphériques VPN en local
* Utilisation d’une passerelle VPN Azure en mode actif-actif
* Combinaison des deux

### <a name = "activeactiveonprem"></a>Utilisation de plusieurs périphériques VPN en local
Vous pouvez utiliser plusieurs périphériques VPN à partir de votre passerelle locale réseau tooconnect tooyour VPN Azure, comme indiqué dans hello suivant schéma :

![Plusieurs périphériques VPN en local](./media/vpn-gateway-highlyavailable/multiple-onprem-vpns.png)

Cette configuration offre plusieurs tunnels actives à partir de hello même VPN Azure tooyour local passerelles Bonjour même emplacement. Elle comporte certaines exigences et contraintes :

1. Vous avez besoin de toocreate plusieurs connexions VPN de S2S à partir de votre tooAzure de périphériques VPN. Lorsque vous vous connectez plusieurs périphériques VPN à partir de hello tooAzure du réseau local même, vous devez toocreate une passerelle de réseau local pour chaque périphérique VPN et une connexion à partir de votre passerelle de réseau local toohello passerelle VPN Azure.
2. les passerelles de réseau local Hello correspondant tooyour des périphériques VPN doivent avoir des adresses IP publiques uniques Bonjour « GatewayIpAddress » propriété.
3. Cette configuration requiert le protocole BGP. Chaque passerelle de réseau local qui représente un périphérique VPN doit avoir une BGP homologue adresse IP spécifiée dans la propriété « BgpPeerIpAddress » de hello.
4. champ de propriété de préfixe d’adresse Hello dans chaque passerelle de réseau local ne doit pas se chevaucher. Vous devez spécifier hello « BgpPeerIpAddress » dans /32 format CIDR dans le champ de préfixe d’adresse hello, par exemple, 10.200.200.254/32.
5. Vous devez utiliser le protocole BGP tooadvertise hello mêmes préfixes Hello du réseau local même passerelle VPN Azure de tooyour préfixes, et le trafic de hello ne sera transmis via ces tunnels simultanément.
6. Chaque connexion est comptabilisée dans le nombre maximal de hello des tunnels pour votre passerelle VPN Azure, 10 pour Basic et Standard de références (SKU) et 30 pour HighPerformance SKU. 

Dans cette configuration, la passerelle VPN Azure de hello est toujours en mode de type actif / passif, donc hello même comportement du basculement et brève interruption se produira toujours comme décrit [ci-dessus](#activestandby). Mais cette configuration évite les défaillances ou les interruptions sur votre réseau local et sur vos périphériques VPN.

### <a name="active-active-azure-vpn-gateway"></a>Utilisation d’une passerelle VPN Azure en mode actif-actif
Vous pouvez maintenant créer une passerelle VPN Azure dans une configuration actif / actif, où les deux instances de passerelle hello que machines virtuelles établiront que tooyour périphérique VPN sur site, les tunnels VPN de S2S comme illustré hello suivant diagramme :

![Actif/actif](./media/vpn-gateway-highlyavailable/active-active.png)

Dans cette configuration, chaque instance de passerelle Azure aura une adresse IP publique unique, et chaque établit un périphérique VPN IPsec/IKE S2S VPN tunnel tooyour local spécifié dans votre passerelle de réseau local et votre connexion. Notez que les deux tunnels VPN sont en fait partie de hello même connexion. Vous allez toujours besoin tooconfigure votre tooaccept de périphérique VPN local ou établir deux S2S VPN tunnels toothose deux VPN Azure passerelle adresses IP publiques.

Étant donné que les instances de passerelle Azure hello se trouvent dans la configuration active-active, trafic hello à partir de votre réseau virtuel Azure de tooyour local réseau sera répercuté sur les deux tunnels simultanément, même si votre périphérique VPN sur site peut privilégier un tunnel Hello autres. Notez bien que hello même flux TCP ou UDP traverse toujours hello même tunnel ou chemin d’accès, sauf si un événement de maintenance se produit sur une des instances de hello.

Lors d’une maintenance planifiée ou un événement non planifié se produit une instance de passerelle tooone, tunnel d’IPsec hello à partir de cette instance de tooyour local périphérique VPN va être déconnecté. Hello des itinéraires correspondants sur vos périphériques VPN doivent être supprimés ou retirés automatiquement afin que le trafic de hello bascule sur toohello autres tunnel IPsec active. Sur hello côté Azure, passez hello en se produit automatiquement à partir de l’instance active du toohello instance hello affectée.

### <a name="dual-redundancy-active-active-vpn-gateways-for-both-azure-and-on-premises-networks"></a>Double redondance : passerelles VPN de type actif-actif pour Azure et les réseaux locaux
option la plus fiable de Hello est les passerelles toocombine hello actif sur votre réseau et sur Azure, comme indiqué dans le schéma hello ci-dessous.

![Double redondance](./media/vpn-gateway-highlyavailable/dual-redundancy.png)

Ici vous créez et configurer la passerelle VPN Azure de hello dans une configuration actif / actif et créez deux passerelles de réseau local et deux connexions pour vos deux locale des appareils VPN comme décrit ci-dessus. résultat de Hello est une connectivité de maille pleine de 4 tunnels IPsec entre votre réseau virtuel Azure et votre réseau local.

Toutes les passerelles et les tunnels sont actifs en hello côté Azure, pour que le trafic de hello soient réparties entre tous les 4 tunnels simultanément, bien que chaque TCP ou UDP de flux sera à nouveau suivi hello tunnel même ou de chemin d’accès de bienvenue côté Azure. Même si en répartissant le trafic de hello, vous constaterez légèrement meilleur débit sur des tunnels IPsec hello, hello principal objectif de cette configuration est pour la haute disponibilité. Et en raison de la nature statistique de toohello de propagation de hello, il est mesure de hello tooprovide difficile sur le trafic d’application de quelle manière les différentes conditions affectent le débit hello.

Cette topologie nécessite deux passerelles de réseau local et de la paire de hello toosupport deux connexions de périphériques VPN sur site et BGP est requis tooallow hello deux connexions toohello même réseau local. Ces exigences sont même hello comme hello [ci-dessus](#activeactiveonprem). 

## <a name="highly-available-vnet-to-vnet-connectivity-through-azure-vpn-gateways"></a>Connectivité haute disponibilité entre deux réseaux virtuels via les passerelles VPN Azure
Hello même configuration actif-actif peut également appliquer les connexions réseau à tooAzure. Vous pouvez créer des passerelles VPN actif pour les deux réseaux virtuels et les connecter hello tooform ensemble complète même maillage connectivité de 4 tunnels entre hello deux réseaux virtuels, comme indiqué dans hello diagramme ci-dessous :

![Connexion entre deux réseaux virtuels](./media/vpn-gateway-highlyavailable/vnet-to-vnet.png)

Cela garantit une paire de tunnels entre deux réseaux virtuels hello pour tous les événements de maintenance planifiée, offrant une meilleure disponibilité existent toujours. Bien que hello même topologie pour la connectivité entre différents locaux requiert deux connexions, topologie de réseau virtuel à réseau virtuel hello ci-dessus devez qu’une seule connexion pour chaque passerelle. En outre, BGP est facultatif, sauf si le routage de transit sur hello réseau à connexion est requis.

## <a name="next-steps"></a>Étapes suivantes
Consultez [configuration des passerelles VPN actif pour entre différents locaux et les connexions de réseau à](vpn-gateway-activeactive-rm-powershell.md) pour les étapes tooconfigure actif entre différents locaux et les connexions au réseau.

