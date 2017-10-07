---
title: connexion aaaHybrid avec application de couche 2 | Documents Microsoft
description: "Découvrez comment toodeploy équipements virtuels et UDR toocreate un environnement d’application à plusieurs niveaux dans Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 1f509bec-bdd1-470d-8aa4-3cf2bb7f6134
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/05/2016
ms.author: jdial
ms.openlocfilehash: 53599862289dbf9c6ab3289b0cb8dda6430f20f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-appliance-scenario"></a>Scénario d’appliance virtuelle
Un scénario courant entre le client Azure supérieure est hello besoin tooprovide un toohello d’application à deux niveaux exposé Internet, tout en autorisant le niveau précédent toohello d’accès à partir d’un centre de données local. Ce document vous guidera dans un scénario à l’aide d’utilisateur défini itinéraires (UDR), une passerelle VPN et le réseau équipements virtuels toodeploy un environnement à deux niveaux qui répond aux hello suivant les exigences :

* Application Web doit être accessible à partir de hello Internet public uniquement.
* Application hello hébergement du serveur Web doit être en mesure de tooaccess un serveur d’applications principal.
* Tout le trafic à partir de hello application web de toohello Internet doit traverser un équipement virtuel pare-feu. Cette appliance virtuelle ne sera utilisée que pour le trafic Internet.
* Tout le trafic entrant du serveur d’applications toohello doit traverser un équipement virtuel pare-feu. Cet appareil virtuel sera utilisé pour le serveur d’accès toohello principal fin et l’accès à venir de hello sur un réseau local via une passerelle VPN.
* Les administrateurs doivent être des équipements virtuels pare-feu hello toomanage en mesure de leur ordinateur local, en utilisant un troisième pare-feu appliance virtuelle utilisé exclusivement à des fins de gestion.

Il s’agit d’un scénario avec une zone DMZ et un réseau protégé. Ce scénario peut être mis en œuvre dans Azure à l’aide de groupes de sécurité réseau, d’appliances virtuelles de pare-feu ou d’une combinaison des deux. tableau de Hello ci-dessous présente certains des avantages et inconvénients entre les groupes de sécurité réseau et les équipements virtuels pare-feu hello.

|  | Avantages | Inconvénients |
| --- | --- | --- |
| Groupe de sécurité réseau |Aucun coût. <br/>Intégré dans Azure RBAC. <br/>Possibilité de créer des règles dans les modèles ARM. |Complexité variable dans les environnements de grande taille. |
| Pare-feu |Contrôle total sur le plan des données. <br/>Gestion centralisée via la console du pare-feu. |Coût de l’appliance de pare-feu. <br/>Non intégré dans Azure RBAC. |

solution Hello ci-dessous utilise un pare-feu équipements virtuels tooimplement un scénario de réseau protégé/un réseau de périmètre.

## <a name="considerations"></a>Considérations
Vous pouvez déployer l’environnement hello expliqué ci-dessus dans Azure à l’aide de différentes fonctionnalités disponibles aujourd'hui, comme suit.

* **Réseau virtuel**. Un réseau virtuel Azure agit dans le réseau local de tooan similaire de manière et peuvent être placé dans un ou plusieurs isolation du trafic tooprovide sous-réseaux et la séparation des préoccupations.
* **Appliance virtuelle**. Plusieurs partenaires fournissent des équipements virtuels Bonjour Azure Marketplace qui peut être utilisé pour les trois pare-feu hello décrites ci-dessus. 
* **Itinéraires définis par l’utilisateur**. Tables d’itinéraires peuvent contenir UDRs utilisées par Azure flux de hello toocontrol mise en réseau de paquets au sein d’un réseau virtuel. Ces tables d’itinéraires peuvent être appliqué toosubnets. Une des fonctionnalités les plus récents de hello dans Azure est hello capacité tooapply un toohello de table itinéraire GatewaySubnet, fournissant hello capacité tooforward tout le trafic entrant dans hello réseau virtuel Azure à partir d’une appliance virtuelle à tooa connexion hybride.
* **Transfert IP**. Par défaut, hello du moteur de mise en réseau Azure transférer les paquets toovirtual cartes d’interface réseau (NIC) uniquement si hello adresse NIC IP correspond à l’adresse IP de destination de paquets hello. Par conséquent, si un UDR définit que tooa donné appliance virtuelle doit être envoyé à un paquet, hello du moteur de mise en réseau Azure diminuerait, ce paquet. paquet de hello tooensure est remis tooa machine virtuelle (dans ce cas, une appliance virtuelle) qui n’est pas destination réelle de hello pour les paquets hello, vous devez tooenable le transfert IP pour l’appliance virtuelle hello.
* **Groupes de sécurité réseau (NSG)**. exemple Hello ci-dessous ne fait pas l’utilisation de groupes de sécurité réseau, mais vous pouvez utiliser des sous-réseaux toohello de groupes de sécurité réseau appliquées et/ou des cartes réseau dans cet solution toofurther filtre hello le trafic vers et depuis ces sous-réseaux et les cartes réseau.

