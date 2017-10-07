---
title: "Vue d’ensemble de la passerelle VPN : Créer les connexions VPN intersite les réseaux virtuels tooAzure | Documents Microsoft"
description: "Cette vue d’ensemble de la passerelle VPN explique hello façons tooconnect tooAzure réseaux virtuels à l’aide d’une connexion VPN sur Internet de hello. Des diagrammes de configuration de connexion de base sont inclus."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 2358dd5a-cd76-42c3-baf3-2f35aadc64c8
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/05/2017
ms.author: cherylmc
ms.openlocfilehash: 899270734270632a5b12d56021c924e977725a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway"></a>À propos de la passerelle VPN

Une passerelle VPN est un type de passerelle de réseau virtuel qui envoie le trafic chiffré sur une tooan connexion publique emplacement local. Vous pouvez également utiliser des VPN passerelles toosend chiffré le trafic entre les réseaux virtuels Azure sur le réseau de Microsoft hello. toosend chiffré le trafic réseau entre votre réseau virtuel Azure et votre site local, vous devez créer une passerelle VPN pour votre réseau virtuel.

Chaque réseau virtuel peut avoir qu’une seule passerelle VPN, toutefois, vous pouvez créer plusieurs connexions toohello même passerelle VPN. La configuration d’une connexion sur plusieurs sites en est un bon exemple. Lorsque vous créez plusieurs connexions toohello même passerelle VPN, tous les tunnels VPN, y compris les Point-to-Site VPN, la bande passante hello partage qui n’est disponible pour la passerelle de hello.

### <a name="whatis"></a>Qu’est-ce qu’une passerelle de réseau virtuel ?

Une passerelle de réseau virtuel est composée de deux ou plusieurs ordinateurs virtuels qui sont déployés tooa de sous-réseau spécifique appelé hello GatewaySubnet. Hello machines virtuelles qui se trouvent dans hello GatewaySubnet sont créés lorsque vous créez la passerelle de réseau virtuel hello. Ordinateurs virtuels de passerelle de réseau virtuel sont des tables de routage configuré toocontain et passerelle toohello spécifique de services. Vous ne pouvez pas configurer directement hello machines virtuelles qui font partie de la passerelle de réseau virtuel hello et vous ne devez jamais déployer des ressources supplémentaires toohello GatewaySubnet.

Lorsque vous créez une passerelle de réseau virtuel à l’aide du type de passerelle hello « Vpn », il crée un type spécifique de la passerelle de réseau virtuel qui chiffre le trafic ; une passerelle VPN. Une passerelle VPN peut prendre jusqu'à too45 minutes toocreate. En effet, hello machines virtuelles de passerelle VPN de hello sont en cours toohello déployé GatewaySubnet et configuré avec les paramètres hello que vous avez spécifié. Hello SKU de passerelle que vous sélectionnez détermine hello plus puissant sont des machines virtuelles.

## <a name="gwsku"></a>SKU de passerelle

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

## <a name="configuring"></a>Configuration d’une passerelle VPN

Une connexion par passerelle VPN s’appuie sur plusieurs ressources qui sont configurées avec des paramètres spécifiques. La plupart des ressources de hello peut être configurée séparément, bien qu’ils doivent être configurés dans un certain ordre, dans certains cas.

### <a name="settings"></a>Paramètres

les paramètres de Hello que vous avez choisi pour chaque ressource sont critiques toocreating une connexion réussie. Pour plus d’informations sur les ressources et paramètres spécifiques pour la passerelle VPN, consultez [À propos des paramètres de passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md). Hello contient toohelp informations comprendre de types de passerelle, types de VPN, les types de connexion, les sous-réseaux de passerelle, passerelles de réseau local et divers autres paramètres de ressource que vous pourriez vouloir tooconsider.

### <a name="tools"></a>Outils de déploiement

Vous pouvez commencer à créer et configurer des ressources à l’aide d’un outil de configuration, par exemple hello portail Azure. Vous pouvez ultérieurement décider tooswitch tooanother outil, tels que PowerShell tooconfigure des ressources supplémentaires, ou modifier des ressources existantes, le cas échéant. Actuellement, vous ne pouvez pas configurer chaque ressource et le paramètre de ressource Bonjour portail Azure. instructions Hello dans les articles hello pour chaque topologie de connexion spécifient quand un outil de configuration spécifique est nécessaire. 

### <a name="models"></a>Modèle de déploiement

