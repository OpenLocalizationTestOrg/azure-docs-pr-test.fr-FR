---
title: "aaaAzure et vue d’ensemble du réseau de machine virtuelle Linux | Documents Microsoft"
description: "Vue d’ensemble de la mise en réseau de machines virtuelles Azure et Linux."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: b5420e35-0463-4456-9803-6142db150f2e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: c3de2dc583c62160e10c0e97e96fef49b9eaffbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-network-overview"></a>Vue d’ensemble du réseau de machines virtuelles Azure et Linux
## <a name="virtual-networks"></a>Virtual Network
Un réseau virtuel Azure (VNet) est une représentation de votre propre réseau dans le cloud de hello. Il s’agit d’une isolation logique de hello Azure cloud dédié tooyour abonnement. Vous pouvez contrôler entièrement les blocs d’adresses IP hello, les paramètres DNS, les stratégies de sécurité et les tables d’itinéraires au sein de ce réseau. Vous pouvez également segmenter votre réseau virtuel en plusieurs sous-réseaux et lancer des machines virtuelles IaaS Azure et/ou des services cloud (instances de rôle PaaS). En outre, vous pouvez vous connecter hello réseau virtuel tooyour sur réseau local à l’aide d’une des options de connectivité hello disponibles dans Azure. Fondamentalement, vous pouvez développer votre tooAzure réseau, avec un contrôle complet sur les blocs d’adresses IP avec avantage hello d’échelle de l’entreprise Qu'azure fournit.

* [Présentation du réseau virtuel.](../../virtual-network/virtual-networks-overview.md)

un réseau virtuel à l’aide de toocreate hello CLI d’Azure, accédez toofollow ici hello Parcourir.

* [Comment un réseau virtuel à l’aide de toocreate hello CLI d’Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

## <a name="network-security-groups"></a>Network Security Group
Groupe de sécurité réseau (NSG) contient une liste de règles de liste de contrôle d’accès (ACL) qui autorisent ou refusent le trafic réseau tooyour des instances de machine virtuelle dans un réseau virtuel. Des groupes de sécurité réseau peuvent être associés à des sous-réseaux ou à des instances de machine virtuelle au sein de ce sous-réseau. Lorsqu’un groupe de sécurité réseau est associé à un sous-réseau, listes de contrôle hello appliquent instances de machine virtuelle tooall hello dans ce sous-réseau. En outre, le trafic tooan machine virtuelle individuelle peut être limité par l’association d’un groupe de sécurité réseau directement toothat machine virtuelle.

* [Présentation du groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md)
* [Comment les groupes de sécurité réseau toocreate dans hello CLI d’Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

## <a name="user-defined-routes"></a>Itinéraires définis par l’utilisateur
Lorsque vous ajoutez des machines virtuelles (VM) tooa réseau virtuel (VNet) dans Azure, vous remarquerez que les machines virtuelles de hello sont en mesure de toocommunicate entre eux sur le réseau de hello, automatiquement. Vous n’avez pas besoin de toospecify une passerelle, bien hello machines virtuelles sont dans des sous-réseaux différents. Hello vaut également pour la communication entre toohello de machines virtuelles hello Internet public et réseau de local tooyour même lorsqu’une connexion hybride à partir d’Azure tooyour propre centre de données est présente.

* [Présentation des itinéraires définis par l’utilisateur et du transfert IP](../../virtual-network/virtual-networks-udr-overview.md)
* [Créer un UDR Bonjour CLI d’Azure](../../virtual-network/virtual-network-create-udr-arm-cli.md)

## <a name="associating-a-fqdn-tooyour-linux-vm"></a>Association d’un nom de domaine complet de tooyour Linux VM
Lorsque vous créez un ordinateur virtuel (VM) Bonjour portail Azure à l’aide du modèle de déploiement de gestionnaire de ressources hello, une adresse IP publique ressource pour la machine virtuelle de hello est automatiquement créée. Vous utilisez cette hello d’accès IP adresse tooremotely machine virtuelle. Bien que le portail de hello ne crée pas un nom de domaine complet ou le nom de domaine complet, par défaut, vous pouvez ajouter un fois hello machine virtuelle est créée.

* [Créer un nom de domaine complet dans hello portail Azure](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="network-interfaces"></a>Interfaces réseau
Une interface réseau (NIC) est interconnexion hello entre un ordinateur virtuel (VM) et le hello sous-jacent réseau du logiciel. Cet article explique quelles une interface réseau est et comment il est utilisé dans le modèle de déploiement du Gestionnaire de ressources Azure hello.

* [Interfaces de réseau virtuel](../../virtual-network/virtual-network-network-interface.md)

## <a name="virtual-nics-and-dns-labeling"></a>Cartes réseau virtuelles et étiquetage DNS
Si vous disposez d’un serveur, vous devez toobe persistant, mais ce serveur est traité comme animaux et est détruit et déployé fréquemment, vous pouvez toouse DNS étiquetage nom de votre carte réseau toopersist hello sur hello réseau virtuel.  Avec hello suivant la procédure pas à pas vous va installer une carte de réseau nommé de manière permanente avec une adresse IP statique.

* [Créer un environnement complet de Linux à l’aide de hello CLI d’Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="virtual-network-gateways"></a>Passerelles de réseau virtuel
Sert de passerelle de réseau virtuel toosend le trafic de réseau entre les réseaux virtuels Azure et les emplacements sur site et également entre les réseaux virtuels dans Azure (au réseau). Lorsque vous configurez une passerelle VPN, vous devez créer et configurer une passerelle de réseau virtuel et une connexion à la passerelle de réseau virtuel.

* [À propos de la passerelle VPN](../../vpn-gateway/vpn-gateway-about-vpngateways.md)

## <a name="internal-load-balancing"></a>Équilibrage de charge interne
Un équilibrage de charge Azure est de type Couche 4 (TCP, UDP). équilibrage de charge Hello offre une haute disponibilité en répartissant le trafic entrant entre les instances de service intègre dans les services de cloud computing ou les machines virtuelles dans un jeu d’équilibrage de charge. Azure Load Balancer peut également présenter ces services sur plusieurs ports, plusieurs adresses IP ou les deux.

* [Création d’un équilibreur de charge interne à l’aide de hello CLI d’Azure](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)

