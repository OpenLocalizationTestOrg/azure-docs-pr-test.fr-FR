---
title: "aaaOverview d’un scénario de récupération d’urgence Oracle dans votre environnement Azure | Documents Microsoft"
description: "Scénario de récupération d’urgence pour une base de données Oracle Database 12c dans votre environnement Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a>Récupération d’urgence pour une base de données Oracle Database 12c dans votre environnement Azure

## <a name="assumptions"></a>Hypothèses

- Vous disposez d’une connaissance de la conception d’Oracle Data Guard et des environnements Azure.


## <a name="goals"></a>Objectifs
- Concevoir une topologie de hello et de configuration qui répondent à vos besoins de reprise après sinistre.

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a>Scénario 1 : site principal et site de récupération d’urgence sur Azure

Un client dispose d’Oracle des bases de données de site principal de hello. Un site de récupération d’urgence se trouve dans une autre région. client de Hello utilise Oracle Data Guard pour une récupération rapide entre ces sites. site principal de Hello possède également une base de données secondaire pour la création de rapports et d’autres utilisations. 

### <a name="topology"></a>Topologie

Voici un résumé de hello le programme d’installation Azure :

- Deux sites (un site principal et un site de récupération d’urgence)
- Deux réseaux virtuels
- Deux bases de données Oracle avec Data Guard (primaire et secondaire)
- Deux bases de données Oracle avec Golden Gate ou Data Guard (site principal uniquement)
- Les deux services d’application, un serveur principal et sur le site de récupération d’urgence de hello
- Un *à haute disponibilité,* qui est utilisé pour la base de données et application de service sur le site principal de hello
- Un jumpbox sur chaque site, ce qui restreint le réseau privé de l’accès toohello et autorise uniquement l’authentification dans par un administrateur
- Jumpbox, service d’application, base de données et passerelle VPN sur des sous-réseaux distincts
- Le groupe de sécurité réseau est appliqué sur les sous-réseaux d’application et de base de données

![Capture d’écran de la page de la topologie hello récupération d’urgence](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a>Scénario 2 : site principal local et site de récupération d’urgence sur Azure

Un client dispose d’une configuration de base de données Oracle locale (site principal). Le site de récupération d’urgence est sur Azure. Oracle Data Guard permet une récupération rapide entre ces sites. site principal de Hello possède également une base de données secondaire pour la création de rapports et d’autres utilisations. 

Deux approches sont possibles pour cette configuration.

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a>Méthode 1 : Les connexions directes entre locaux et Azure, nécessitant des ports TCP ouverts sur les pare-feu hello 

Nous ne recommandons des connexions directes, car ils exposent toohello de ports TCP hello world à l’extérieur.

#### <a name="topology"></a>Topologie

Voici un résumé de hello le programme d’installation Azure :

- Un site de récupération d’urgence 
- Un seul réseau virtuel
- Une base de données Oracle avec Data Guard (active)
- Service d’une application sur le site de récupération d’urgence de hello
- Un jumpbox, ce qui restreint le réseau privé de l’accès toohello et autorise uniquement l’authentification dans par un administrateur
- Jumpbox, service d’application, base de données et passerelle VPN sur des sous-réseaux distincts
- Le groupe de sécurité réseau est appliqué sur les sous-réseaux d’application et de base de données
- Un tooallow/règle de stratégie de groupe de sécurité réseau entrants le port 1521 TCP (ou un port défini par l’utilisateur)
- Un groupe de sécurité réseau/règle de stratégie toorestrict uniquement hello IP adresse/adresses locales (base de données ou application) tooaccess hello réseau virtuel

![Capture d’écran de la page de la topologie hello récupération d’urgence](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a>Approche 2 : VPN de site à site
La meilleure approche consiste à utiliser des VPN de site à site. Pour plus d’informations sur la configuration d’un VPN, consultez [Créer un réseau virtuel avec une connexion VPN de Site à Site à l’aide de CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).

#### <a name="topology"></a>Topologie

Voici un résumé de hello le programme d’installation Azure :

- Un site de récupération d’urgence 
- Un seul réseau virtuel 
- Une base de données Oracle avec Data Guard (active)
- Service d’une application sur le site de récupération d’urgence de hello
- Un jumpbox, ce qui restreint le réseau privé de l’accès toohello et autorise uniquement l’authentification dans par un administrateur
- Une jumpbox, un service d’application, une base de données et une passerelle VPN se trouvent sur des sous-réseaux distincts
- Le groupe de sécurité réseau est appliqué sur les sous-réseaux d’application et de base de données
- Connexion VPN de site à site entre un site local et un site sur Azure

![Capture d’écran de la page de la topologie hello récupération d’urgence](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a>Documentation supplémentaire

- [Concevoir et mettre en œuvre une base de données Oracle sur Azure](oracle-design.md)
- [Implémenter Oracle Data Guard sur une machine virtuelle Linux Azure](configure-oracle-dataguard.md)
- [Implémenter Oracle Golden Gate sur une machine virtuelle Linux Azure](configure-oracle-golden-gate.md)
- [Sauvegarde et récupération Oracle](oracle-backup-recovery.md)


## <a name="next-steps"></a>Étapes suivantes

- [Didacticiel : créer des machines virtuelles hautement disponibles](../../linux/create-cli-complete.md)
- [Explorer des exemples Azure CLI de déploiement de machines virtuelles](../../linux/cli-samples.md)
