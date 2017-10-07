---
title: "Planification et conception des connexions entre les systèmes locaux : passerelle VPN Azure | Microsoft Docs"
description: "En savoir plus sur la planification et la conception de la passerelle VPN pour les connexions entre locaux, hybrides et entre réseaux virtuels"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a>Planification et conception de la passerelle VPN

La planification et la conception de vos configurations intersites et entre réseaux virtuels peuvent être simples ou complexes, selon vos besoins de mise en réseau. Cet article présente diverses considérations relatives à la conception et à la planification de base.

## <a name="planning"></a>Planification

### <a name="compare"></a>Options de connectivité intersite

Si vous souhaitez tooconnect votre site sur les sites en toute sécurité tooa des réseaux virtuels, que vous disposez de trois façons différentes toodo donc : Site à Site, Point-to-Site et ExpressRoute. Comparer les connexions entre différents sites hello qui sont disponibles. option Hello que vous choisissez peut dépendre d’un certain nombre d’éléments, tels que :

* Quel est le type de débit requis par votre solution ?
* Voulez-vous vraiment toocommunicate sur hello Internet public via VPN sécurisée, ou via une connexion privée ?
* Avez-vous un toouse de disponible d’adresse IP publique ?
* Envisagez-vous toouse un périphérique VPN ? Si tel est le cas, est-il compatible ?
* Ne voulez-vous connecter qu’un petit nombre d’ordinateurs, ou souhaitez-vous mettre en place une connexion permanente pour votre site ?
* Quel type de passerelle VPN est requis pour la solution de hello souhaité toocreate ?
* Quelle référence SKU de passerelle devez-vous utiliser ?

### <a name="planningtable"></a>Tableau de planification

Hello tableau suivant peut vous aider à déterminer hello meilleure option de connectivité de votre solution.

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <a name="gwsku"></a>SKU de passerelle

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <a name="wf"></a>Flux de travail

Hello liste suivante indique hello des flux de travail courant pour la connectivité du cloud :

1. Conception et planification de que votre adresse de hello connectivité topologie et de la liste des espaces pour tous les réseaux vous souhaitez tooconnect.
2. Créez un réseau virtuel Azure. 
3. Créer une passerelle VPN de réseau virtuel de hello.
4. Créez et configurez des connexions tooon des réseaux locaux ou autres réseaux virtuels (si nécessaire).
5. Créez et configurez une connexion Point-à-Site pour votre passerelle VPN Azure (en fonction des besoins).

## <a name="design"></a>Conception
### <a name="topologies"></a>Topologies de connexion

Commencez par examiner les diagrammes hello Bonjour [sur la passerelle du VPN](vpn-gateway-about-vpngateways.md) l’article. article de Hello contient des diagrammes de base, les modèles de déploiement hello pour chaque topologie et les outils de déploiement disponibles hello vous pouvez utiliser toodeploy votre configuration.

### <a name="designbasics"></a>Concepts de base

Hello les sections suivantes présentent les principes fondamentaux de passerelle hello VPN. 

#### <a name="servicelimits"></a>Limites des services de mise en réseau

