---
title: "les groupes de sécurité aaaNetwork dans Azure | Documents Microsoft"
description: "Découvrez comment le flux tooisolate et contrôler le trafic au sein de vos réseaux virtuels à l’aide de pare-feu de hello distribué dans Azure à l’aide de groupes de sécurité réseau."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 20e850fc-6456-4b5f-9a3f-a8379b052bc9
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/11/2016
ms.author: jdial
ms.openlocfilehash: 3528ce833dab17977327c3c9ae0e78316e5e6a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="filter-network-traffic-with-network-security-groups"></a>Filtrer le trafic réseau avec les groupes de sécurité réseau

Un groupe de sécurité réseau (NSG) contient une liste de règles de sécurité qui autorisent ou refusent tooresources de trafic réseau connecté tooAzure de réseaux virtuels (VNet). Groupes de sécurité réseau peuvent être associé toosubnets, des ordinateurs virtuels individuels (classique), ou l’interface réseau (NIC) attaché tooVMs (Resource Manager). Lorsqu’un groupe de sécurité réseau est associé tooa sous-réseau, les règles de hello s’appliquent tooall ressources toohello connecté sous-réseau. Le trafic peut encore être limité en également associer un tooa groupe de sécurité réseau de machine virtuelle ou la carte réseau.

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md). Cet article couvre l’utilisation de ces deux modèles, mais Microsoft recommande que la plupart des nouveaux déploiements utilisent le modèle de gestionnaire de ressources hello.

## <a name="nsg-resource"></a>Ressource du groupe de sécurité réseau
Groupes de sécurité réseau contient hello propriétés suivantes :