![Connectivité IPv6](./media/virtual-network-scenario-udr-gw-nva/figure01.png)

Dans cet exemple, il existe un abonnement qui contient les éléments suivants de hello :

* 2 groupes de ressources, ne pas illustrés hello. 
  * **ONPREMRG**. Contient toutes les ressources toosimulate nécessaire un réseau local.
  * **AZURERG**. Contient toutes les ressources nécessaires pour l’environnement de réseau virtuel Azure hello. 
* Un réseau virtuel nommé **onpremvnet** utilisé toomimic local d’un centre de données segmentée comme indiqué ci-dessous.
  * **onpremsn1**. Sous-réseau contenant un ordinateur virtuel (VM) en cours d’exécution Ubuntu toomimic un serveur local.
  * **onpremsn2**. Sous-réseau contenant une machine virtuelle exécutant Ubuntu toomimic un ordinateur local utilisé par un administrateur.
* Il existe une appliance virtuelle pare-feu nommée **OPFW** sur **onpremvnet** utilisé toomaintain un tunnel trop**azurevnet**.
* Un réseau virtuel nommé **azurevnet** segmenté comme indiqué ci-dessous.
  * **azsn1**. Sous-réseau de pare-feu externe utilisé exclusivement pour les pare-feu externe hello. Tout le trafic Internet entrera par ce sous-réseau. Ce sous-réseau ne contient qu’un pare-feu externe toohello de carte réseau liée.
  * **azsn2**. Sous-réseau frontal qui héberge une machine virtuelle en cours d’exécution en tant qu’un serveur web qui est accessible à partir de hello Internet.
  * **azsn3**. Sous-réseau principal qui héberge une machine virtuelle exécutant un serveur d’applications principal qui sera accessible par le serveur de web frontal hello.
  * **azsn4**. Sous-réseau de gestion utilisé exclusivement tooprovide gestion accès tooall pare-feu équipements virtuels. Ce sous-réseau contient uniquement une carte réseau pour chaque appliance virtuelle pare-feu utilisé dans les solutions hello.
  * **GatewaySubnet**. Sous-réseau de connexion hybride Azure requis pour la connectivité de tooprovide ExpressRoute et passerelle VPN entre réseaux virtuels Azure et d’autres réseaux. 
* Il existe 3 équipements virtuels pare-feu Bonjour **azurevnet** réseau. 
  * **AZF1**. Pare-feu externe exposé toohello Internet public à l’aide d’une ressource d’adresse IP publique dans Azure. Vous devez tooensure vous disposez d’un modèle à partir de hello Marketplace, ou directement à partir de votre fournisseur de matériel, qui configure une appliance virtuelle 3-NIC.
  * **AZF2**. Le pare-feu interne utilisé le trafic de toocontrol entre **azsn2** et **azsn3**. C’est également une appliance virtuelle à 3 cartes réseau.
  * **AZF3**. Tooadministrators accessible de pare-feu administration à partir de hello centre de données sur site et sous-réseau de gestion tooa connecté utilisé toomanage tous les appareils de pare-feu. Vous pouvez trouver des modèles d’appliance virtuelle 2-NIC Bonjour Marketplace, ou la demande directement à partir de votre fournisseur de matériel.

