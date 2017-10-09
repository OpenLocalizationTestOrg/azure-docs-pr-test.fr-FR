---
title: "itinéraires définis par l’aaaUser et le transfert IP dans Azure | Documents Microsoft"
description: "Découvrez comment tooconfigure les itinéraires définis par l’utilisateur (UDR) et le transfert IP de tooforward trafic toonetwork des équipements virtuels dans Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: c39076c4-11b7-4b46-a904-817503c4b486
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f1f1d46166d5a7c776f472b7ade1354d943ece10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-routes-and-ip-forwarding"></a>Itinéraires définis par l’utilisateur et transfert IP

Lorsque vous ajoutez des machines virtuelles (VM) tooa réseau virtuel (VNet) dans Azure, vous remarquerez que les machines virtuelles de hello sont en mesure de toocommunicate entre eux sur le réseau de hello, automatiquement. Vous n’avez pas besoin de toospecify une passerelle, bien hello machines virtuelles sont dans des sous-réseaux différents. Hello vaut également pour la communication entre toohello de machines virtuelles hello Internet public et réseau de local tooyour même lorsqu’une connexion hybride à partir d’Azure tooyour propre centre de données est présente.

Ce flux de communication est possible, car Azure utilise une série de toodefine d’itinéraires système le flux de trafic IP. Les itinéraires système contrôlent le flux de hello de communication Bonjour les scénarios suivants :

* Depuis hello même sous-réseau.
* À partir d’un sous-réseau tooanother au sein d’un réseau virtuel.
* À partir de machines virtuelles toohello Internet.
* À partir d’un réseau virtuel tooanother réseau virtuel via une passerelle VPN.
* À partir d’un réseau virtuel tooanother réseau virtuel via le réseau virtuel d’homologation (chaînage de Service).
* Un réseau virtuel tooyour sur un réseau local via une passerelle VPN.

Hello figure ci-dessous un paramétrage simple avec un réseau virtuel, deux sous-réseaux et quelques machines virtuelles, ainsi que de hello itinéraires système qui permettent de tooflow du trafic IP.

![Itinéraires système dans Azure](./media/virtual-networks-udr-overview/Figure1.png)

Bien que l’utilisation de hello d’itinéraires du système facilite le trafic automatiquement pour votre déploiement, il existe des cas dans lequel vous souhaitez toocontrol hello routage des paquets via un équipement virtuel. Vous pouvez donc en créant des itinéraires définis par l’utilisateur qui spécifier saut suivant de hello pour les paquets entrants à la place de l’appliance virtuelle tooa sous-réseau spécifique toogo tooyour, et activation IP transfert pour hello machine virtuelle en cours d’exécution en tant que l’appliance virtuelle hello.

Hello figure ci-dessous illustre les itinéraires définis par l’utilisateur et transfert tooforce paquets IP envoyés tooone sous-réseau à partir d’un autre toogo via un équipement virtuel sur un troisième sous-réseau.

![Itinéraires système dans Azure](./media/virtual-networks-udr-overview/Figure2.png)

> [!IMPORTANT]
> Itinéraires définis par l’utilisateur sont appliqué tootraffic quitter un sous-réseau à partir de n’importe quelle ressource (comme des interfaces réseau attachement tooVMs) dans le sous-réseau de hello. Vous ne pouvez pas créer des itinéraires toospecify comment le trafic entre un sous-réseau à partir d’Internet, de hello pour l’instance. équipement Hello vous transférez le trafic toocannot être Bonjour même sous-réseau que l’origine de trafic de hello. Créez toujours un sous-réseau distinct pour vos équipements. 
> 
> 

## <a name="route-resource"></a>Ressources d’itinéraire
Routage des paquets sur un réseau TCP/IP basé sur une table d’itinéraires définie sur chaque nœud sur le réseau physique de hello. Une table de routage est qu'une collection d’itinéraires individuelles utilisées toodecide où les paquets tooforward basée sur la destination de hello adresse IP. Un itinéraire se compose des éléments suivants de hello :