| Propriété | Description | Contraintes | Considérations |
| --- | --- | --- | --- |
| Nom |Nom de hello NSG |Doit être unique au sein de la région de hello.<br/>Peut contenir des lettres, des chiffres, des traits de soulignement, des points et des traits d’union.<br/>Doit commencer par une lettre ou un chiffre.<br/>Doit se terminer par une lettre, un chiffre ou un trait de soulignement.<br/>Ne doit pas dépasser 80 caractères. |Étant donné que vous devrez peut-être toocreate plusieurs groupes de sécurité réseau, assurez-vous que vous disposez d’une convention d’affectation de noms qui rend la fonction de hello tooidentify facile de vos groupes de sécurité réseau. |
| Région |Azure [région](https://azure.microsoft.com/regions) où hello NSG est créé. |Groupes de sécurité réseau peuvent uniquement être associé tooresources dans hello même région que hello groupe de sécurité réseau. |toolearn sur les groupes de sécurité réseau nombre que vous avez par région, lire hello [Azure limite](../azure-subscription-service-limits.md#virtual-networking-limits-classic) l’article.|
| Groupe de ressources |Hello [groupe de ressources](../azure-resource-manager/resource-group-overview.md#resource-groups) hello NSG existe dans. |Bien qu’il existe un groupe de sécurité réseau dans un groupe de ressources, il peut être associé à tooresources dans n’importe quel groupe de ressources, tant que ressource de hello fait partie de hello même région Azure que hello groupe de sécurité réseau. |Groupes de ressources est toomanage utilisé ensemble, comme une unité de déploiement de plusieurs ressources.<br/>Vous pouvez envisager de hello NSG avec elle est associée à des ressources de regroupement. |
| Règles |Règles de trafic entrant ou sortant définissant le trafic qui est autorisé ou refusé. | |Consultez hello [règles du groupe de sécurité réseau](#Nsg-rules) section de cet article. |

> [!NOTE]
> ACL basées sur le point de terminaison et la sécurité du réseau de groupes ne sont pas pris en charge sur hello la même instance de machine virtuelle. Si vous souhaitez toouse un groupe de sécurité réseau et que vous disposez déjà d’un point de terminaison ACL en place, tout d’abord supprimer les ACL du point de terminaison de hello. toolearn comment tooremove une ACL, lire hello [gestion Access Control Lists (ACL) pour les points de terminaison à l’aide de PowerShell](virtual-networks-acl-powershell.md) l’article.
> 

### <a name="nsg-rules"></a>règles de groupe de sécurité réseau
Règles du groupe de sécurité réseau contient hello propriétés suivantes :

| Propriété | Description | Contraintes | Considérations |
| --- | --- | --- | --- |
| **Name** |Nom de règle de hello. |Doit être unique au sein de la région de hello.<br/>Peut contenir des lettres, des chiffres, des traits de soulignement, des points et des traits d’union.<br/>Doit commencer par une lettre ou un chiffre.<br/>Doit se terminer par une lettre, un chiffre ou un trait de soulignement.<br/>Ne doit pas dépasser 80 caractères. |Vous peut avoir plusieurs règles au sein d’un groupe de sécurité réseau, par conséquent, assurez-vous que vous suivez une convention d’affectation de noms qui vous permet de fonction de hello tooidentify de votre règle. |
| **Protocole** |Toomatch de protocole pour la règle de hello. |TCP, UDP ou * |À l’aide de * comme un protocole inclut ICMP (trafic est-ouest uniquement), en ainsi que UDP et TCP et peut réduire nombre hello de règles que vous avez besoin.<br/>AT hello même temps, à l’aide de * est peut-être trop large une approche, il est donc recommandé d’utiliser * uniquement lorsque cela est nécessaire. |
| **Plage de ports source** |Toomatch plage du port source pour la règle de hello. |Numéro de port à partir de 1 too65535, plage de ports unique (exemple : 1-65535), ou * (pour tous les ports). |Les ports source peuvent être éphémères. Privilégiez l’utilisation de * dans la plupart des cas, sauf si votre programme client utilise un port spécifique.<br/>Essayez de plages de ports toouse autant que possible tooavoid hello besoin de plusieurs règles.<br/>Il est impossible de regrouper plusieurs ports ou plages de ports à l’aide d’une virgule. |
| **Plage de ports de destination** |Toomatch plage du port destination pour la règle de hello. |Numéro de port à partir de 1 too65535, plage de ports unique (exemple : 1-65535), ou \* (pour tous les ports). |Essayez de plages de ports toouse autant que possible tooavoid hello besoin de plusieurs règles.<br/>Il est impossible de regrouper plusieurs ports ou plages de ports à l’aide d’une virgule. |
| **Préfixe d’adresse source** |Source adresse préfixe ou balise toomatch pour la règle de hello. |Adresse IP unique (par exemple, 10.10.10.10), sous-réseau IP (par exemple, 192.168.1.0/24), [balise par défaut](#default-tags) ou * (pour toutes les adresses). |Envisagez d’utiliser des plages, les balises par défaut, et * nombre de hello tooreduce de règles. |
| **Préfixe d’adresse de destination** |Destination adresse préfixe ou balise toomatch pour la règle de hello. | Adresse IP unique (par exemple, 10.10.10.10), sous-réseau IP (par exemple, 192.168.1.0/24), [balise par défaut](#default-tags) ou * (pour toutes les adresses). |Envisagez d’utiliser des plages, les balises par défaut, et * nombre de hello tooreduce de règles. |
| **Direction** |Direction de toomatch le trafic pour la règle de hello. |Entrant ou sortant. |Les règles de trafic entrant et de trafic sortant sont traitées séparément, en fonction de la direction. |
| **Priorité** |Les règles sont vérifiées dans l’ordre de hello de priorité. Une fois qu’une règle s’applique, plus aucune correspondance de règle n’est testée. | Nombre compris entre 100 et 4096. | Envisagez de créer des règles de saut priorités par 100 pour chaque espace de tooleave de règle de nouvelles règles que vous pouvez créer dans hello futures. |
| **Access** |Type d’accès tooapply si hello règle met en correspondance. | Autoriser ou refuser. | Gardez à l’esprit que si une règle d’autorisation n’est pas trouvée pour un paquet, les paquets hello sont supprimé. |

Les NSG contiennent deux ensembles de règles : les règles de trafic entrant et les règles de trafic sortant. priorité de Hello pour une règle doit être unique dans chaque jeu. 

![Traitement des règles de groupe de sécurité réseau](./media/virtual-network-nsg-overview/figure3.png) 

image précédente de Hello montre le traitement des règles du groupe de sécurité réseau.

### <a name="default-tags"></a>Balises par défaut
Balises par défaut sont des identificateurs fournis par le système tooaddress une catégorie d’adresses IP. Vous pouvez utiliser des balises par défaut dans hello **préfixe d’adresse source** et **préfixe d’adresse de destination** propriétés d’une règle. Les balises par défaut que vous pouvez utiliser sont au nombre de trois :

* **VirtualNetwork** (Resource Manager) (**VIRTUAL_NETWORK** pour classique) : cette balise inclut l’espace d’adressage de réseau virtuel hello (plages CIDR définis dans Azure), tous les connectée espaces d’adressage local et Réseaux virtuels Azure (réseaux locaux).
* **AzureLoadBalancer** (Resource Manager) (**AZURE_LOADBALANCER** pour Classic) : cette balise désigne l’équilibreur de charge de l’infrastructure Azure. balise de Hello traduit tooan proviennent de l’IP du centre de données Azure dans lequel les tests de contrôle d’intégrité d’Azure.
* **Internet** (Resource Manager) (**INTERNET** pour classique) : cette balise désigne l’espace d’adressage IP hello qui se trouve en dehors du réseau virtuel de hello et accessible via l’Internet public. plage de Hello inclut hello [Azure appartenant à un espace IP public](https://www.microsoft.com/download/details.aspx?id=41653).

### <a name="default-rules"></a>Règles par défaut
Tous les groupes de ressources réseau contiennent un ensemble de règles par défaut. les règles par défaut Hello ne peut pas être supprimés, mais comme ils sont affectés de priorité la plus faible de hello, elles peuvent être remplacées par les règles hello que vous créez. 

les règles par défaut Hello autoriser et interdire le trafic comme suit :
- **Réseau virtuel :** le trafic en provenance et à destination d’un réseau virtuel est autorisé à la fois dans les directions entrante et sortante.
- **Internet :** le trafic sortant est autorisé, mais le trafic entrant est bloqué.
- **L’équilibrage de charge :** charge équilibrage tooprobe hello l’intégrité d’autoriser Azure de vos machines virtuelles et les instances de rôle. Vous pouvez remplacer cette règle si vous n’utilisez pas un jeu d’équilibrage de la charge.

**Les règles par défaut sont :**

| Name | Priorité | IP Source | Port source | IP de destination | Port de destination | Protocole | Access |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVNetInBound |65 000 | VirtualNetwork | * | VirtualNetwork | * | * | AUTORISER |
| AllowAzureLoadBalancerInBound | 65 001 | AzureLoadBalancer | * | * | * | * | AUTORISER |
| DenyAllInBound |65 500 | * | * | * | * | * | REFUSER |

**Les règles sortantes par défaut sont :**

| Name | Priorité | IP Source | Port source | IP de destination | Port de destination | Protocole | Access |
| --- | --- | --- | --- | --- | --- | --- | --- |
| AllowVnetOutBound | 65 000 | VirtualNetwork | * | VirtualNetwork | * | * | AUTORISER |
| AllowInternetOutBound | 65 001 | * | * | Internet | * | * | AUTORISER |
| DenyAllOutBound | 65 500 | * | * | * | * | * | REFUSER |

## <a name="associating-nsgs"></a>Association de groupe de sécurité réseau
Vous pouvez associer un tooVMs du groupe de sécurité réseau, cartes réseau et les sous-réseaux, selon le modèle de déploiement hello que vous utilisez, comme suit :

* **Machine virtuelle (classique uniquement) :** règles de sécurité sont appliquées tooall trafic vers/depuis hello machine virtuelle. 
* **Carte réseau (Resource Manager uniquement) :** règles de sécurité sont appliquées tooall trafic vers/depuis hello de carte réseau hello NSG n’est associé à. Dans une machine virtuelle multi-NIC, vous pouvez appliquer différents (ou même hello) tooeach du groupe de sécurité réseau NIC individuellement. 
* **Sous-réseau (Gestionnaire de ressources et standard) :** règles de sécurité sont appliquées tooany trafic vers/à partir de toutes les ressources connectées toohello réseau virtuel.

Vous pouvez associer des différents groupes de sécurité réseau tooa machine virtuelle (ou carte réseau, en fonction du modèle de déploiement hello) et hello sous-réseau connecté à une carte réseau ou une machine virtuelle. Les règles de sécurité est appliqués toohello trafic, par priorité, chaque groupe de sécurité réseau, Bonjour les suivantes : ordre :

- **Trafic entrant**

  1. **Groupe de sécurité réseau appliqué toosubnet :** si un groupe de sécurité réseau du sous-réseau a un trafic de toodeny règle correspondante, les paquets hello sont supprimé.

  2. **Groupe de sécurité réseau appliqué tooNIC** (Resource Manager) ou la machine virtuelle (classique) : si groupe de sécurité réseau VM\NIC a une règle de correspondance qui refuse le trafic, les paquets sont ignorés à hello VM\NIC, même si un groupe de sécurité réseau de sous-réseau possède une règle de correspondance qui autorise le trafic.

- **Trafic sortant**

  1. **Groupe de sécurité réseau appliqué tooNIC** (Resource Manager) ou la machine virtuelle (classique) : si un groupe de sécurité réseau VM\NIC a une règle de correspondance qui refuse le trafic, les paquets sont ignorés.

  2. **Groupe de sécurité réseau appliqué toosubnet :** si un groupe de sécurité réseau de sous-réseau possède une règle de correspondance qui refuse le trafic, les paquets sont ignorés, même si un groupe de sécurité réseau VM\NIC a une règle de correspondance qui autorise le trafic.

> [!NOTE]
> Bien que vous ne pouvez associer un seul groupe de sécurité réseau tooa sous-réseau, machine virtuelle ou carte réseau ; Vous pouvez associer hello même groupe de sécurité réseau tooas beaucoup de ressources que vous le souhaitez.
>

## <a name="implementation"></a>Implémentation
Vous pouvez implémenter des groupes de sécurité réseau dans hello Gestionnaire de ressources ou des modèles de déploiement classique à l’aide de hello suite d’outils :

| Outil de déploiement | Classique | Gestionnaire de ressources |
| --- | --- | --- |
| Portail Azure   | Oui | [Oui](virtual-networks-create-nsg-arm-pportal.md) |
| PowerShell     | [Oui](virtual-networks-create-nsg-classic-ps.md) | [Oui](virtual-networks-create-nsg-arm-ps.md) |
| Azure CLI **V1**   | [Oui](virtual-networks-create-nsg-classic-cli.md) | [Oui](virtual-networks-create-nsg-cli-nodejs.md) |
| Azure CLI **V2**   | Non | [Oui](virtual-networks-create-nsg-arm-cli.md) |
| Modèle Azure Resource Manager   | Non  | [Oui](virtual-networks-create-nsg-arm-template.md) |

## <a name="planning"></a>Planification
Avant d’implémenter des groupes de sécurité réseau, vous devez hello tooanswer suivant questions :

1. Les types de ressources voulez-vous tooor de trafic toofilter de ? Vous pouvez connecter des ressources telles que des NIC (Resource Manager), des machines virtuelles (Classic), des services cloud, des environnements App Service et VM Scale Sets. 
2. Sont des ressources hello toofilter du trafic à partir de toosubnets connectés dans des réseaux virtuels existants ?

Pour plus d’informations sur la planification de la sécurité réseau dans Azure, consultez hello [services de cloud computing et de sécurité réseau](../best-practices-network-security.md) l’article. 

## <a name="design-considerations"></a>Remarques relatives à la conception
Une fois que vous connaissez les réponses hello questions toohello Bonjour [planification](#Planning) section, passez en revue les hello les sections suivantes avant de définir vos groupes de sécurité réseau :

### <a name="limits"></a>limites
Il existe des limites de nombre toohello de groupes de sécurité réseau que vous pouvez avoir un abonnement et le nombre de règles par groupe de sécurité réseau. toolearn plus d’informations sur les limites de hello, lire hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.

### <a name="vnet-and-subnet-design"></a>Conception de réseau virtuel et de sous-réseau
Étant donné que les groupes de sécurité réseau peuvent être appliqués toosubnets, vous pouvez réduire le nombre hello de groupes de sécurité réseau par vos ressources de regroupement par sous-réseau et en appliquant des groupes de sécurité réseau toosubnets.  Si vous décidez de toosubnets des groupes de sécurité réseau tooapply, vous découvrirez peut-être que réseaux virtuels existants et les sous-réseaux que vous avez pas définis avec des groupes de sécurité réseau à l’esprit. Vous pouvez peut-être toodefine toosupport nouveaux réseaux virtuels et sous-réseaux la conception de votre groupe de sécurité réseau et déployer vos nouvelles ressources tooyour nouveaux sous-réseaux. Vous pouvez ensuite définir un toomove de stratégie de migration existant de nouveaux sous-réseaux de ressources toohello. 

### <a name="special-rules"></a>Règles spéciales
Si vous bloquez le trafic autorisé en suivant les règles de hello, votre infrastructure ne peut pas communiquer avec les services Azure essentiels :

* **Adresse IP virtuelle du nœud de l’hôte hello :** infrastructure de base des services tels que DHCP, DNS et contrôle d’intégrité sont fournis via l’hôte virtualisé de hello l’adresse IP 168.63.129.16. Cette adresse IP publique appartient tooMicrosoft et est hello seule adresse IP virtualisée utilisée dans toutes les régions à cet effet. Cette adresse IP mappe toohello adresse IP physique de l’ordinateur de serveur hello (nœud hôte) hébergeant hello machine virtuelle. nœud de l’hôte Hello joue le rôle sonde d’intégrité d’équilibrage de charge relais DHCP de hello, la résolution DNS récursive hello et source de sonde hello pour hello sonde d’intégrité hello machine. Adresse IP de toothis communication n’est pas une attaque.
* **Gestion des licences (Service de gestion de clés) :** les images Windows en cours d’exécution sur les machines virtuelles doivent être acquises sous licence. tooensure de licences, une demande est envoyée serveurs hôte de Service de gestion de clés toohello qui gèrent de telles requêtes. Hello est demandé sortant via le port 1688.

### <a name="icmp-traffic"></a>Trafic ICMP
règles de groupe de sécurité réseau actuellement Hello autorisent uniquement pour les protocoles *TCP* ou *UDP*. Il n’existe aucune balise spécifique pour *ICMP*. Toutefois, le trafic ICMP est autorisé dans un réseau virtuel par règle hello AllowVNetInBound par défaut, qui permet de tooand le trafic à partir de n’importe quel port et le protocole dans hello réseau virtuel.

### <a name="subnets"></a>Sous-réseaux
* Tenez compte nombre hello des niveaux de que votre charge de travail nécessite. Chaque couche peut être isolée à l’aide d’un sous-réseau, avec un sous-réseau de toohello NSG appliqué. 
* Si vous devez tooimplement un sous-réseau pour une passerelle VPN ou un circuit ExpressRoute, **pas** s’appliquent à un sous-réseau de toothat du groupe de sécurité réseau. Si vous le faites, la connectivité entre réseaux virtuels ou entre différents locaux risque de ne pas fonctionner. 
* Si vous devez tooimplement une appliance virtuelle de réseau (NVA), se connecter propre sous-réseau de hello NVA tooits et créer des itinéraires définis par l’utilisateur (UDR) tooand à partir de hello NVA. Vous pouvez implémenter un niveau de sous-réseau du trafic toofilter de groupe de sécurité réseau dans et hors de ce sous-réseau. toolearn plus d’informations sur UDRs, lecture hello [itinéraires définis par l’utilisateur](virtual-networks-udr-overview.md) l’article.

### <a name="load-balancers"></a>Équilibreurs de charge
* Adresse de réseau et de l’équilibrage de charge hello, respectez les règles de translation (NAT) pour chaque équilibrage de charge utilisé par chacune de vos charges de travail. Les règles NAT sont pool principal lié tooa qui contient les instances de rôle Services de machines virtuelles/Cloud (classiques) ou les cartes réseau (Resource Manager). Envisagez de créer un groupe de sécurité réseau pour chaque pool principal, ce qui permet uniquement le trafic mappé via les règles de hello implémentés dans les équilibreurs de charge hello. Création d’un groupe de sécurité réseau pour chaque pool principal garantit que le trafic provenant de pool principal de toohello directement (plutôt que via l’équilibrage de charge hello), sont également filtrées.
* Déploiements classiques, vous permet de créer des points de terminaison qui mappent des ports sur un tooports d’équilibrage de charge sur vos machines virtuelles ou les instances de rôle. Vous pouvez également créer votre propre équilibreur de charge public individuel par le biais de Resource Manager. port de destination Hello pour le trafic entrant est le port effectivement hello hello machine virtuelle ou instance de rôle, pas le port hello exposé par un équilibrage de charge. port source de Hello et l’adresse de toohello de connexion hello sur que machine virtuelle est un port et une adresse hello ordinateur distant Bonjour Internet, pas port de hello et l’adresse exposées par l’équilibrage de charge hello.
* Lorsque vous créez des groupes de sécurité réseau toofilter le trafic passant par un équilibreur de charge interne (ILB), hello source port et adresse plage appliquée proviennent de hello ordinateur, l’équilibrage de charge hello pas d’origine. plage de port et l’adresse de destination Hello sont celles de l’ordinateur de destination hello, équilibrage de charge hello pas.

### <a name="other"></a>Autres
* Listes de contrôle d’accès basé sur le point de terminaison (ACL) et les groupes de sécurité réseau ne sont pas pris en charge sur hello même instance de machine virtuelle. Si vous souhaitez toouse un groupe de sécurité réseau et que vous disposez déjà d’un point de terminaison ACL en place, tout d’abord supprimer les ACL du point de terminaison de hello. Pour plus d’informations sur la façon tooremove un point de terminaison ACL, consultez hello [gérer les ACL de point de terminaison](virtual-networks-acl-powershell.md) l’article.
* Dans le Gestionnaire de ressources, vous pouvez utiliser une carte réseau de tooa groupe de sécurité réseau associé pour les machines virtuelles avec la gestion des tooenable plusieurs cartes réseau (accès à distance) sur une base par carte de réseau. Association tooeach de groupes de sécurité réseau unique carte réseau permet de séparer des types de trafic entre les cartes réseau.
* Utilisation de toohello similaire d’équilibreurs de charge, lors du filtrage du trafic à partir d’autres réseaux virtuels, vous devez utiliser plage d’adresses hello source d’ordinateur distant hello, pas les passerelle hello connexion hello des réseaux virtuels.
* De nombreux services Azure ne peut pas être tooVNets connecté. Si une ressource Azure n’est pas connecté tooa réseau virtuel, vous ne pouvez pas utiliser une ressource de groupe de sécurité réseau toofilter trafic toohello.  Lire la documentation hello pour les services de hello utiliser toodetermine si le service de hello peut être connecté tooa réseau virtuel.

## <a name="sample-deployment"></a>Exemple de déploiement
tooillustrate l’application hello d’informations de hello dans cet article, envisagez un scénario courant d’une application à deux niveaux illustré hello illustration suivante :

![Groupes de sécurité réseau](./media/virtual-network-nsg-overview/figure1.png)

Comme indiqué dans le diagramme de hello, hello *Web1* et *Web2* les machines virtuelles sont connectée toohello *frontal* sous-réseau et hello *DB1* et *DB2* les machines virtuelles sont connectée toohello *principal* sous-réseau.  Les deux sous-réseaux font partie de hello *TestVNet* réseau virtuel. chaque composants d’application Hello s’exécutent dans un réseau virtuel de tooa Azure VM connecté. scénario de Hello a hello suivant les exigences :

1. Séparation du trafic entre hello WEB et les serveurs de base de données.
2. Équilibrage de transférer le trafic de règles à partir de serveurs web de tooall d’équilibrage de charge hello sur le port 80.
3. La charge du trafic vers l’avant du règles NAT équilibrage sera disponible dans l’équilibrage de charge hello sur tooport 50001 port 3389 sur hello WEB1 VM.
4. Aucun toohello accès frontal ou principal des ordinateurs virtuels à partir de hello Internet, à l’exception des exigences 2 et 3.
5. Aucun accès Internet sortant à partir de serveurs WEB ou de la base de données de hello.
6. Accès à partir du sous-réseau du serveur frontal hello est autorisé tooport 3389 de n’importe quel serveur web.
7. Accès à partir du sous-réseau du serveur frontal hello est autorisé tooport 3389 de n’importe quel serveur de base de données.
8. Accès à partir du sous-réseau du serveur frontal hello est autorisé tooport 1433 de tous les serveurs de base de données.
9. Séparation du trafic de gestion (port 3389) et du trafic de base de données (1433) sur les différentes NIC des serveurs de base de données

Exigences de 1 à 6 (à l’exception de la configuration requise, 3 et 4) sont tous les espaces toosubnet restreints. Hello NSG suivant exigences hello précédente, tout en réduisant le nombre de hello de groupes de sécurité réseau requis :

### <a name="frontend"></a>FrontEnd
**Règles de trafic entrant**

| Règle | Access | Priorité | Plage d’adresses source | Port source | Plage d’adresses de destination | Port de destination | Protocole |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-HTTP-Internet | AUTORISER | 100 | Internet | * | * | 80 | TCP |
| Allow-Inbound-RDP-Internet | AUTORISER | 200 | Internet | * | * | 3389 | TCP |
| Deny-Inbound-All | REFUSER | 300 | Internet | * | * | * | TCP |

**Règles de trafic sortant**

| Règle | Access | Priorité | Plage d’adresses source | Port source | Plage d’adresses de destination | Port de destination | Protocole |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All |REFUSER |100 | * | * | Internet | * | * |

### <a name="backend"></a>BackEnd
**Règles de trafic entrant**

| Règle | Access | Priorité | Plage d’adresses source | Port source | Plage d’adresses de destination | Port de destination | Protocole |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All | REFUSER | 100 | Internet | * | * | * | * |

**Règles de trafic sortant**

| Règle | Access | Priorité | Plage d’adresses source | Port source | Plage d’adresses de destination | Port de destination | Protocole |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Internet-All | REFUSER | 100 | * | * | Internet | * | * |

Hello, groupes de sécurité réseau suivants sont créés et associés tooNICs Bonjour suivant des machines virtuelles :

### <a name="web1"></a>WEB1
**Règles de trafic entrant**

| Règle | Access | Priorité | Plage d’adresses source | Port source | Plage d’adresses de destination | Port de destination | Protocole |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Internet | AUTORISER | 100 | Internet | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet | AUTORISER | 200 | Internet | * | * | 80 | TCP |

> [!NOTE]
> plage d’adresses source Hello pour les règles précédentes hello est **Internet**, pas hello adresse IP virtuelle d’équilibrage de charge hello. le port source Hello est *, pas 500001. Les règles NAT pour les équilibreurs de charge ne sont pas hello même en tant que règles de sécurité de groupe de sécurité réseau. Les règles de sécurité de groupe de sécurité réseau sont toujours associées toohello d’origine et la destination finale du trafic, **pas** équilibrage de charge hello entre hello deux. 
> 
> 

### <a name="web2"></a>WEB2
**Règles de trafic entrant**

| Règle | Access | Priorité | Plage d’adresses source | Port source | Plage d’adresses de destination | Port de destination | Protocole |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Deny-Inbound-RDP-Internet | REFUSER | 100 | Internet | * | * | 3389 | TCP |
| Allow-Inbound-HTTP-Internet | AUTORISER | 200 | Internet | * | * | 80 | TCP |

### <a name="db-servers-management-nic"></a>Serveurs de base de données (NIC de gestion)
**Règles de trafic entrant**

| Règle | Access | Priorité | Plage d’adresses source | Port source | Plage d’adresses de destination | Port de destination | Protocole |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-RDP-Front-end | AUTORISER | 100 | 192.168.1.0/24 | * | * | 3389 | TCP |

### <a name="db-servers-database-traffic-nic"></a>Serveurs de base de données (NIC du trafic de base de données)
**Règles de trafic entrant**

| Règle | Access | Priorité | Plage d’adresses source | Port source | Plage d’adresses de destination | Port de destination | Protocole |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Allow-Inbound-SQL-Front-end | AUTORISER | 100 | 192.168.1.0/24 | * | * | 1433 | TCP |

Étant donné que certains des groupes de sécurité réseau hello sont associé tooindividual de cartes réseau, les règles de hello sont pour les ressources déployées par le biais du Gestionnaire de ressources. Les règles sont combinées pour le sous-réseau et la NIC, selon leur mode d’association. 

## <a name="next-steps"></a>Étapes suivantes
* [Déployer les NSG (Resource Manager)](virtual-networks-create-nsg-arm-pportal.md)
* [Déployer les NSG (Classic)](virtual-networks-create-nsg-classic-ps.md)
* [Gestion des journaux de groupe de sécurité réseau](virtual-network-nsg-manage-log.md).
* [Résoudre les problèmes relatifs aux NSG] (virtual-network-nsg-troubleshoot-portal.md)