## <a name="user-defined-routing-udr"></a>Itinéraire défini par l’utilisateur (UDR)
Chaque sous-réseau dans Azure peut être lié tooa UDR table utilisée toodefine comment le trafic initié dans ce sous-réseau est routé. Si aucune UDRs ne sont définies, Azure utilise par défaut itinéraires tooallow trafic tooflow à partir d’un seul sous-réseau tooanother. toobetter comprendre UDRs, visitez le site [que sont les itinéraires définis d’utilisateur et le transfert IP](virtual-networks-udr-overview.md#ip-forwarding).

tooensure communication s’effectue via hello pare-feu approprié, en fonction de la dernière demande hello ci-dessus, vous devez suivant de hello toocreate table d’itinéraires contenant UDRs dans **azurevnet**.

### <a name="azgwudr"></a>azgwudr
Dans ce scénario, hello uniquement le trafic circulant de local tooAzure sera utilisé toomanage hello pare-feu en vous connectant trop**AZF3**, et que le trafic doit traverser le pare-feu interne hello, **AZF2**. Par conséquent, qu’une seule est nécessaire dans hello **GatewaySubnet** comme indiqué ci-dessous.

| Destination | Tronçon suivant | Explication |
| --- | --- | --- |
| 10.0.4.0/24 |10.0.3.11 |Permet de pare-feu de gestion local le trafic tooreach **AZF3** |

### <a name="azsn2udr"></a>azsn2udr
| Destination | Tronçon suivant | Explication |
| --- | --- | --- |
| 10.0.3.0/24 |10.0.2.11 |Permet de sous-réseau de trafic toohello principal réseau hébergeant le serveur d’applications hello via **AZF2** |
| 0.0.0.0/0 |10.0.2.10 |Permet à tous les autres toobe du trafic routé via **AZF1** |

### <a name="azsn3udr"></a>azsn3udr
| Destination | Tronçon suivant | Explication |
| --- | --- | --- |
| 10.0.2.0/24 |10.0.3.10 |Autorise le trafic trop**azsn2** tooflow à partir de l’application serveur toohello webserver via **AZF2** |

Vous devez également les tables d’itinéraires toocreate des sous-réseaux hello **onpremvnet** toomimic hello centre de données sur site.

### <a name="onpremsn1udr"></a>onpremsn1udr
| Destination | Tronçon suivant | Explication |
| --- | --- | --- |
| 192.168.2.0/24 |192.168.1.4 |Autorise le trafic trop**onpremsn2** via **OPFW** |

### <a name="onpremsn2udr"></a>onpremsn2udr
| Destination | Tronçon suivant | Explication |
| --- | --- | --- |
| 10.0.3.0/24 |192.168.2.4 |Permet de sous-réseau de trafic toohello sauvegardée dans Azure via **OPFW** |
| 192.168.1.0/24 |192.168.2.4 |Autorise le trafic trop**onpremsn1** via **OPFW** |

## <a name="ip-forwarding"></a>transfert IP
UDR et le routage IP sont des fonctionnalités que vous pouvez utiliser dans la combinaison tooallow équipements virtuels toobe utilisé toocontrol le flux de trafic dans un réseau virtuel Azure.  Une appliance virtuelle n’est rien de plus qu’une machine virtuelle qui exécute un application utilisée toohandle le trafic d’une certaine façon, tel qu’un pare-feu ou un périphérique NAT.

Cet appareil virtuel que machine virtuelle doit être en mesure de tooreceive trafic entrant qui est ne traité pas tooitself. tooallow de trafic de machine virtuelle tooreceive adressé tooother destinations, vous devez activer le transfert IP pour hello machine virtuelle. Il s’agit de configuration, n’est pas un paramètre dans le système d’exploitation de hello invité Azure. Votre appliance virtuelle toujours besoins toorun certain type d’application toohandle hello le trafic entrant et acheminer de manière appropriée.

toolearn en savoir plus sur le transfert IP, visitez [que sont les itinéraires définis d’utilisateur et le transfert IP](virtual-networks-udr-overview.md#ip-forwarding).

Par exemple, imaginez que vous avez hello après l’installation dans un réseau virtuel Azure :

* Le sous-réseau **onpremsn1** contient une machine virtuelle nommée **onpremvm1**.
* Le sous-réseau **onpremsn2** contient une machine virtuelle nommée **onpremvm2**.
* Une appliance virtuelle nommée **OPFW** est connecté trop**onpremsn1** et **onpremsn2**.
* Un itinéraire défini par l’utilisateur lié trop**onpremsn1** Spécifie que tout le trafic trop**onpremsn2** doivent être envoyées trop**OPFW**.

AT que ce point, si **onpremvm1** tente d’une connexion avec tooestablish **onpremvm2**, hello UDR sera utilisé et que le trafic sera envoyé trop**OPFW** en tant que tronçon suivant de hello. N’oubliez pas que hello destination du paquet n’est pas modifié, il indique toujours **onpremvm2** hello destination. 

Sans activé pour le transfert IP **OPFW**, hello logique de réseau virtuelle Azure supprimera les paquets hello, car elle permet uniquement les paquets envoyé de toobe tooa machine virtuelle si hello adresse IP de la machine virtuelle est la destination hello pour les paquets hello.

Avec le transfert IP, hello logique de réseau virtuel Azure transfèrera tooOPFW de paquets hello, sans modifier son adresse de destination d’origine. **OPFW** doit gérer les paquets hello et pour déterminer quelles toodo avec eux.

Pour le scénario hello ci-dessus toowork, vous devez activer le transfert IP sur les cartes réseau de hello pour **OPFW**, **AZF1**, **AZF2**, et **AZF3** qui sont utilisés pour (toutes les cartes réseau à l’exception de hello ceux liés toohello gestion sous-réseau) de routage. 

## <a name="firewall-rules"></a>Règles de pare-feu
Comme décrit ci-dessus, le transfert IP seulement garantit les équipements virtuels toohello les paquets sont envoyés. Votre application doit tout de même toodecide le toodo avec les paquets. Dans le scénario hello ci-dessus, vous devrez hello toocreate suivant les règles dans vos applications :

### <a name="opfw"></a>OPFW
OPFW représente un périphérique local contenant hello suivant les règles :

* **Itinéraire**: tout le trafic too10.0.0.0/16 (**azurevnet**) doivent être envoyés via le tunnel **ONPREMAZURE**.
* **Stratégie** : autoriser tout le trafic bidirectionnel entre **port2** et **ONPREMAZURE**.

### <a name="azf1"></a>AZF1
AZF1 représente une appliance virtuelle Azure contenant hello suivant les règles :

* **Stratégie** : autoriser tout le trafic bidirectionnel entre **port1** et **port2**.

### <a name="azf2"></a>AZF2
AZF2 représente une appliance virtuelle Azure contenant hello suivant les règles :

* **Itinéraire**: tout le trafic too10.0.0.0/16 (**onpremvnet**) doivent être envoyés une adresse IP de passerelle Azure toohello (par exemple, 10.0.0.1) via **port1**.
* **Stratégie** : autoriser tout le trafic bidirectionnel entre **port1** et **port2**.

## <a name="network-security-groups-nsgs"></a>Groupes de sécurité réseau (NSG)
Dans ce scénario, les groupes de sécurité réseau ne sont pas utilisés. Toutefois, vous pouvez appliquer des groupes de sécurité réseau tooeach toorestrict entrant et sortant du trafic de sous-réseau. Par exemple, vous pouvez appliquer hello suivant le sous-réseau FW externe NSG règles toohello.

**Entrant**

* Autoriser tout le trafic TCP de hello Internet tooport 80 sur n’importe quel ordinateur virtuel dans un sous-réseau de hello.
* Refuser tout le trafic à partir de hello Internet.

**Sortant**

* Refuser tout trafic toohello Internet.

## <a name="high-level-steps"></a>Étapes de haut niveau
toodeploy ce scénario, suivez hello procédure générale ci-dessous.

1. Connexion tooyour abonnement Azure.
2. Si vous voulez toodeploy un Bonjour toomimic de réseau virtuel local réseau, configurer les ressources de hello qui font partie de **ONPREMRG**.
3. Prévoir les ressources hello qui font partie de **AZURERG**.
4. Tunnel hello de fourniture de **onpremvnet** trop**azurevnet**.
5. Une fois que toutes les ressources sont configurés, ouvrez une session trop**onpremvm2** et la connectivité de tootest ping 10.0.3.101 entre **onpremsn2** et **azsn3**.