| Propriété | Description | Contraintes | Considérations |
| --- | --- | --- | --- |
| Préfixe d’adresse |Hello destination CIDR toowhich hello itinéraire s’applique, comme 10.1.0.0/16. |Doit être une plage CIDR valide représentant les adresses sur hello Internet public, réseau virtuel Azure ou centre de données local. |Vérifiez que hello **préfixe d’adresse** ne contient pas d’adresse hello pour hello **adresse du saut suivant**, sinon votre paquets entrera dans une boucle allant de tronçon suivant de hello source toohello sans atteindre destination de Hello. |
| Type de tronçon suivant |type de Hello du paquet de hello tronçon Azure doit être envoyé à. |Doit être une des valeurs suivantes de hello : <br/> **Réseau virtuel**. Représente un réseau virtuel local de hello. Par exemple, si vous avez deux sous-réseaux, 10.1.0.0/16 et 10.2.0.0/16 dans hello même réseau virtuel, itinéraire hello pour chaque sous-réseau dans la table d’itinéraires hello aura une valeur de saut suivante de *réseau virtuel*. <br/> **Passerelle de réseau virtuel**. Représente une passerelle VPN de site à site Azure. <br/> **Internet**. Représente la passerelle Internet de hello par défaut fournie par hello Infrastructure Azure. <br/> **Appliance virtuelle**. Représente une appliance virtuelle que vous avez ajouté tooyour réseau virtuel Azure. <br/> **None**. Représente un trou noir. Paquets transférés tooa noires ne seront pas transmis du tout. |Envisagez d’utiliser **Appliance virtuelle** toodirect tooa machine virtuelle ou équilibrage de charge Azure adresse IP interne du trafic.  Ce type permet de spécifier de hello d’une adresse IP, comme décrit ci-dessous. Envisagez d’utiliser un **aucun** toostop des paquets à partir de flux tooa donnée de destination de type. |
| adresse de tronçon suivant |adresse du tronçon suivant Hello contient adresse hello paquets doivent être transférés. Valeurs de tronçon suivant sont autorisés uniquement dans les itinéraires où le type de tronçon suivant hello est *Appliance virtuelle*. |Doit être une adresse IP qui est accessible dans hello réseau virtuel où hello défini par l’utilisateur un itinéraire est appliquée, sans passer par un **passerelle de réseau virtuel**. adresse IP de Hello a toobe hello du réseau virtuel même lorsqu’elle est appliquée, ou sur un réseau virtuel de ressources. |Si l’adresse IP de hello représente un ordinateur virtuel, veillez à activer [transfert IP](#IP-forwarding) dans Azure pour hello machine virtuelle. Si hello représente hello interne adresse IP de l’équilibrage de charge Azure, assurez-vous que vous avez une règle pour chaque port d’équilibrage de charge correspondante solde de tooload vous le souhaitez.|

Dans Azure PowerShell certaines des valeurs de « Type de tronçon suivant » hello ont des noms différents :

* Le réseau virtuel est nommé VnetLocal
* La passerelle de réseau virtuel est nommée VirtualNetworkGateway
* L’appliance virtuelle est nommée VirtualAppliance
* Internet est nommé Internet
* Aucun est nommé None

### <a name="system-routes"></a>Itinéraires système
Chaque sous-réseau créé dans un réseau virtuel est automatiquement associée à une table de routage qui contient hello suivant les règles de routage système :

* **Règle locale Vnet**: cette règle est automatiquement créée pour chaque sous-réseau d’un réseau virtuel. Il indique qu’il existe un lien direct entre les machines virtuelles de hello Bonjour réseau virtuel et il n’existe aucun saut suivant intermédiaire.
* **Règle local**: cette règle s’applique la plage d’adresses locales toohello tooall trafic à destination et utilise la passerelle VPN en tant que destination du saut suivante hello.
* **Règle Internet**: cette règle gère tout le trafic destiné toohello Internet public (préfixe d’adresse 0.0.0.0/0) et utilise hello infrastructure internet que la passerelle hello de tronçon suivant pour tout le trafic destiné toohello Internet.

### <a name="user-defined-routes"></a>Itinéraires définis par l’utilisateur
Pour la plupart des environnements, vous devez uniquement les itinéraires de système hello déjà définis par Azure. Toutefois, devez toocreate une table de routage, vous ajoutez un ou plusieurs itinéraires dans les cas spécifiques, telles que :

* Le tunneling forcé toohello Internet via votre réseau local.
* Utiliser des appliances virtuelles dans votre environnement Azure.

Dans les scénarios de hello ci-dessus, vous avez toocreate une table d’itinéraires et ajouter tooit d’itinéraires définis par l’utilisateur. Vous pouvez avoir plusieurs tables d’itinéraires et hello même table d’itinéraires peut être associé tooone ou autres sous-réseaux. Et chaque sous-réseau ne peut être une table d’itinéraires unique tooa associé. Tous les ordinateurs virtuels et services de cloud computing dans un sous-réseau, utilisent hello itinéraire table associée toothat sous-réseau.

Sous-réseaux s’appuient sur les itinéraires du système jusqu'à ce qu’une table de routage est associé toohello sous-réseau. Une fois que l’association existe, le routage se base sur la correspondance de préfixe la plus longue parmi les itinéraires définis par l’utilisateur et les itinéraires du système. S’il existe plusieurs itinéraires avec hello locales même correspond alors un itinéraire est sélectionné selon son origine dans hello suivant l’ordre :

1. Itinéraire défini par l’utilisateur
2. Itinéraire BGP (lorsque ExpressRoute est utilisé)
3. Itinéraire du système

toolearn itinéraires, défini par l’utilisateur de toocreate voir [comment tooCreate achemine et activer le transfert IP dans Azure](virtual-network-create-udr-arm-template.md).

> [!IMPORTANT]
> Les itinéraires définis par l’utilisateur sont uniquement appliqué tooAzure de machines virtuelles et services de cloud computing. Par exemple, si vous souhaitez tooadd appliance virtuelle pare-feu entre votre réseau local et le Azure, vous devez toocreate un itinéraire défini par l’utilisateur pour vos tables d’itinéraires Azure qui transmet tout le trafic entrant toohello local adresse espace toohello virtuel équipement. Vous pouvez également ajouter un défini par l’utilisateur (UDR) d’itinéraire toohello GatewaySubnet tooforward tout le trafic local tooAzure via l’appliance virtuelle hello. Il s’agit d’un ajout récent.
> 
> 

### <a name="bgp-routes"></a>Itinéraires BGP
Si vous avez une connexion ExpressRoute entre votre réseau local et le Azure, vous pouvez activer des itinéraires BGP toopropagate à partir de votre tooAzure de réseau local. Ces itinéraires BGP sont utilisés dans hello même façon que les itinéraires système et utilisateur défini des itinéraires dans chaque sous-réseau Azure. Pour plus d’informations, consultez la page [Présentation d’ExpressRoute](../expressroute/expressroute-introduction.md)

> [!IMPORTANT]
> Vous pouvez configurer votre force de toouse environnement Azure le tunneling forcé via votre réseau local en créant un itinéraire défini par l’utilisateur pour 0.0.0.0/0 de sous-réseau qui utilise la passerelle VPN de hello en tant que tronçon suivant de hello. Toutefois, cela ne fonctionne que si vous utilisez une passerelle VPN, et non ExpressRoute. Pour ExpressRoute, le tunneling forcé est configuré via BGP.
> 
> 

## <a name="ip-forwarding"></a>Transfert IP
Comme décrit ci-dessus, un des hello principales raisons toocreate un itinéraire défini par l’utilisateur est l’appliance virtuelle tooforward trafic tooa. Une appliance virtuelle n’est rien de plus qu’une machine virtuelle qui exécute un application utilisée toohandle le trafic d’une certaine façon, tel qu’un pare-feu ou un périphérique NAT.

Cet appareil virtuel que machine virtuelle doit être en mesure de tooreceive trafic entrant qui est ne traité pas tooitself. tooallow de trafic de machine virtuelle tooreceive adressé tooother destinations, vous devez activer le transfert IP pour hello machine virtuelle. Il s’agit de configuration, n’est pas un paramètre dans le système d’exploitation de hello invité Azure.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[créer des itinéraires dans le modèle de déploiement du Gestionnaire de ressources hello](virtual-network-create-udr-arm-template.md) et les associer toosubnets. 
* Découvrez comment trop[créer des itinéraires dans le modèle de déploiement classique hello](virtual-network-create-udr-classic-ps.md) et les associer toosubnets.