Lorsque vous configurez une passerelle VPN, étapes hello que suivre dépendent de modèle de déploiement hello que vous avez utilisé toocreate votre réseau virtuel. Par exemple, si vous avez créé votre réseau virtuel à l’aide du modèle de déploiement classique de hello, vous utilisez les instructions hello et obtenir des instructions pour le déploiement classique de hello toocreate de modèle et configurer les paramètres de votre passerelle VPN. Pour plus d’informations sur les modèles de déploiement, voir [Comprendre les modèles de déploiement Resource Manager et de déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="diagrams"></a>Diagrammes de topologie de connexion

Il est important tooknow que différentes configurations sont disponibles pour les connexions de passerelle VPN. Vous devez toodetermine configuration qui correspond à vos besoins. Dans les sections de hello ci-dessous, vous pouvez afficher des diagrammes de topologie et les informations sur hello suivant des connexions VPN de passerelle : hello les sections suivantes contiennent des tables qui répertorient :

* Modèle de déploiement disponible
* Outils de configuration disponibles
* Liens directement l’article tooan, s’il est disponible

Utilisez hello diagrammes et les descriptions toohelp hello Sélectionnez connexion topologie toomatch vos besoins. Hello diagrammes montrent hello topologies de ligne de base principale, mais il est possible de toobuild configurations plus complexes à l’aide de diagrammes de hello comme indication.

## <a name="s2smulti"></a>Site à site et multi-sites (tunnel VPN IPsec/IKE)

### <a name="S2S"></a>Site à site

Une connexion par passerelle VPN site à site (S2S) est une connexion via un tunnel VPN IPsec/IKE (S2S ou IKEv1). Une connexion S2S nécessite un VPN périphérique local qui a un tooit d’adresse IP publique et ne se trouve pas derrière un NAT. Les connexions S2S peuvent être utilisées pour les configurations hybrides et entre différents locaux.   

![Exemple de connexion site à site de passerelle VPN Azure](./media/vpn-gateway-about-vpngateways/vpngateway-site-to-site-connection-diagram.png)

### <a name="Multi"></a>Multi-sites

Ce type de connexion est une variation de hello connexion Site à Site. Vous créez plusieurs connexions VPN à partir de votre passerelle de réseau virtuel, en général, la connexion toomultiple sites locaux. Lorsque vous travaillez avec plusieurs connexions, vous devez utiliser un type de VPN basé sur l’itinéraire (équivalent d’une passerelle dynamique pour les réseaux virtuels classiques). Étant donné que chaque réseau virtuel peut avoir uniquement une passerelle VPN, toutes les connexions via la passerelle de hello partagent la bande passante disponible de hello. Cela est souvent appelé connexion « multi-sites ».

![Exemple de connexion multisites de passerelle VPN Azure](./media/vpn-gateway-about-vpngateways/vpngateway-multisite-connection-diagram.png)

### <a name="deployment-models-and-methods-for-site-to-site-and-multi-site"></a>Modèles et méthodes de déploiement pour les connexions site à site et multi-sites

[!INCLUDE [vpn-gateway-table-site-to-site](../../includes/vpn-gateway-table-site-to-site-include.md)]

## <a name="P2S"></a>Point à site (VPN sur SSTP)

Une passerelle VPN de Point-to-Site (P2S) vous permet de créer un réseau virtuel tooyour de connexion sécurisée à partir d’un ordinateur client. Connexions de point-to-Site VPN sont utiles lorsque vous souhaitez tooconnect tooyour réseau virtuel à partir d’un emplacement distant, par exemple lorsque vous sont télétravailleurs d’accueil ou d’une conférence. Un VPN P2S est également un toouse solution utile au lieu d’un VPN de Site à Site lorsque vous avez seulement quelques clients nécessitant tooconnect tooa réseau virtuel. 

Contrairement aux connexions S2S, les connexions P2S ne nécessitent pas d’adresse IP publique locale ni de périphérique VPN. Les connexions P2S peuvent être utilisées avec les connexions via S2S hello même passerelle VPN, tant que tous les hello configuration requise pour les connexions sont compatibles.

P2S utilise hello Tunneling protocole SSTP (Secure Socket), qui est un protocole de VPN basée sur le protocole SSL. Un réseau VPN P2S est établie en le démarrant à partir de l’ordinateur client de hello.

![Exemple de connexion de point à site de passerelle VPN Azure](./media/vpn-gateway-about-vpngateways/vpngateway-point-to-site-connection-diagram.png)

### <a name="deployment-models-and-methods-for-point-to-site"></a>Méthodes et modèles de déploiement pour les connexions point à site

[!INCLUDE [vpn-gateway-table-point-to-site](../../includes/vpn-gateway-table-point-to-site-include.md)]

## <a name="V2V"></a>Connexions de réseau virtuel à réseau virtuel (tunnel VPN IPsec/IKE)

Connexion d’un réseau virtuel de réseau virtuel tooanother (au réseau) est tooconnecting comme emplacement d’un site réseau virtuel tooan local. Les deux types de connectivité utilisent un tooprovide de passerelle VPN un tunnel sécurisé utilisant IPsec/IKE. Vous pouvez même combiner une communication de réseau virtuel à réseau virtuel avec des configurations de connexion multi-sites. Vous établissez ainsi des topologies réseau qui combinent une connectivité entre différents locaux et une connectivité entre différents réseaux virtuels.

Hello vous connectez des réseaux virtuels peut être :

* Bonjour identiques ou différentes régions
* Bonjour identiques ou différents abonnements 
* Bonjour modèles de déploiement identiques ou différents

![Exemple de connexion tooVNet réseau virtuel de passerelle VPN Azure](./media/vpn-gateway-about-vpngateways/vpngateway-vnet-to-vnet-connection-diagram.png)

### <a name="connections-between-deployment-models"></a>Connexions entre modèles de déploiement

Azure propose actuellement deux modèles de déploiement : le modèle classique et le modèle Resource Manager. Si vous utilisez Azure depuis un certain temps, vous avez probablement des machines virtuelles et des rôles d’instance Azure exécutés dans un réseau virtuel classique. Il est possible que vos nouvelles machines virtuelles et instances de rôle s’exécutent dans un réseau virtuel créé dans Resource Manager. Vous pouvez créer une connexion entre hello réseaux virtuels tooallow les ressources hello dans un réseau virtuel toocommunicate, directement des ressources dans un autre.

### <a name="vnet-peering"></a>Homologation de réseaux virtuels

Vous pouvez être en mesure de toouse d’homologation toocreate votre connexion, de réseau virtuel tant que votre réseau virtuel répond à certaines exigences. L’homologation de réseau virtuel n’utilise pas de passerelle de réseau virtuel. Pour plus d’informations, consultez l’article [Homologation de réseaux virtuels](../virtual-network/virtual-network-peering-overview.md).

### <a name="deployment-models-and-methods-for-vnet-to-vnet"></a>Modèles et méthodes de déploiement pour les connexions de réseau virtuel à réseau virtuel

[!INCLUDE [vpn-gateway-table-vnet-to-vnet](../../includes/vpn-gateway-table-vnet-to-vnet-include.md)]

## <a name="ExpressRoute"></a>ExpressRoute (connexion privée dédiée)

Microsoft Azure ExpressRoute vous permet d’étendre vos réseaux locaux dans hello cloud de Microsoft sur une connexion privée dédiée facilitée par un fournisseur de connectivité. Grâce à ExpressRoute, vous pouvez établir des services de cloud computing tooMicrosoft de connexions, tels que Microsoft Azure, Office 365, CRM Online. La connectivité peut provenir d'un réseau universel (IP VPN), d’un réseau Ethernet point à point ou d’une interconnexion virtuelle via un fournisseur de connectivité dans un centre de colocalisation.

Les connexions ExpressRoute ne sont pas établies via hello Internet public. Ainsi, toooffer de connexions ExpressRoute plus la fiabilité, débits plus importants, latences moindres et une sécurité accrue par rapport aux connexions classiques sur Internet de hello.

Une connexion ExpressRoute n’utilise pas de passerelle VPN, mais une passerelle de réseau virtuel dans le cadre de sa configuration requise. Dans une connexion ExpressRoute, la passerelle de réseau virtuel hello est configuré avec le type de passerelle hello « ExpressRoute », plutôt que « Vpn ». Pour plus d’informations sur ExpressRoute, consultez hello [présentation technique d’ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="coexisting"></a>Coexistence de connexions ExpressRoute et de site à site

ExpressRoute est une connexion directe à partir de votre réseau étendu dédiée (pas sur hello Internet public) tooMicrosoft Services, y compris Azure. Site-à-Site VPN transitent au format chiffré via hello du trafic Internet public. En cours tooconfigure en mesure de connexions VPN de Site à Site et ExpressRoute pour le même réseau virtuel hello présente plusieurs avantages.

Vous pouvez configurer un VPN de Site à Site comme un chemin d’accès sécurisé de basculement pour ExpressRoute, ou utiliser des VPN de Site à Site tooconnect toosites qui ne sont pas partie de votre réseau, mais qui sont connectés via ExpressRoute. Notez que cette configuration nécessite deux passerelles de réseau virtuel pour hello même réseau virtuel, à l’aide hello du type de passerelle « Vpn » et à l’aide de type de passerelle hello « ExpressRoute » hello.

![Exemple de connexions coexistantes ExpressRoute et passerelle VPN](./media/vpn-gateway-about-vpngateways/expressroute-vpngateway-coexisting-connections-diagram.png)

### <a name="deployment-models-and-methods-for-s2s-and-expressroute"></a>Méthodes et modèles de déploiement pour les connexions S2S et ExpressRoute

[!INCLUDE [vpn-gateway-table-coexist](../../includes/vpn-gateway-table-coexist-include.md)]

## <a name="pricing"></a>Tarification

[!INCLUDE [vpn-gateway-about-pricing-include](../../includes/vpn-gateway-about-pricing-include.md)]

Pour plus d’informations sur les références de passerelle pour la passerelle VPN, consultez [Références (SKU) de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

## <a name="faq"></a>Forum Aux Questions

Pour les questions fréquemment posées sur la passerelle VPN, consultez hello [Forum aux questions de la passerelle VPN](vpn-gateway-vpn-faq.md).

## <a name="next-steps"></a>Étapes suivantes

- Planifiez votre configuration de passerelle VPN. Consultez [Planification et conception de la passerelle VPN](vpn-gateway-plan-design.md).
- Hello de vue [Forum aux questions de la passerelle VPN](vpn-gateway-vpn-faq.md) pour plus d’informations.
- Hello de vue [abonnement et les limites de service](../azure-subscription-service-limits.md#networking-limits).
- En savoir plus sur certaines des hello autre clé [fonctionnalités de réseau](../networking/networking-overview.md) de Azure.
