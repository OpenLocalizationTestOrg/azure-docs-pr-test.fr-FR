---
title: "mise en réseau aaaAzure | Documents Microsoft"
description: "Découvrez les fonctionnalités et les services de mise en réseau Azure."
services: networking
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: jdial
ms.openlocfilehash: 18945d139427f2e65138c0fd223e663fa46e9211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking"></a>Mise en réseau Azure

Azure fournit un éventail de fonctionnalités de mise en réseau qui peuvent être utilisées ensemble ou séparément. Cliquez sur un de hello suivant toolearn fonctionnalités clés plus à leur sujet :
- [Connectivité entre les ressources Azure](#connectivity): ressources Azure de se connecter dans un réseau virtuel sécurisé et privé dans le cloud de hello.
- [Connectivité Internet](#internet-connectivity): communiquer tooand à partir des ressources Azure sur hello Internet.
- [Connectivité locale](#on-premises-connectivity): se connecter à une ressources tooAzure du réseau local via un réseau privé virtuel (VPN) sur Internet de hello ou via un tooAzure connexion dédiée.
- [Direction de trafic et de l’équilibrage de charge](#load-balancing): charge équilibrer le trafic tooservers dans hello même emplacement et tooservers de diriger le trafic dans des emplacements différents.
- [Sécurité](#security) : filtrez le trafic réseau entre les sous-réseaux ou des machines virtuelles du réseau.
- [Routage](#routing) : utilisez le routage par défaut ou contrôlez entièrement le routage entre vos ressources Azure et locales.
- [Facilité de gestion](#manageability) : analysez et gérez vos ressources réseau Azure.
- [Outils de déploiement et configuration](#tools): utiliser un portail web ou les outils de ligne de commande multiplateforme toodeploy et configurer les ressources réseau.

## <a name="Connectivity"></a>Connectivité entre les ressources Azure

Les ressources Azure, comme les machines virtuelles, les services de cloud computing, les jeux de mise à l’échelle de machines virtuelles et les environnements Azure App Service peuvent communiquer en privé entre elles via un réseau virtuel Azure. Un réseau virtuel est une isolation logique de hello Azure cloud dédié tooyour [abonnement](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fnetworking%2ftoc.json). Vous pouvez implémenter plusieurs réseaux virtuels au sein de chaque abonnement Azure et de chaque [région](https://azure.microsoft.com/regions) Azure. Chaque réseau virtuel est isolé des autres réseaux virtuels. Pour chaque réseau virtuel, vous pouvez :

- Spécifier un espace d’adressage IP privé personnalisé à l’aide d’adresses (RFC 1918) publiques et privées. Azure attribue toohello connecté de ressources réseau virtuel d’une adresse IP privée à partir de l’espace d’adressage hello que vous attribuez.
- Segment hello réseau virtuel dans un ou plusieurs sous-réseaux et allouer une partie du sous-réseau tooeach d’espace d’adresses réseau virtuel de hello.
- Utiliser la résolution de noms fournie par Azure ou spécifier que votre propre serveur DNS pour une utilisation par les ressources connectées tooa réseau virtuel.

toolearn plus sur le service de réseau virtuel Azure hello, lire hello [vue d’ensemble du réseau virtuel](../virtual-network/virtual-networks-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article. Vous pouvez vous connecter à des réseaux virtuels tooeach autres, l’activation de ressources connecté toocommunicate de réseau virtuel tooeither entre eux via des réseaux virtuels. Vous pouvez utiliser ou pour les deux hello suivant tooeach réseaux virtuels tooconnect du options autres :

- **Homologation :** permet aux ressources connecté toodifferent réseaux virtuels Azure dans hello même toocommunicate région Azure entre eux. Hello la bande passante et latence pour hello des réseaux virtuels sont hello identique comme si les ressources hello ont été connecté toohello même réseau virtuel. toolearn en savoir plus sur l’homologation, lire hello [présentation d’homologation du réseau virtuel](../virtual-network/virtual-network-peering-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.
- **Passerelle VPN :** permet aux ressources concernant toodifferent réseaux virtuels Azure dans différentes régions Azure toocommunicate entre eux. Le trafic entre les réseaux virtuels transite par une passerelle VPN Azure. La bande passante entre les réseaux virtuels est la bande passante limitée toohello de passerelle de hello. toolearn plus d’informations sur la connexion de réseaux virtuels avec une passerelle VPN, lire hello [configurer une connexion au réseau entre les régions](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.

## <a name="internet-connectivity"></a>Connectivité Internet

Toutes les ressources Azure de tooa connecté réseau virtuel ont connectivité sortante toohello Internet par défaut. Hello adresse IP privée de ressource de hello est l’adresse IP publique de (SNAT) tooa de traduction d’adresses de réseau source par hello infrastructure Azure. toolearn plus en détail la connectivité Internet sortante, lire hello [présentation des connexions sortantes dans Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.

toocommunicate entrant tooAzure ressources hello Internet ou toocommunicate toohello sortant Internet sans SNAT, une ressource doit être affectée à une adresse IP publique. toolearn plus d’informations sur les adresses IP publiques, lire hello [des adresses IP publiques](../virtual-network/virtual-network-public-ip-address.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.

## <a name="on-premises-connectivity"></a>Connectivité locale

Vous pouvez accéder aux ressources de votre réseau virtuel en toute sécurité via une connexion VPN ou une connexion privée directe. toosend le trafic réseau entre votre réseau virtuel Azure et votre réseau local, vous devez créer une passerelle de réseau virtuel. Configurez les paramètres pour le type de hello toocreate hello passerelle de connexion que vous le souhaitez, le réseau VPN ou ExpressRoute.

Vous pouvez vous connecter votre tooa de réseau local virtuel à l’aide de n’importe quelle combinaison de hello options suivantes :

**Point à site (VPN sur SSTP)**

Hello illustration suivante montre les connexions de distinct point toosite entre plusieurs ordinateurs et un réseau virtuel :

![Point à site](./media/networking-overview/point-to-site.png)

Cette connexion est établie entre un seul ordinateur et un réseau virtuel. Ce type de connexion est idéale si vous débutez avec Azure, ou pour les développeurs, car il requiert peu ou aucune modification tooyour réseau. Cela est également pratique lorsque vous vous connectez à partir d’un emplacement distant, comme lors d’une conférence ou à domicile. Connexions de point à site sont souvent associées à une connexion de site à site via hello même passerelle de réseau virtuel. connexion de Hello utilise communication via tooprovide chiffré le protocole SSTP hello sur hello Internet entre des ordinateurs de hello et hello réseau virtuel. latence Hello pour un réseau de point-to-site VPN est imprévisible, étant donné que le trafic de hello traverse hello Internet.

**Site à site (tunnel VPN IPsec/IKE)**

![De site à site](./media/networking-overview/site-to-site.png)

Cette connexion est établie entre votre appareil VPN local et une passerelle VPN Azure. Ce type de connexion permet de n’importe quelle ressource locale que vous autorisez tooaccess hello réseau virtuel. connexion de Hello est un réseau VPN IPSec/IKE qui fournit une communication chiffrée sur hello Internet entre votre appareil local et une passerelle VPN Azure de hello. Vous pouvez vous connecter à plusieurs toohello de sites locaux même passerelle VPN. Hello local périphérique VPN sur chaque site doit avoir une adresse IP publique externe qui n’est pas derrière un NAT. latence Hello pour une connexion site à site est imprévisible, étant donné que le trafic de hello traverse hello Internet.

**ExpressRoute (connexion privée dédiée)**

![ExpressRoute](./media/networking-overview/expressroute.png)

Ce type de connexion est établi entre votre réseau et Azure via un partenaire ExpressRoute. Cette connexion est privée. Le trafic ne parcourt pas hello Internet. latence Hello pour une connexion ExpressRoute est prévisible, étant donné que le trafic ne traversent hello Internet. Vous pouvez associer ExpressRoute à une connexion de site à site.

toolearn plus d’informations sur tous les hello précédente options de connexion, lisez hello [diagrammes de topologie de connexion](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.

## <a name="load-balancing"></a>Équilibrage de charge et direction de trafic

Microsoft Azure propose plusieurs services destinés à gérer la distribution et l’équilibrage de la charge du trafic réseau. Vous pouvez utiliser une des hello suivant fonctionnalités ensemble ou séparément :

**Équilibrage de la charge du DNS**

Hello service Azure Traffic Manager fournit global DNS l’équilibrage de charge. Traffic Manager répond tooclients avec hello adresse d’un point de terminaison sain, en fonction de hello routage des méthodes suivantes :
- **L’emplacement géographique :** les Clients sont redirigés vers toospecific, points de terminaison (Azure, imbriqué ou externe) basé sur quel emplacement géographique leur requête DNS provient. Cette méthode rend possibles des scénarios où connaître la région géographique d’un client, et le routage en conséquence, est importante. Exemples : respect des obligations en matière de souveraineté des données, localisation de contenu et d’expérience utilisateur, mesure du trafic en provenance de différentes régions.
- **Performances :** adresse hello retourné toohello client est client de toohello hello « le plus proche ». point de terminaison « le plus proche » Hello n’est pas nécessairement le plus proche, mesurée avec la distance géographique. Au lieu de cela, cette méthode détermine le point de terminaison le plus proche hello en mesurant la latence du réseau. Traffic Manager gère un Internet table tootrack hello aller-retour temps de latence entre les plages d’adresses IP et chaque centre de données Azure.
- **Priorité :** le trafic est dirigé toohello le point de terminaison de principal (priorité la plus élevée). Si le point de terminaison principal hello n’est pas disponible, les itinéraires de Traffic Manager hello trafic toohello deuxième point de terminaison. Si les deux points de terminaison principal et secondaire de hello ne sont pas disponibles, le trafic de hello va toohello troisième, et ainsi de suite. Disponibilité du point de terminaison hello est basée sur état hello configuré (activé ou désactivé) et hello du point de terminaison en cours d’analyse.
- **Tourniquet (round-robin) pondéré :** pour chaque requête, Traffic Manager choisit au hasard un point de terminaison disponible. probabilité Hello de choisir un point de terminaison est basée sur le poids hello affectés tooall les points de terminaison disponibles. À l’aide de hello même poids entre tous les points de terminaison entraîne une distribution du trafic même. Sur les points de terminaison spécifiques à l’aide de poids supérieur ou inférieurs provoque ces toobe de points de terminaison renvoyé plus ou moins fréquemment dans les réponses DNS hello.

Hello illustration suivante montre une demande pour un tooa de dirigées vers des applications web point de terminaison de l’application Web. Les points de terminaison peuvent également être d’autres services Azure, tels que des machines virtuelles et services de cloud computing.

![Traffic Manager](./media/networking-overview/traffic-manager.png)

Hello se connecte directement toothat le point de terminaison. Azure Traffic Manager détecte lorsqu’un point de terminaison n’est pas intègre et redirige ensuite le point de terminaison clients tooa différents, sain. toolearn plus sur le Gestionnaire de trafic, lire hello [présentation de Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.

**Équilibrage de charge d’application**

Hello service de passerelle d’Application Azure fournit le contrôleur de remise d’application (ADC) en tant que service. Passerelle d’application offre diverses fonctionnalités de l’équilibrage de charge couche 7 (HTTP/HTTPS) pour vos applications, y compris une application web de pare-feu tooprotect vos applications web à partir des vulnérabilités et des exploits. Passerelle d’application vous permet également productivité de batterie de serveurs web toooptimize en déchargeant la passerelle d’application sollicitant beaucoup le processeur SSL arrêt toohello. 

Autres fonctionnalités de routage de couche 7 incluent distribution alternée de trafic entrant d’affinité de session basée sur un cookie, le routage basé sur le chemin d’accès URL et hello capacité toohost plusieurs sites Web derrière une passerelle d’application unique. Cette dernière peut être configurée en tant que passerelle accessible sur Internet, passerelle interne uniquement ou une combinaison des deux. La passerelle Application Gateway est une solution Azure entièrement gérée, très évolutive et hautement disponible. Elle fournit un ensemble complet de fonctionnalités de diagnostics et de journalisation, pour une meilleure gérabilité. toolearn plus sur la passerelle d’Application, lire hello [vue d’ensemble de la passerelle d’Application](../application-gateway/application-gateway-introduction.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.

Hello image suivante montre URL de routage avec la passerelle d’Application par chemin d’accès :

![Application Gateway](./media/networking-overview/application-gateway.png)

**Équilibrage de charge réseau**

Hello équilibrage de charge Azure fournit à hautes performances et à faible latence couche 4 l’équilibrage de charge pour tous les protocoles UDP et TCP. Il gère les connexions entrantes et sortantes. Vous pouvez configurer des points de terminaison avec équilibrage de charge interne et public. Vous pouvez définir des règles toomap entrant des destinations de pool de connexions tooback-end à l’aide de TCP et HTTP-détection d’intégrité options toomanage disponibilité du service. toolearn plus d’informations sur l’équilibrage de charge, lire hello [vue d’ensemble de l’équilibrage de charge](../load-balancer/load-balancer-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.

Hello illustration suivante montre une application multicouche côté Internet qui utilise les deux programmes d’équilibrage de charge internes et externes :

![Équilibrage de charge](./media/networking-overview/load-balancer.png)

## <a name="security"></a>Sécurité

Vous pouvez filtrer tooand le trafic à partir des ressources Azure à l’aide de hello options suivantes :

- **Réseau :** vous pouvez implémenter toofilter de groupes (NSG) de sécurité réseau Azure entrant et sortant du trafic tooAzure ressources. Chaque groupe de sécurité réseau contient une ou plusieurs règles de trafic entrant et sortant. Chaque règle spécifie les adresses IP de source hello, adresses IP de destination, port et protocole que le trafic est filtré à l’aide. Groupes de sécurité réseau peuvent être appliqué tooindividual sous-réseaux et des ordinateurs virtuels individuels. toolearn plus d’informations sur les groupes de sécurité réseau, lire hello [présentation des groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.
- **Application :** avec une passerelle Application Gateway et le pare-feu d’applications web, vous pouvez protéger vos applications web contre les vulnérabilités et failles. Des exemples courants sont les attaques par injection SQL, les scripts intersites et les en-têtes mal formés. Application Gateway filtre ce trafic et l’empêche d’atteindre vos serveurs web. Vous êtes en mesure de tooconfigure les règles à activer. stratégies de négociation SSL Hello capacité tooconfigure est fourni tooallow certaine stratégies toobe désactivées. toolearn plus d’informations sur les pare-feu d’applications web hello, lire hello [pare-feu d’applications Web](../application-gateway/application-gateway-web-application-firewall-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.

Si vous avez besoin de capacité réseau Azure ne fournir ou souhaitez que les applications de réseau toouse vous utilisez localement, vous pouvez implémenter des produits de hello dans les machines virtuelles et les connecter tooyour réseau virtuel. Hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances) contient plusieurs différentes machines virtuelles préconfigurés avec les applications réseau que vous utilisez actuellement. Ces ordinateurs virtuels préconfigurés sont généralement référencé tooas réseau équipements virtuels (NVA). Les NVA sont disponibles avec des applications comme les pare-feu et l’optimisation du réseau étendu.

## <a name="routing"></a>Routage

Azure crée des tables d’itinéraires qui permettent de sous-réseau connecté tooany de ressources dans n’importe quel toocommunicate de réseau virtuel entre eux par défaut. Vous pouvez implémenter une ou deux hello suivant les types d’itinéraires toooverride hello Azure crée les itinéraires par défaut :
- **Défini par l’utilisateur :** vous pouvez créer des tables d’itinéraires personnalisés avec les itinéraires qui contrôlent où le trafic est routé toofor chaque sous-réseau. toolearn plus d’informations sur les itinéraires définis par l’utilisateur, lecture hello [itinéraires définis par l’utilisateur](../virtual-network/virtual-networks-udr-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.
- **Protocole de passerelle (BGP) de la bordure :** si vous vous connectez à votre réseau local de tooyour de réseau virtuel à l’aide d’une connexion de passerelle VPN à Azure ou ExpressRoute, vous pouvez les propager tooyour des itinéraires BGP des réseaux virtuels. BGP est hello protocole de routage standard couramment utilisé dans hello Internet tooexchange routage et l’accessibilité des informations entre deux ou plusieurs réseaux. Lorsqu’il est utilisé dans le contexte hello des réseaux virtuels Azure, BGP Active hello les passerelles VPN Azure et vos périphériques VPN local, appelé BGP homologues ou voisins, tooexchange « achemine » qui informent les deux passerelles sur la disponibilité de hello et l’accessibilité de ces préfixes toogo via des passerelles de hello ou routeurs impliqués. Protocole BGP peut également activer le routage de transit entre plusieurs réseaux en propageant les itinéraires une passerelle BGP apprend à partir d’un tooall d’homologue BGP autres homologues BGP. toolearn en savoir plus sur BGP, consultez hello [BGP en vue d’ensemble des passerelles de VPN Azure](../vpn-gateway/vpn-gateway-bgp-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.

## <a name="manageability"></a>Facilité de gestion

Azure fournit suivant de hello toomonitor des outils et de gérer la mise en réseau :
- **Journaux d’activité :** ressources Azure toutes les ont des journaux d’activité qui fournissent des informations sur les opérations effectuées placer, l’état des opérations et qui a lancé une opération hello. toolearn plus d’informations sur les journaux d’activité, lire hello [vue d’ensemble des journaux d’activité](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.
- **Journaux de diagnostic :** périodique et événements spontanées sont créés par les ressources du réseau et consignés dans les comptes de stockage Azure, envoyés tooan concentrateur d’événements Azure ou envoyés tooAzure Analytique de journal. Journaux de diagnostic fournissent l’intégrité de toohello un aperçu d’une ressource. Les journaux de diagnostic sont fournis pour l’équilibrage de charge (sur Internet), les groupes de sécurité réseau, les itinéraires et Application Gateway. toolearn plus d’informations sur les journaux de diagnostic, lire hello [vue d’ensemble des journaux de Diagnostic](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.
- **Métriques** : Les métriques sont des mesures et des compteurs de performances collectés sur une période donnée. Métriques peuvent être des alertes de tootrigger utilisés en fonction des seuils. Les métriques sont actuellement disponibles pour Application Gateway. toolearn plus d’informations sur les métriques, lire hello [vue d’ensemble des métriques](../monitoring-and-diagnostics/monitoring-overview-metrics.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.
- **Résolution des problèmes :** des informations de dépannage sont accessible directement dans hello portail Azure. informations de Hello vous aide à diagnostiquer les problèmes courants liés à ExpressRoute, passerelle VPN, passerelle d’Application, les journaux de sécurité réseau, itinéraires, DNS, équilibrage de charge et Traffic Manager.
- **Contrôle d’accès en fonction du rôle (RBAC) :** contrôlez qui peut créer et gérer les ressources réseau avec le contrôle d’accès en fonction du rôle (RBAC). En savoir plus sur RBAC en lisant hello [prise en main RBAC](../active-directory/role-based-access-control-what-is.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article. 
- **Capture de paquets :** hello Observateur de réseau Azure offre de service hello toorun possibilité de capture un paquet sur une machine virtuelle via une extension dans hello machine virtuelle. Cette fonctionnalité est disponible pour les machines virtuelles Linux et Windows. toolearn plus sur la capture des paquets, lire hello [vue d’ensemble de la capture de paquet](../network-watcher/network-watcher-packet-capture-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.
- **Vérifier les flux IP :** Observateur réseau vous permet de tooverify des flux IP entre une machine virtuelle Azure et un toodetermine ressource distante si les paquets sont autorisées ou refusées. Cette fonctionnalité permet aux administrateurs hello tooquickly diagnostiquer les problèmes de connectivité. toolearn en savoir plus sur le flux des tooverify IP, lire hello [les flux IP vérifier la vue d’ensemble](../network-watcher/network-watcher-ip-flow-verify-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.
- **Résoudre les problèmes de connectivité VPN :** hello fonctionnalité de résolution des problèmes VPN de l’Observateur réseau fournit hello tooquery permet une connexion ou la passerelle et vérifier l’intégrité du hello des ressources de hello. toolearn plus d’informations sur la résolution des problèmes de connexions VPN, lire hello [dépannage vue d’ensemble de la connectivité VPN](../network-watcher/network-watcher-troubleshoot-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.
- **Afficher la topologie du réseau :** afficher une représentation graphique des ressources du réseau hello dans un réseau virtuel avec l’Observateur réseau. toolearn plus sur l’affichage de la topologie réseau, lire hello [vue d’ensemble de la topologie](../network-watcher/network-watcher-topology-overview.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.

## <a name="tools"></a>Outils de gestion et de configuration

Vous pouvez déployer et configurer les ressources de mise en réseau Azure hello suite d’outils :

- **Portail Azure :** une interface utilisateur graphique qui s’exécute dans un navigateur. Ouvrez hello [portail Azure](http://portal.azure.com).
- **Azure PowerShell :** des outils de ligne de commande pour la gestion d’Azure à partir d’ordinateurs Windows. En savoir plus sur Azure PowerShell lors de la lecture de hello [vue d’ensemble d’Azure PowerShell](/powershell/azure/overview?view=azurermps-3.8.0?toc=%2fazure%2fnetworking%2ftoc.json) l’article.
- **Interface de ligne de commande Azure (CLI) :** des outils de ligne de commande pour la gestion d’Azure à partir d’ordinateurs Windows, Mac OS ou Linux. En savoir plus sur hello CLI d’Azure par la lecture de hello [vue d’ensemble de l’interface CLI d’Azure](/cli/azure/get-started-with-azure-cli?toc=%2fazure%2fnetworking%2ftoc.json) l’article.
- **Les modèles de gestionnaire de ressources Azure :** un fichier (dans le format JSON) qui définit l’infrastructure de hello et configuration d’une solution Azure. Un modèle vous permet de déployer votre solution à plusieurs reprises tout au long de son cycle de vie pour avoir la garantie que vos ressources présentent un état cohérent lors de leur déploiement. toolearn plus d’informations sur la création de modèles, lire hello [meilleures pratiques pour la création de modèles](../azure-resource-manager/resource-manager-template-best-practices.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article. Modèles peuvent être déployés avec hello portail Azure, CLI, ou PowerShell. tooget démarré avec les modèles immédiatement, déployez l’une des hello nombreux modèles préconfigurés Bonjour [modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/?term=network) bibliothèque. 

## <a name="pricing"></a>Tarification

Certaines de hello Azure services réseau ont un coût, tandis que d’autres sont libres. Hello de vue [réseau virtuel](https://azure.microsoft.com/pricing/details/virtual-network), [passerelle VPN](https://azure.microsoft.com/pricing/details/vpn-gateway), [Application Gateway](https://azure.microsoft.com/en-us/pricing/details/application-gateway/), [équilibrage de charge](https://azure.microsoft.com/pricing/details/load-balancer), [l’Observateur réseau](https://azure.microsoft.com/pricing/details/network-watcher), [DNS](https://azure.microsoft.com/pricing/details/dns), [Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager) et [ExpressRoute](https://azure.microsoft.com/pricing/details/expressroute) pages pour plus d’informations de tarification.

## <a name="next-steps"></a>Étapes suivantes

- Créer votre premier réseau et connecter plusieurs machines virtuelles tooit, en effectuant les étapes hello Bonjour [créer votre premier réseau virtuel](../virtual-network/virtual-network-get-started-vnet-subnet.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.
- Connecter votre réseau virtuel de tooa ordinateur en procédant comme hello Bonjour [configurer une connexion de point-to-site](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.
- Équilibre la charge de serveurs de toopublic le trafic Internet en procédant comme hello Bonjour [créer un équilibrage de charge sur Internet](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fnetworking%2ftoc.json) l’article.
