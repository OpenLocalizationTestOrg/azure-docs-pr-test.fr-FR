---
title: "équilibrage de charge aaaInternal vue d’ensemble | Documents Microsoft"
description: "Vue d’ensemble de l’équilibreur de charge interne et de ses fonctionnalités. Fonctionne d’un équilibrage de charge pour les points de terminaison internes des scénarios possibles et Azure tooconfigure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a>Présentation de l’équilibrage de charge interne

Contrairement aux hello Internet exposés à équilibrage de charge, équilibreur de charge interne hello (équilibrage de charge interne) dirige le trafic tooresources uniquement à l’intérieur du service de cloud computing hello ou à l’aide de VPN tooaccess hello infrastructure Azure. infrastructure de Hello restreint l’accès toohello à charge équilibrée adresses IP virtuelles (VIP) d’un Service Cloud ou d’un réseau virtuel afin qu’ils ne seront jamais directement exposé tooan Internet point de terminaison. Cela permet la ligne interne de toorun d’applications métier (LOB) dans Azure et accessible à partir de dans le cloud de hello ou à partir des ressources locales.

## <a name="why-you-may-need-an-internal-load-balancer"></a>Pourquoi utiliser un équilibreur de charge interne

L’équilibrage de charge interne (ILB) d’Azure fournit un équilibrage de charge entre les machines virtuelles qui résident dans un service cloud ou un réseau virtuel avec une portée régionale. Pour plus d’informations sur l’utilisation de hello et la configuration de réseaux virtuels avec une portée régionale, consultez [des réseaux virtuels régionaux](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) Bonjour blog Azure. Les réseaux virtuels existants qui ont été configurés pour un groupe d'affinités ne peuvent pas utiliser l'ILB.

Équilibrage de charge interne permet hello les types d’équilibrage de charge suivants :

* Dans un service cloud, à partir de l’ensemble de tooa de machines virtuelles des machines virtuelles qui résident dans hello même service cloud (voir Figure 1).
* Dans un réseau virtuel, à partir d’ordinateurs virtuels dans le jeu de tooa de réseau virtuel hello des machines virtuelles qui résident dans hello même service cloud de hello virtuel réseau (voir Figure 2).
* Pour un réseau virtuel intersite, à partir de l’ensemble de tooa d’ordinateurs locaux des machines virtuelles qui résident dans hello même service cloud de hello virtuel réseau (voir Figure 3).
* Les applications accessibles sur Internet, à plusieurs niveaux dans lequel les couches principales de hello ne sont pas exposés à Internet mais nécessitent équilibrage de charge pour le trafic à partir de la couche de hello sur Internet.
* Équilibrer la charge pour des applications métier (LOB) hébergées dans Azure, sans matériel ou logiciel d'équilibrage de charge supplémentaire. Inclure des serveurs locaux jeu hello d’ordinateurs dont le trafic est à charge équilibrée.

## <a name="internet-facing-multi-tier-applications"></a>Une application multiniveau sur internet

niveau de Hello web possède des points de terminaison exposés à Internet pour les clients Internet et fait partie d’un jeu d’équilibrage de charge. équilibrage de charge Hello distribue le trafic entrant à partir des clients web pour les serveurs web TCP port 443 (HTTPS) toohello.

serveurs de base de données Hello sont derrière un point de terminaison d’équilibrage de charge qui utilisent des serveurs web de hello pour le stockage. Cette base de données service Équilibrage de point de terminaison, le trafic qui est à charge équilibrée entre les serveurs de base de données hello dans le jeu d’équilibrage de charge interne hello.

Hello ci-dessous illustre d’image hello Internet faisant face à des applications à plusieurs niveaux au sein de hello même service cloud.

![Service cloud unique d'équilibrage de charge interne](./media/load-balancer-internal-overview/IC736321.png)

Illustration 1 - Application multi-niveau sur Internet

Une autre utilisation possible pour une application multicouche est lorsque hello équilibrage de charge interne déployé tooa autre service cloud que hello un service hello consommateur pour hello équilibrage de charge interne.

Cloud services à l’aide du même réseau virtuel aura de hello accéder au point de terminaison toohello équilibrage de charge interne. Hello ci-dessous illustre image sont des serveurs web frontaux dans un autre service cloud à partir de hello de base de données principale et à l’aide de hello de point de terminaison ILB dans hello même réseau virtuel.

![Équilibrage de charge interne entre les services cloud](./media/load-balancer-internal-overview/IC744147.png)

Figure 2 : serveurs frontaux dans un service cloud différent

## <a name="intranet-line-of-business-applications"></a>Applications cœur de métier (LOB) Intranet

Le trafic des clients sur le réseau local de hello obtenir équilibrée ensemble hello serveurs métier à l’aide du réseau de tooAzure de connexion VPN.

ordinateur client de Hello aura accès tooan IP adresse du service VPN Azure à l’aide de VPN de point de toosite. Il permet de hello d’utilisation hello application LOB hébergée derrière le point de terminaison hello équilibrage de charge interne.

![À l’aide de VPN de point de toosite d’équilibrage de charge interne](./media/load-balancer-internal-overview/IC744148.png)

Figure 3 : applications métier hébergées derrière le point de terminaison hello équilibrage de charge

Un autre scénario pour hello LOB est toohave un réseau de toohello virtuel site toosite VPN où le point de terminaison ILB hello est configuré. Ainsi, sur site réseau du trafic toobe routé toohello point de terminaison ILB.

![À l’aide du site toosite VPN d’équilibrage de charge interne](./media/load-balancer-internal-overview/IC744150.png)

Point de terminaison de la figure 4 - le trafic de réseau local routée toohello équilibrage de charge interne

## <a name="limitations"></a>Limites

Les configurations d’équilibrage de charge internes ne prennent pas en charge SNAT. Dans le contexte de hello de ce document, SNAT fait référence de traduction d’adresses réseau tooport usurpation d’identité source.  Cela s’applique tooscenarios où une machine virtuelle dans un pool d’équilibrage de charge a besoin d’adresse IP de serveur frontal de tooreach hello respectifs interne équilibrage de charge. Ce scénario n’est pas pris en charge pour l’équilibreur de charge interne. Échecs de connexion seront produit lorsque les flux hello sont à charge équilibrée toohello machine virtuelle qui provient du flux de hello. Vous devez utiliser un équilibreur de charge de type proxy pour de tels scénarios.

## <a name="next-steps"></a>Étapes suivantes

[Prise en charge d'Azure Resource Manager pour l'équilibrage de charge Azure](load-balancer-arm.md)

[Prise en main de la configuration d’un équilibrage de charge sur Internet](load-balancer-get-started-internet-arm-ps.md)

[Prise en main de la configuration d’un équilibrage de charge interne](load-balancer-get-started-ilb-arm-ps.md)

[Configuration d’un mode de distribution d’équilibrage de charge](load-balancer-distribution-mode.md)

[Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)
