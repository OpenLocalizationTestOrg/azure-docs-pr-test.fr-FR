---
title: "aaaAzure FAQ sur le réseau virtuel | Documents Microsoft"
description: "Toohello réponses plus fréquemment posées sur les réseaux virtuels Microsoft Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 54bee086-a8a5-4312-9866-19a1fba913d0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/18/2017
ms.author: jdial
ms.openlocfilehash: c2f9faee41b9c45e8bb196c58282d597ae732e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-network-frequently-asked-questions-faq"></a>FAQ sur les réseaux virtuels Azure

## <a name="virtual-network-basics"></a>Concepts de base du réseau virtuel

### <a name="what-is-an-azure-virtual-network-vnet"></a>Qu’est un réseau virtuel (VNet) Azure ?
Un réseau virtuel de Azure (VNet) est une représentation de votre propre réseau dans le cloud de hello. Il s’agit d’une isolation logique de hello Azure cloud dédié tooyour abonnement. Vous pouvez utiliser des réseaux virtuels tooprovision et gérer des réseaux privés virtuels (VPN) dans Azure et, éventuellement, hello de lien avec les autres réseaux virtuels dans Azure, ou avec votre site sur des réseaux virtuels informatique toocreate hybride ou intersite solutions d’infrastructure. Chaque réseau virtuel que vous créez a son propre bloc CIDR et permettre d’être lié tooother réseaux locaux et des réseaux virtuels tant que blocs CIDR hello ne se chevauchent pas. Vous avez également le contrôle des paramètres du serveur DNS pour les réseaux virtuels et la segmentation de réseau virtuel de hello en sous-réseaux.

Utilisez les réseaux virtuels pour effectuer les actions suivantes :

* Créer un réseau virtuel cloud uniquement privé dédié Vous n’avez pas toujours besoin d’une configuration intersite pour votre solution. Lorsque vous créez un réseau virtuel, vos services et machines virtuelles au sein de votre réseau virtuel peuvent communiquer directement et en toute sécurité entre eux dans le cloud de hello. Cela conserve le trafic en toute sécurité au sein de hello réseau virtuel, mais vous permet toujours de tooconfigure des connexions de point de terminaison pour les ordinateurs virtuels de hello et services qui requièrent la communication Internet dans le cadre de votre solution.
* Étendez en toute sécurité votre centre de données avec des réseaux virtuels, vous pouvez créer à l’échelle traditionnel toosecurely (S2S) VPN de site à site la capacité de votre centre de données. Réseaux privés virtuels S2S utiliser IPSEC tooprovide une connexion sécurisée entre votre passerelle VPN d’entreprise et de Azure.
* Scénarios de cloud hybride activer que des réseaux virtuels vous donnent hello flexibilité toosupport un éventail de scénarios de cloud hybride. Vous pouvez connecter en toute sécurité des applications basées sur le cloud tooany type local et du système telles que des grands systèmes systèmes Unix.

### <a name="how-do-i-know-if-i-need-a-vnet"></a>Comment savoir si j’ai besoin d’un réseau virtuel ?
Hello [vue d’ensemble du réseau virtuel](virtual-networks-overview.md) article fournit une table de décision qui vous permet de déterminer l’option de conception de réseau meilleures hello pour vous.

