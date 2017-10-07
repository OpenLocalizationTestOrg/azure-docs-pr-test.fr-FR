---
title: aaaOverview de protocole BGP avec les passerelles VPN Azure | Documents Microsoft
description: "Cet article fournit une vue d’ensemble du protocole BGP avec les passerelles VPN Azure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: f8c3985c-c128-4f34-835c-0e88742bf36e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: ced3f77ecd791c84fb72b96447e839be3bf94846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a>Vue d’ensemble du protocole BGP avec les passerelles VPN Azure
Cet article fournit une vue d’ensemble de la prise en charge du protocole BGP (Border Gateway Protocol) avec les passerelles VPN Azure.

BGP est hello protocole de routage standard couramment utilisé dans hello Internet tooexchange routage et l’accessibilité des informations entre deux ou plusieurs réseaux. Lorsque BGP utilisé dans le contexte de hello de réseaux virtuels Azure, Active les passerelles VPN Azure hello et vos périphériques VPN local, appelés homologues BGP ou voisins, tooexchange « achemine » qui vous informe les deux passerelles sur la disponibilité de hello et l’accessibilité pour les les préfixes toogo via des passerelles de hello ou routeurs impliqués. Protocole BGP peut également activer le routage de transit entre plusieurs réseaux en propageant les itinéraires une passerelle BGP apprend à partir d’un tooall d’homologue BGP autres homologues BGP. 

## <a name="why-use-bgp"></a>Pourquoi utiliser le protocole BGP ?
Le protocole BGP est une fonctionnalité facultative que vous pouvez utiliser avec les passerelles VPN Azure basées sur des itinéraires. Vous devez également vous assurer de que vos périphériques VPN locale prend en charge BGP avant d’activer la fonctionnalité de hello. Vous pouvez continuer toouse les passerelles VPN Azure et vos périphériques VPN de localement sans BGP. Il s’agit de hello équivalente à l’aide d’itinéraires statiques (sans BGP) *et* à l’aide d’un routage dynamique avec protocole BGP entre les réseaux Azure.

Le protocole BGP offre plusieurs avantages et de nouvelles fonctionnalités :

### <a name="support-automatic-and-flexible-prefix-updates"></a>Prise en charge de mises à jour de préfixe automatiques et flexibles
Avec protocole BGP, vous devez uniquement toodeclare un préfixe minimale tooa spécifique de l’homologue BGP sur tunnel d’IPsec S2S VPN hello. Il peut être aussi petit que le préfixe d’un hôte (/ 32) de hello adresse IP l’homologue BGP de votre périphérique VPN sur site. Vous pouvez contrôler qui local préfixes réseau que vous souhaitez tooadvertise tooAzure tooallow tooaccess de votre réseau virtuel Azure.

Vous pouvez également publier un préfixe plus étendu, qui peut inclure certains préfixes d’adresses de votre réseau virtuel, par exemple un large espace d’adressage IP privé (par exemple, 10.0.0.0/8). Notez bien que les préfixes hello ne peut pas être identiques à l’un des préfixes d’espaces de votre réseau virtuel. Ces préfixes de réseau virtuel itinéraires tooyour identiques seront rejetées.

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a>Prise en charge de plusieurs tunnels entre un réseau virtuel et un site local avec basculement automatique basé sur le protocole BGP
Vous pouvez établir plusieurs connexions entre votre réseau virtuel Azure et vos périphériques VPN de local Bonjour même emplacement. Cette fonctionnalité fournit plusieurs tunnels (chemins d’accès) entre deux réseaux de hello dans une configuration actif / actif. Si un des tunnels de hello est déconnecté, les itinéraires correspondants hello seront retirées via BGP et le trafic de hello déplace automatiquement les tunnels toohello restantes.

Hello suivant schéma montre un exemple simple de ce programme d’installation à haute disponibilité :

![Plusieurs chemins actifs](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a>Prise en charge du routage de transit entre vos réseaux locaux et plusieurs réseaux virtuels Azure
Protocole BGP permet à plusieurs passerelles toolearn et propager les préfixes à partir de différents réseaux, si elles sont connectés directement ou indirectement. Ceci peut permettre un routage de transit avec des passerelles VPN Azure entre vos sites locaux ou sur plusieurs réseaux virtuels Azure.

Hello diagramme suivant montre un exemple de topologie de cascade avec plusieurs chemins d’accès qui peuvent transiter le trafic entre hello deux réseaux locaux via des passerelles VPN Azure dans hello Microsoft Networks :

![Transit sur plusieurs tronçons](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a>Forum Aux Questions sur le protocole BGP
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a>Étapes suivantes
Consultez [mise en route avec protocole BGP sur les passerelles VPN Azure](vpn-gateway-bgp-resource-manager-ps.md) pour les étapes tooconfigure BGP pour les connexions de réseau virtuel à réseau virtuel et votre entre différents locaux.