Faites défiler hello tables tooview [limites des services de mise en réseau](../azure-subscription-service-limits.md#networking-limits). limites de Hello répertoriés peuvent affecter votre conception.

#### <a name="subnets"></a>À propos des sous-réseaux

Lorsque vous créez des connexions, vous devez prendre en compte vos plages de sous-réseau. Il ne peut pas avoir de chevauchement entre des plages d’adresses de sous-réseau. Un sous-réseau qui se chevauchent est lorsqu’un emplacement local ou de réseau virtuel contient hello contient du même espace d’adressage hello autre emplacement. Cela signifie que vous avez besoin des ingénieurs de votre réseau pour votre toocarve de réseaux sur site local à une plage pour vous toouse pour votre adresse IP Azure/sous-réseaux de l’espace d’adressage. Vous avez besoin d’espace d’adressage qui n’est pas utilisé sur le réseau de site local hello.

Il est également important d’éviter le chevauchement des sous-réseaux lorsque vous travaillez avec des connexions entre réseaux virtuels. Si vos sous-réseaux se chevauchent et une adresse IP existe dans l’envoi de hello et la destination des réseaux virtuels, les connexions réseau à échouent. Azure ne peut pas acheminer hello données toohello autre réseau virtuel comme adresse de destination hello fait partie de hello envoi réseau virtuel.

Les passerelles VPN nécessitent un sous-réseau spécifique appelé sous-réseau de passerelle. Tous les sous-réseaux de passerelle doivent être nommés GatewaySubnet toowork correctement. Veillez tooname pas votre sous-réseau de passerelle, un autre nom et ne pas déployer des machines virtuelles ou n’importe quel autre sous-réseau de passerelle toohello. Voir [Sous-réseaux de passerelle](vpn-gateway-about-vpn-gateway-settings.md#gwsub).

#### <a name="local"></a>À propos des passerelles de réseau local

passerelle de réseau local Hello fait généralement référence d’emplacement de site tooyour. Dans le modèle de déploiement classique de hello, passerelle de réseau local hello est tooas auxquels un Site réseau Local. Lorsque vous configurez une passerelle de réseau local, vous lui donnez un nom, spécifiez hello adresse IP publique du périphérique VPN hello localement et les préfixes d’adresse hello qui se trouvent dans un emplacement local de hello. Azure examine les préfixes d’adresse de destination hello pour le trafic réseau, consulte configuration hello que vous avez spécifié pour la passerelle de réseau local hello et route les paquets en conséquence. Vous pouvez modifier les préfixes d’adresse hello en fonction des besoins. Pour plus d’informations, voir [Passerelles de réseau local](vpn-gateway-about-vpn-gateway-settings.md#lng).

#### <a name="gwtype"></a>À propos des types de passerelles

Il est essentiel de sélection du type de passerelle est correct de hello pour votre topologie. Si vous sélectionnez un type incorrect hello, votre passerelle ne fonctionne pas correctement. type de passerelle Hello spécifie comment la passerelle hello elle-même se connecte et est un paramètre de configuration requise pour le modèle de déploiement du Gestionnaire de ressources hello.

types de passerelle Hello sont :

* Vpn
* ExpressRoute

#### <a name="connectiontype"></a>À propos des types de connexions

Chaque configuration nécessite un type de connexion spécifique. types de connexion Hello sont :

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

#### <a name="vpntype"></a>À propos des types de VPN

Chaque configuration nécessite un type de VPN spécifique. Si vous combinez deux configurations, telles que la création d’une connexion Site à Site et un toohello de connexion de Point-to-Site même réseau virtuel, vous devez utiliser un type VPN qui satisfait les exigences de connexion.

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

Hello tableaux suivants indiquent les type de VPN hello comme il mappe tooeach configuration de la connexion. Vérifiez que hello type VPN pour votre configuration de hello correspond à la passerelle que vous souhaitez toocreate. 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <a name="devices"></a>Périphériques VPN et connexions de site à site

connexion tooconfigure un Site à Site, quel que soit le modèle de déploiement, vous devez hello éléments suivants :

* un périphérique VPN compatible avec les passerelles VPN Azure
* une adresse IPv4 publique qui ne se trouve pas derrière un NAT

Vous devez être toohave configurer votre périphérique VPN ou demandez à une personne qui peut configurer le périphérique de hello pour vous.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="forcedtunnel"></a>Envisager le routage avec tunneling forcé

Dans la plupart des configurations, vous pouvez configurer le tunneling forcé. Forcé tunneling permet de rediriger ou de « forcer » tous les Internet liées au trafic tooyour arrière local emplacement via un tunnel VPN de Site à Site pour l’inspection et d’audit. Il s’agit d’une condition de sécurité critique pour la plupart des stratégies informatiques d’entreprise. 

Sans tunneling forcé, le trafic Internet à partir de vos machines virtuelles dans Azure traverse toujours l’infrastructure réseau Azure directement out toohello Internet, sans hello option tooallow vous tooinspect ou audit du trafic hello. Accès Internet non autorisé peut entraîner la divulgation de tooinformation ou d’autres types de failles de sécurité.

Une connexion de tunneling forcé peut être configurée dans les deux modèles de déploiement et à l’aide de différents outils. Pour plus d’informations, consultez [Configurer un tunneling forcé](vpn-gateway-forced-tunneling-rm.md).

**Diagramme du tunneling forcé**

![Diagramme du tunneling forcé de la passerelle VPN Azure](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a>Étapes suivantes

Consultez hello [Forum aux questions de la passerelle VPN](vpn-gateway-vpn-faq.md) et [sur la passerelle du VPN](vpn-gateway-about-vpngateways.md) articles pour plus d’informations toohelp vous avec votre conception.

Pour plus d’informations sur les paramètres de passerelle spécifiques, voir [À propos des paramètres de la passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md).