### <a name="how-do-i-get-started"></a>Comment faire pour démarrer ?
Visitez hello [documentation sur le réseau virtuel](https://docs.microsoft.com/azure/virtual-network/) tooget a démarré. Ce document fournit des informations de présentation et de déploiement pour toutes les fonctionnalités de réseau virtuel hello.

### <a name="can-i-use-vnets-without-cross-premises-connectivity"></a>Puis-je utiliser des réseaux virtuels sans connectivité intersite ?
Oui. Vous pouvez utiliser un réseau virtuel sans connectivité hybride. Cela est particulièrement utile si vous souhaitez que les contrôleurs de domaine Active Directory Microsoft Windows Server toorun et batteries de serveurs SharePoint dans Azure.

### <a name="can-i-perform-wan-optimization-between-vnets-or-a-vnet-and-my-on-premises-data-center"></a>Puis-je exécuter une optimisation WAN entre des réseaux virtuels ou entre un réseau virtuel et mon centre de données local ?

Oui. Vous pouvez déployer un [appliance virtuelle de réseau WAN optimisation](https://azure.microsoft.com/marketplace/?term=wan+optimization) à partir de plusieurs fournisseurs via hello Azure Marketplace.

## <a name="configuration"></a>Configuration

### <a name="what-tools-do-i-use-toocreate-a-vnet"></a>Que faire outils utiliser toocreate un réseau virtuel ?
Vous pouvez utiliser hello suivant outils toocreate ou configurer un réseau virtuel :

* Portail Azure (pour les réseaux virtuels classiques et Resource Manager).
* Fichier de configuration réseau (netcfg - pour les réseaux virtuels classiques uniquement). Consultez hello [configurer un réseau virtuel à l’aide d’un fichier de configuration réseau](virtual-networks-using-network-configuration-file.md) l’article.
* PowerShell (pour les réseaux virtuels classiques et Resource Manager).
* Interface de ligne de commande Azure (pour les réseaux virtuels classiques et Resource Manager).

### <a name="what-address-ranges-can-i-use-in-my-vnets"></a>Quelles plages d’adresses puis-je utiliser dans mes réseaux virtuels ?
Toute plage d’adresses IP définie dans [RFC 1918](http://tools.ietf.org/html/rfc1918). Par exemple, 10.0.0.0/16.

### <a name="can-i-have-public-ip-addresses-in-my-vnets"></a>Puis-je avoir des adresses IP publiques dans mes réseaux virtuels ?
Oui. Pour plus d’informations sur les plages d’adresses IP publiques, consultez hello [espace d’adressage IP Public dans un réseau virtuel](virtual-networks-public-ip-within-vnet.md) l’article. Vos adresses IP publiques ne sera pas directement accessibles depuis Internet de hello.

### <a name="is-there-a-limit-toohello-number-of-subnets-in-my-vnet"></a>Existe-t-il un toohello limiter le nombre de sous-réseaux dans mon réseau virtuel ?
Oui. Hello de lecture [Azure limite](../azure-subscription-service-limits.md#networking-limits) article pour plus d’informations. Les espaces d’adressage de sous-réseau ne peuvent pas se chevaucher.

### <a name="are-there-any-restrictions-on-using-ip-addresses-within-these-subnets"></a>Existe-t-il des restrictions sur l’utilisation des adresses IP au sein de ces sous-réseaux ?
Oui. Azure réserve des adresses IP dans chaque sous-réseau. Hello prénom et adresses IP des sous-réseaux de hello sont réservés pour la conformité de protocole, ainsi que de 3 plus d’adresses utilisées pour les services Azure.

### <a name="how-small-and-how-large-can-vnets-and-subnets-be"></a>Quelle taille peuvent avoir les réseaux virtuels et les sous-réseaux ?
sous-réseau de plus petite Hello que nous prenons en charge est/29 et hello plus grande est/8 (à l’aide de définitions de sous-réseau CIDR).

### <a name="can-i-bring-my-vlans-tooazure-using-vnets"></a>Puis-je afficher mon tooAzure de réseaux locaux virtuels à l’aide de réseaux virtuels ?
Non. Les réseaux virtuels sont des superpositions de couche 3. Azure ne prend en charge aucune sémantique de couche 2.

### <a name="can-i-specify-custom-routing-policies-on-my-vnets-and-subnets"></a>Puis-je spécifier des stratégies de routage personnalisées sur des réseaux virtuels et des sous-réseaux ?
Oui. Vous pouvez utiliser le routage défini par utilisateur (UDR, User Defined Routing). Pour plus d’informations sur l’UDR, voir [Itinéraires définis d’utilisateur et transfert IP](virtual-networks-udr-overview.md).

### <a name="do-vnets-support-multicast-or-broadcast"></a>Les réseaux virtuels prennent-ils en charge la multidiffusion ou la diffusion ?
Non. Nous ne prenons pas en charge la multidiffusion ou la diffusion.

### <a name="what-protocols-can-i-use-within-vnets"></a>Quels protocoles puis-je utiliser au sein de réseaux virtuels ?
Vous pouvez utiliser les protocoles TCP, UDP et ICMP TCP/IP au sein des réseaux virtuels. La multidiffusion, la diffusion, les paquets encapsulés IP dans IP et les paquets Encapsulation générique de routage (GRE, Generic Routing Encapsulation) sont bloqués dans les réseaux virtuels. 

### <a name="can-i-ping-my-default-routers-within-a-vnet"></a>Puis-je effectuer un test Ping sur mes routeurs par défaut au sein d’un réseau virtuel ?
Non.

### <a name="can-i-use-tracert-toodiagnose-connectivity"></a>Puis-je utiliser tracert toodiagnose connectivité ?
Non.

### <a name="can-i-add-subnets-after-hello-vnet-is-created"></a>Puis-je ajouter des sous-réseaux après hello que réseau virtuel est créé ?
Oui. Sous-réseaux peuvent être ajoutés tooVNets à tout moment tant que l’adresse de sous-réseau hello ne fait pas partie d’un autre sous-réseau hello réseau virtuel.

### <a name="can-i-modify-hello-size-of-my-subnet-after-i-create-it"></a>Puis-je modifier taille hello de mon sous-réseau une fois le créer ?
Oui. Vous pouvez ajouter, supprimer, développer ou réduire un sous-réseau si aucune machine virtuelle ou aucun service n’y est déployé.

### <a name="can-i-modify-subnets-after-i-created-them"></a>Puis-je modifier des sous-réseaux après leur création ?
Oui. Vous pouvez ajouter, supprimer et modifier des blocs CIDR hello utilisés par un réseau virtuel.

### <a name="can-i-connect-toohello-internet-if-i-am-running-my-services-in-a-vnet"></a>Puis-je connecter toohello internet si j’exécute mon services dans un réseau virtuel ?
Oui. Tous les services déployés au sein d’un réseau virtuel peuvent se connecter toohello internet. Chaque service cloud déployé dans Azure a une adresse IP virtuelle publiquement adressable affectée tooit. Avoir toodefine des points de terminaison d’entrée pour les rôles PaaS et pour les machines virtuelles tooenable ces connexions à partir de hello tooaccept des services internet.

### <a name="do-vnets-support-ipv6"></a>Les réseaux virtuels prennent-ils en charge IPv6 ?
Non. Vous ne pouvez pas utiliser IPv6 avec les réseaux virtuels pour l’instant.

### <a name="can-a-vnet-span-regions"></a>Un réseau virtuel peut-il couvrir plusieurs régions ?
Non. Un réseau virtuel est limité tooa une seule région.

### <a name="can-i-connect-a-vnet-tooanother-vnet-in-azure"></a>Puis-je connecter un réseau virtuel dans Azure de tooanother réseau virtuel ?
Oui. Vous pouvez vous connecter à un réseau virtuel tooanother réseau virtuel à l’aide de :
- Une passerelle VPN Azure. Hello de lecture [configurer une connexion réseau à](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article pour plus d’informations. 
- L’homologation de réseaux virtuels. Hello de lecture [vue d’ensemble d’homologation du réseau virtuel](virtual-network-peering-overview.md) article pour plus d’informations.

## <a name="name-resolution-dns"></a>Résolution de noms pour les machines virtuelles et les instances de rôle

### <a name="what-are-my-dns-options-for-vnets"></a>Quelles sont les options DNS pour les réseaux virtuels ?
Table de décision utilisez hello sur hello [résolution de noms pour les machines virtuelles et Instances de rôle](virtual-networks-name-resolution-for-vms-and-role-instances.md) tooguide page tous les hello DNS options disponibles.

### <a name="can-i-specify-dns-servers-for-a-vnet"></a>Puis-je spécifier des serveurs DNS pour un réseau virtuel ?
Oui. Vous pouvez spécifier des adresses IP de serveur DNS dans les paramètres de réseau virtuel hello. Elle sera appliquée en tant que hello ou les serveurs DNS par défaut pour toutes les machines virtuelles dans hello réseau virtuel.

### <a name="how-many-dns-servers-can-i-specify"></a>Combien de serveurs DNS puis-je spécifier ?
Hello de référence [Azure limite](../azure-subscription-service-limits.md#networking-limits) article pour plus d’informations.

### <a name="can-i-modify-my-dns-servers-after-i-have-created-hello-network"></a>Puis-je modifier mes serveurs DNS une fois que j’ai créé le réseau de hello ?
Oui. Vous pouvez modifier la liste des serveurs DNS hello pour votre réseau virtuel à tout moment. Si vous modifiez la liste des serveurs DNS, vous devez toorestart des machines virtuelles de hello dans votre réseau virtuel pour qu’ils toopick serveur DNS de la nouvelle hello.

### <a name="what-is-azure-provided-dns-and-does-it-work-with-vnets"></a>Qu’est ce qu’un serveur DNS fourni par Azure et fonctionne-t-il avec les réseaux virtuels ?
Le serveur DNS fourni par Azure est un serveur DNS mutualisé proposé par Microsoft. Azure enregistre toutes vos machines virtuelles et instances de rôle de service cloud dans ce service. Ce service fournit la résolution de noms par nom d’hôte pour les machines virtuelles et instances de rôle contenues dans hello même service cloud et par nom de domaine complet pour les machines virtuelles et instances de rôle dans hello même réseau virtuel. Hello de lecture [résolution de noms pour les machines virtuelles et Instances de rôle](virtual-networks-name-resolution-for-vms-and-role-instances.md) toolearn article plus sur le système DNS.

> [!NOTE]
> Il existe une limite à cette toohello temps tout d’abord 100 services de cloud computing dans un réseau virtuel pour la résolution de nom entre locataires utilisant un DNS fourni par Azure. Si vous utilisez votre propre serveur DNS, cette restriction ne s’applique pas.
> 
> 

### <a name="can-i-override-my-dns-settings-on-a-per-vm--service-basis"></a>Puis-je remplacer mes paramètres DNS sur la base machine virtuelle/service ?
Oui. Vous pouvez définir les serveurs DNS sur un par cloud service base toooverride hello paramètres par défaut. Toutefois, nous vous recommandons d’utiliser autant que possible le DNS à l’échelle du réseau.

### <a name="can-i-bring-my-own-dns-suffix"></a>Puis-je afficher mon propre suffixe DNS ?
Non. Vous ne pouvez pas spécifier un suffixe DNS personnalisé pour vos réseaux virtuels.

## <a name="connecting-virtual-machines"></a>Connexion aux machines virtuelles

### <a name="can-i-deploy-vms-tooa-vnet"></a>Puis-je déployer des machines virtuelles tooa réseau virtuel ?
Oui. Tous les tooa d’interfaces (NIC) connectées réseau machine virtuelle déployée via le modèle de déploiement du Gestionnaire de ressources hello doit être connecté tooa réseau virtuel. Ordinateurs virtuels déployés via le modèle de déploiement classique hello peuvent éventuellement être connecté tooa réseau virtuel.

### <a name="what-are-hello-different-types-of-ip-addresses-i-can-assign-toovms"></a>Quels sont hello différents types d’adresses IP tooVMs puis-je attribuer ?
* **Privé :** affecté tooeach carte réseau sur chaque machine virtuelle. adresse de Hello est affecté à l’aide d’une méthode statique ou dynamique de hello. Les adresses IP privées sont affectés à partir de la plage hello que vous avez spécifié dans les paramètres de sous-réseau hello de votre réseau virtuel. Ressources déployées via le modèle de déploiement classique de hello sont affectées des adresses IP privées, même s’ils ne sont pas connectés tooa réseau virtuel. Une adresse IP privée avec le reste de méthode dynamique hello affecté tooa ressource jusqu'à la suppression de ressources de hello (machines virtuelles ou Cloud Service emplacements de déploiement). Une adresse IP privée assignée avec la méthode dynamique hello peut changer lors d’une machine virtuelle est redémarrée après avoir Bonjour arrêtée (désallouée) d’état. Une adresse IP privée attribuée avec hello méthode statique reste affectée tooa ressources jusqu'à ce que la ressource de hello est supprimée. Si vous avez besoin de tooensure cette adresse IP privée de hello pour une ressource ne change jamais tant que ressource de hello est supprimée, affecter une adresse IP privée avec la méthode statique hello.
* **Public :** tooNICs éventuellement attribué attaché tooVMs déployés via le modèle de déploiement du Gestionnaire de ressources Azure hello. adresse de Hello peut être affectée à la méthode d’allocation statique ou dynamique hello. Instances de rôle de tous les ordinateurs virtuels et Services de cloud computing déployés via le modèle de déploiement classique hello existent dans un service cloud, qui est attribué un *dynamique*, public adresse IP virtuelle (VIP). Une adresse IP *statique* publique, appelée [Adresse IP réservée](virtual-networks-reserved-public-ip.md), peut éventuellement être attribuée en tant qu’adresse IP virtuelle. Vous pouvez affecter publique tooindividual d’adresses IP instances de rôle des machines virtuelles ou Services de cloud computing déployés via le modèle de déploiement classique hello. Ces adresses sont appelées [Adresses IP publiques de niveau d’instance (ILPIP)](virtual-networks-instance-level-public-ip.md) et elles peuvent être attribuées de manière dynamique.

### <a name="can-i-reserve-a-private-ip-address-for-a-vm-that-i-will-create-at-a-later-time"></a>Puis-je réserver une adresse IP privée pour une machine virtuelle que je créerai ultérieurement ?
Non. Vous ne pouvez pas réserver d’adresse IP privée. Si une adresse IP privée est disponible lui est affecté tooa machine virtuelle ou instance de rôle par le serveur DHCP hello. Que la machine virtuelle peut ou ne peut pas être hello celui que vous voulez hello privé IP adresse toobe assigné à. Vous pouvez toutefois modifier hello adresse IP privée une déjà créé VM tooany privée adresse IP disponible.

### <a name="do-private-ip-addresses-change-for-vms-in-a-vnet"></a>Les adresses IP privées peuvent-elles changer pour les machines virtuelles d’un réseau virtuel ?
Cela dépend. Les adresses IP privées dynamiques restent associées à une machine virtuelle jusqu’à ce que celle-ci soit arrêtée (libérée) ou supprimée. Les adresses IP privées statiques ne sont libérées d’une machine virtuelle que lorsque celle-ci est supprimée.

### <a name="can-i-manually-assign-ip-addresses-toonics-within-hello-vm-operating-system"></a>Pouvez-vous attribuer manuellement des tooNICs d’adresses IP au sein du système d’exploitation de l’ordinateur virtuel hello ?
Oui, mais cela n’est pas recommandé. Modification manuelle des adresses IP de hello pour une carte réseau au sein du système d’exploitation de l’ordinateur virtuel pourrait endommager toolosing connectivité toohello machine virtuelle si hello adresse IP tooa carte réseau au sein de hello Azure VM ont été toochange.

### <a name="what-happens-toomy-ip-addresses-if-i-stop-a-cloud-service-deployment-slot-or-shutdown-a-vm-from-within-hello-operating-system"></a>Que passe-t-il toomy des adresses IP si vous arrêtez un emplacement de déploiement de Service Cloud ou de l’arrêt d’une machine virtuelle du système d’exploitation de hello ?
Rien. les adresses IP Hello (VIP publique, public et privé) restent emplacement de déploiement de service de cloud toohello attribué ou la machine virtuelle. Les adresses dynamiques ne sont libérées que si une machine virtuelle est arrêtée (libérée) ou supprimée, ou si un emplacement de déploiement de services cloud est supprimé. En cliquant sur hello **arrêter** bouton pour une machine virtuelle dans hello portail Azure définit son tooStopped état (désalloué). Dans ce cas, hello VM perdrez ses adresses IP.

### <a name="can-i-move-vms-from-one-subnet-tooanother-subnet-in-a-vnet-without-re-deploying"></a>Puis-je déplacer les machines virtuelles d’un sous-réseau de tooanother de sous-réseau dans un réseau virtuel sans redéploiement ?
Oui. Vous trouverez plus d’informations Bonjour [comment toomove un ordinateur virtuel ou un rôle de l’instance tooa autre sous-réseau](virtual-networks-move-vm-role-to-subnet.md) l’article.

### <a name="can-i-configure-a-static-mac-address-for-my-vm"></a>Puis-je configurer une adresse MAC statique pour ma machine virtuelle ?
Non. Une adresse MAC ne peut pas être configurée de manière statique.

### <a name="will-hello-mac-address-remain-hello-same-for-my-vm-once-it-has-been-created"></a>Hello adresse MAC resteront identiques hello pour ma machine virtuelle une fois qu’il a été créé ?
Oui, hello adresse MAC reste hello que même pour une machine virtuelle déployé via hello Gestionnaire de ressources et les modèles de déploiement classique jusqu'à ce qu’il est supprimé. Auparavant, hello adresse MAC a été libéré si hello machine virtuelle a été arrêtée (désallouée), mais désormais adresse MAC de hello est conservée même si hello VM hello désalloué état.

### <a name="can-i-connect-toohello-internet-from-a-vm-in-a-vnet"></a>Puis-je connecter toohello internet à partir d’une machine virtuelle dans un réseau virtuel ?
Oui. Instances de rôle de tous les ordinateurs virtuels et Services de cloud computing déployés au sein d’un réseau virtuel peuvent se connecter à toohello Internet.

## <a name="azure-services-that-connect-toovnets"></a>Services Azure qui se connectent tooVNets

### <a name="can-i-use-azure-app-service-web-apps-with-a-vnet"></a>Puis-je utiliser Azure App Service Web Apps avec un réseau virtuel ?
Oui. Vous pouvez déployer des applications web à l’intérieur d’un réseau virtuel à l’aide d’ASE (App Service Environment). Toutes les applications web peuvent se connecter en toute sécurité et accéder aux ressources de votre réseau virtuel Azure si vous avez configuré une connexion de point à site pour votre réseau virtuel. Pour plus d’informations, consultez hello suivant des articles :

* [Création d'applications web dans un environnement App Service](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Intégrer une application à un réseau virtuel Azure](../app-service-web/web-sites-integrate-with-vnet.md)
* [Utilisation de l’intégration au réseau virtuel et des connexions hybrides avec les applications web](../app-service-web/web-sites-integrate-with-vnet.md#hybrid-connections-and-app-service-environments)

### <a name="can-i-deploy-cloud-services-with-web-and-worker-roles-paas-in-a-vnet"></a>Puis-je déployer des services cloud avec les rôles web et de travail (PaaS) dans un réseau virtuel ?
Oui. Vous pouvez déployer (facultatif) des instances de rôle de services cloud dans des réseaux virtuels. toodo par conséquent, vous spécifiez nom de réseau virtuel hello et mappages de rôle/sous-réseau hello dans la section de configuration de réseau hello de configuration de votre service. Il est inutile tooupdate vos fichiers binaires.

### <a name="can-i-connect-a-virtual-machine-scale-set-vmss-tooa-vnet"></a>Puis-je connecter un réseau virtuel de tooa définir de montée en puissance d’ordinateur virtuel (mise) ?
Oui. Vous devez vous connecter un tooa mise réseau virtuel.

### <a name="can-i-move-my-services-in-and-out-of-vnets"></a>Puis-je faire entrer ou sortir mes services dans les réseaux virtuels ?
Non. Impossible de faire entrer ou de faire sortir des services dans les réseaux virtuels. Vous avez toodelete et redéployez hello service toomove il tooanother réseau virtuel.

## <a name="security"></a>Sécurité

### <a name="what-is-hello-security-model-for-vnets"></a>Qu’est le modèle de sécurité hello pour les réseaux virtuels ?
Réseaux virtuels sont totalement isolées les unes des autres, et les autres services hébergés dans hello infrastructure Azure. Un réseau virtuel est une délimitation d’approbation.

### <a name="can-i-restrict-inbound-or-outbound-traffic-flow-toovnet-connected-resources"></a>Puis-je restreindre des ressources de tooVNet connecté de flux de trafic entrant ou sortant ?
Oui. Vous pouvez appliquer [groupes de sécurité réseau](virtual-networks-nsg.md) tooindividual sous-réseaux au sein d’un réseau virtuel, les cartes réseau attaché tooa réseau virtuel, ou les deux.

### <a name="can-i-implement-a-firewall-between-vnet-connected-resources"></a>Puis-je mettre en place un pare-feu entre les ressources connectées au réseau virtuel ?
Oui. Vous pouvez déployer un [appliance virtuelle de pare-feu réseau](https://azure.microsoft.com/en-us/marketplace/?term=firewall) à partir de plusieurs fournisseurs via hello Azure Marketplace.

### <a name="is-there-information-available-about-securing-vnets"></a>Existe-t-il des informations sur la sécurisation des réseaux virtuels ?
Oui. Consultez hello [présentation de la sécurité réseau Azure](../security/security-network-overview.md) article pour plus d’informations.

## <a name="apis-schemas-and-tools"></a>API, schémas et outils

### <a name="can-i-manage-vnets-from-code"></a>Puis-je gérer les réseaux virtuels à partir du code ?
Oui. Vous pouvez utiliser l’API REST pour les réseaux virtuels Bonjour [Azure Resource Manager](https://msdn.microsoft.com/library/mt163658.aspx) et [classique (gestion des services)](http://go.microsoft.com/fwlink/?LinkId=296833)) modèles de déploiement.

### <a name="is-there-tooling-support-for-vnets"></a>Existe-t-il une prise en charge des outils pour les réseaux virtuels ?
Oui. En savoir plus sur l’utilisation des éléments suivants :
- Hello toodeploy portail Azure des réseaux virtuels via hello [Azure Resource Manager](virtual-networks-create-vnet-arm-pportal.md) et [classique](virtual-networks-create-vnet-classic-pportal.md) modèles de déploiement.
- Toomanage PowerShell réseaux virtuels déployés via hello [le Gestionnaire de ressources](/powershell/resourcemanager/azurerm.network/v3.1.0/azurerm.network.md) et [classique](/powershell/module/azure/?view=azuresmps-3.7.0) modèles de déploiement.
- Hello [Azure interface de ligne de commande (CLI)](../virtual-machines/azure-cli-arm-commands.md#azure-network-commands-to-manage-network-resources) toomanage déployés via les deux modèles de déploiement des réseaux virtuels.  
