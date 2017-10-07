---
title: "Forum aux questions de la passerelle VPN d’aaaAzure | Documents Microsoft"
description: "Hello Forum aux questions de la passerelle VPN. FAQ sur les connexions entre différents locaux de Microsoft Azure Virtual Network, les connexions de configuration hybride et les passerelles VPN."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6ce36765-250e-444b-bfc7-5f9ec7ce0742
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/30/2017
ms.author: cherylmc,yushwang
ms.openlocfilehash: e1737f5832728f513e31f97cc7e752147faaaeb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-faq"></a>FAQ sur la passerelle VPN

## <a name="connecting"></a>Connexion de réseaux toovirtual

### <a name="can-i-connect-virtual-networks-in-different-azure-regions"></a>Puis-je me connecter à des réseaux virtuels dans différentes régions Azure ?

Oui. En fait, il n'existe aucune contrainte de région. Un réseau virtuel peut se connecter tooanother de réseau virtuel Bonjour même région, ou dans une région différente. 

### <a name="can-i-connect-virtual-networks-in-different-subscriptions"></a>Puis-je me connecter à des réseaux virtuels avec différents abonnements ?

Oui.

### <a name="can-i-connect-toomultiple-sites-from-a-single-virtual-network"></a>Puis-je connecter toomultiple sites à partir d’un seul réseau virtuel ?

Vous pouvez vous connecter à des sites de toomultiple à l’aide de Windows PowerShell et hello API REST Azure. Consultez hello [multisite et connectivité de réseau virtuel à réseau virtuel](#V2VMulti) Forum aux questions.

### <a name="what-are-my-cross-premises-connection-options"></a>Quelles sont mes options de connexion entre différents locaux ?

Hello suivant entre différents locaux connexions sont prises en charge :

* Site à site : connexion VPN sur IPsec (IKE v1 et IKE v2). Ce type de connexion requiert un périphérique VPN ou le service RRAS. Pour plus d’informations, consultez [Création d’une connexion de site à site dans le portail Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md).
* Point à site : connexion VPN sur SSTP (Secure Socket Tunneling Protocol). Cette connexion ne nécessite pas un périphérique VPN. Pour plus d’informations, consultez [Configuration d’une connexion point à site à un réseau virtuel à l’aide du portail Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md).
* Au réseau – ce type de connexion est hello identique à une configuration de Site à Site. TooVNet de réseau virtuel est une connexion VPN sur IPsec (IKE v1 et IKE v2). Cette connexion ne nécessite pas un périphérique VPN. Pour plus d’informations, consultez [Configurer une connexion de réseau virtuel à réseau virtuel à l’aide du portail Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).
* Multisite – il s’agit d’une variante d’une configuration de Site à Site qui vous permet de tooconnect plusieurs réseau virtuel local sites tooa. Pour plus d’informations, consultez [Ajouter une connexion de site à site à un réseau virtuel avec une connexion de passerelle VPN existante](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md).
* ExpressRoute – ExpressRoute est un tooAzure connexion directe à partir de votre réseau étendu, pas une connexion VPN sur hello Internet public. Pour plus d’informations, consultez hello [présentation technique d’ExpressRoute](../expressroute/expressroute-introduction.md) et hello [FAQ sur ExpressRoute](../expressroute/expressroute-faqs.md).

Pour plus d’informations sur les connexions à la passerelle VPN, consultez [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).

### <a name="what-is-hello-difference-between-a-site-to-site-connection-and-point-to-site"></a>Qu’est la différence de hello entre une connexion de Site à Site et le Point-to-Site ?

Les configurations **Site à site** (tunnel VPN IPsec/IKE) se trouvent entre votre emplacement local et Azure. Cela signifie que vous pouvez vous connecter à partir de vos ordinateurs situés sur votre ordinateur virtuel de tooany local ou d’une instance de rôle au sein de votre réseau virtuel, selon la façon dont vous choisissez tooconfigure routage et les autorisations. Il s’agit d’une excellente solution pour une connexion entre différents locaux toujours disponibles et elle convient parfaitement aux configurations hybrides. Ce type de connexion s’appuie sur une appliance VPN IPsec (périphérique matériel ou une application logicielle), qui doit être déployée en périphérie hello de votre réseau. toocreate ce type de connexion, doit avoir une adresse IPv4 externe qui n’est pas derrière un NAT.

**Point-to-Site** configurations (VPN sur SSTP) permettent de vous connecter à partir d’un seul ordinateur à partir de n’importe quel endroit tooanything situé dans votre réseau virtuel. Elle utilise le client VPN de hello Windows prédéfini. Dans le cadre de la configuration de Point à Site hello, vous installez un certificat et un package de configuration de client VPN, qui contient les paramètres hello qui permettent à votre ordinateur tooconnect tooany virtual machine ou une instance de rôle au sein du réseau virtuel de hello. Il est très lorsque le réseau virtuel de tooconnect tooa, mais vous ne sont pas locaux. Il est également un bon choix lorsque vous n’avez pas accès tooVPN matériel ou une adresse IPv4 externe, qui sont tous deux requis pour une connexion Site à Site.

Vous pouvez configurer votre toouse de réseau virtuel à la fois Site à Site et Point-to-Site simultanément, à condition que vous créez votre connexion de Site à Site à l’aide d’un VPN de routage pour votre passerelle. Types de VPN basée sur un itinéraire sont appelés des passerelles dynamique dans le modèle de déploiement classique hello.

## <a name="gateways"></a>Passerelles de réseau virtuel

### <a name="is-a-vpn-gateway-a-virtual-network-gateway"></a>Une passerelle VPN est-elle une passerelle de réseau virtuel ?

Une passerelle VPN est un type de passerelle de réseau virtuel. Une passerelle VPN envoie le trafic chiffré entre votre réseau virtuel et votre emplacement local à travers une connexion publique. Vous pouvez également utiliser un trafic de toosend de passerelle VPN entre les réseaux virtuels. Lorsque vous créez une passerelle VPN, vous utilisez valeur - le type de passerelle de hello « Vpn ». Pour plus d’informations, consultez [À propos des paramètres de configuration de la passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md).

### <a name="what-is-a-policy-based-static-routing-gateway"></a>Qu’est-ce qu’une passerelle basée sur une stratégie (routage statique) ?

Les passerelles basées sur des stratégies implémentent des VPN basés sur des stratégies. Les VPN basés sur la stratégie de chiffrement et dirigent les paquets via les tunnels IPsec basées sur les combinaisons de hello de préfixes d’adresses entre votre réseau local et le réseau virtuel Azure de hello. stratégie de Hello (ou un sélecteur de trafic) est généralement définie comme une liste d’accès dans la configuration de VPN hello.

### <a name="what-is-a-route-based-dynamic-routing-gateway"></a>Qu’est-ce qu’une passerelle basée sur l’itinéraire (routage dynamique) ?

Mettre en œuvre des passerelles basées sur l’itinéraire hello VPN basés sur l’itinéraire. Les VPN basés sur l’itinéraire utilisent « itinéraires » dans IP hello transfert ou le routage des paquets toodirect de table dans les interfaces de tunnel leur correspondant. interfaces de tunnel Hello puis chiffrement ou déchiffrement les paquets hello vers et depuis les tunnels hello. Hello sélecteur de stratégie ou le trafic VPN basés sur l’itinéraire sont configurées comme pour tout (ou les caractères génériques).

### <a name="do-i-need-a-gatewaysubnet"></a>Ai-je besoin d’un « sous-réseau de passerelle » ?

Oui. sous-réseau de passerelle Hello contient des adresses IP hello qui utilisent des services de passerelle de réseau virtuel hello. Vous devez toocreate un sous-réseau de passerelle pour votre réseau virtuel dans l’ordre tooconfigure une passerelle de réseau virtuel. Tous les sous-réseaux de passerelle doivent être nommés « GatewaySubnet » toowork correctement. N’attribuez pas un autre nom au sous-réseau de passerelle, Et ne pas déployer des machines virtuelles ou le sous-réseau de passerelle toohello n’importe quel autre.

Lorsque vous créez le sous-réseau de passerelle hello, vous spécifiez hello d’adresses IP qui hello sous-réseau contient. adresses IP de Hello dans le sous-réseau de passerelle hello sont allouées toohello le service de passerelle. Certaines configurations requièrent plus toobe d’adresses IP allouées toohello services de la passerelle que d’effectuer d’autres. Vous souhaitez toomake que votre sous-réseau de passerelle contient suffisamment les adresses IP tooaccommodate une croissance future et supplémentaires nouvelle connexion les configurations possibles. Bien qu’il soit possible de créer un sous-réseau de passerelle aussi petit que /29, nous vous recommandons de créer un sous-réseau de passerelle de taille /27 ou supérieure (/27, /26, /25, etc.). Examinez hello configuration requise pour hello que vous souhaitez toocreate et vérifiez que vous avez le sous-réseau passerelle hello répondra à ces exigences.

### <a name="can-i-deploy-virtual-machines-or-role-instances-toomy-gateway-subnet"></a>Puis-je déployer les ordinateurs virtuels ou le sous-réseau de passerelle toomy rôle instances ?

Non.

### <a name="can-i-get-my-vpn-gateway-ip-address-before-i-create-it"></a>Puis-je obtenir mon adresse IP de passerelle VPN avant de la créer ?

Non. Vous avez toocreate votre adresse IP de passerelle premier tooget hello. Hello changements d’adresses IP si vous supprimez et recréez la passerelle VPN.

### <a name="can-i-request-a-static-public-ip-address-for-my-vpn-gateway"></a>Puis-je demander une adresse IP publique statique pour ma passerelle VPN ?

Non. Seule l’affectation d’adresses IP dynamiques est prise en charge. Toutefois, cela ne signifie pas que l’adresse IP de hello change après que qu’elle a été affectée passerelle VPN de tooyour. Hello seule fois changements d’adresses IP passerelle hello VPN est hello lorsque la passerelle est supprimé et recréé. adresse IP publique la passerelle VPN de Hello ne change pas sur le redimensionnement, la réinitialisation ou autre maintenance/mise à niveau interne de votre passerelle VPN. 

### <a name="how-does-my-vpn-tunnel-get-authenticated"></a>Comment mon tunnel VPN est-il authentifié ?

Azure VPN utilise l'authentification PSK (clé prépartagée). Nous générons une clé prépartagée (PSK) lorsque nous créons le tunnel VPN de hello. Vous pouvez modifier hello généré automatiquement PSK tooyour propre avec l’applet de commande PowerShell de clé pré-partagée définir hello ou l’API REST.

### <a name="can-i-use-hello-set-pre-shared-key-api-tooconfigure-my-policy-based-static-routing-gateway-vpn"></a>Puis-je utiliser hello API de Set Pre-Shared Key tooconfigure mon basée sur des stratégies (routage statique) de passerelle VPN ?

Oui, applet de commande PowerShell et API de Set Pre-Shared Key hello peut être utilisé tooconfigure Azure (statiques) VPN basée sur des stratégies et basée sur un itinéraire VPN de routage (dynamiques).

### <a name="can-i-use-other-authentication-options"></a>Puis-je utiliser les autres options d'authentification ?

Nous sommes limités toousing clés prépartagées (PSK) pour l’authentification.

### <a name="how-do-i-specify-which-traffic-goes-through-hello-vpn-gateway"></a>Comment puis-je indiquer que le trafic traverse la passerelle VPN de hello ?

#### <a name="resource-manager-deployment-model"></a>Modèle de déploiement de Resource Manager

* PowerShell : utilisez le trafic de toospecify « AddressPrefix » pour la passerelle de réseau local hello.
* Portail Azure : accédez passerelle de réseau Local toohello > Configuration > espace d’adressage.

#### <a name="classic-deployment-model"></a>Modèle de déploiement classique

* Portail Azure : accédez toohello de réseau virtuel classique > connexions VPN > connexions VPN de Site à site > nom site Local > site Local > espace d’adressage Client. 
* Portail classique : ajoutez chaque plage que vous voulez envoyer via la passerelle de hello pour votre réseau virtuel sur la page de réseaux hello sous réseaux locaux. 

### <a name="can-i-configure-forced-tunneling"></a>Puis-je configurer un tunneling forcé ?

Oui. Consultez [Configurer un tunneling forcé](vpn-gateway-about-forced-tunneling.md).

### <a name="can-i-set-up-my-own-vpn-server-in-azure-and-use-it-tooconnect-toomy-on-premises-network"></a>Puis-je installer mon propre serveur VPN dans Azure et utiliser le réseau local de toomy tooconnect ?

Oui, vous pouvez déployer votre propre passerelles VPN ou les serveurs dans Azure à partir de hello Azure Marketplace ou créer votre propre routeurs VPN. Vous devez tooconfigure des itinéraires définis par l’utilisateur dans votre réseau virtuel tooensure trafic est acheminé correctement entre vos réseaux locaux et des sous-réseaux de votre réseau virtuel.

### <a name="why-are-certain-ports-opened-on-my-vpn-gateway"></a>Pourquoi certains ports sont-ils ouverts sur ma passerelle VPN ?

Ils sont nécessaires pour la communication avec l’infrastructure Azure. Ils sont protégés (verrouillés) par des certificats Azure. Sans les certificats appropriés, les entités externes, y compris les clients hello de ces passerelles, ne seront pas en mesure de toocause un effet sur ces points de terminaison.

Une passerelle VPN est fondamentalement un périphérique multirésident avec une carte réseau exploite un réseau privé de hello client et une carte réseau tournée hello réseau public. Entités d’infrastructure Azure ne peut pas exploiter des réseaux privés client pour des raisons de conformité, et de disposer de points de terminaison publics tooutilize pour la communication de l’infrastructure. les points de terminaison publics Hello sont analysés régulièrement par l’audit de sécurité Azure.

### <a name="more-information-about-gateway-types-requirements-and-throughput"></a>Plus d'informations sur les types de passerelle, la configuration requise et le débit

Pour plus d’informations, consultez [À propos des paramètres de configuration de la passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md).

## <a name="s2s"></a>Connexions de site à site et périphériques VPN

### <a name="what-should-i-consider-when-selecting-a-vpn-device"></a>Que dois-je prendre en compte lors de la sélection d'un périphérique VPN ?

Nous avons validé un ensemble de périphériques VPN site à site standard en partenariat avec des fournisseurs de périphériques. Vous trouverez une liste de périphériques VPN compatibles, leurs instructions de configuration correspondantes ou des exemples et spécifications des périphériques Bonjour [propos des périphériques VPN](vpn-gateway-about-vpn-devices.md) l’article. Tous les périphériques des familles d’appareils hello répertoriés comme compatible connu doivent fonctionner avec le réseau virtuel. toohelp configurer votre périphérique VPN, consultez l’exemple de configuration de périphérique toohello ou un lien qui correspond la famille de périphériques tooappropriate.

### <a name="where-can-i-find-vpn-device-configuration-settings"></a>Où puis-je trouver les paramètres de configuration des périphériques VPN ?

[!INCLUDE [vpn devices](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="how-do-i-edit-vpn-device-configuration-samples"></a>Comment dois-je modifier les exemples de configuration de périphérique VPN ?

Pour plus d’informations sur la modification des exemples de configuration des périphériques, consultez la page [Modifier les exemples](vpn-gateway-about-vpn-devices.md#editing).

### <a name="where-do-i-find-ipsec-and-ike-parameters"></a>Où puis-je trouver les paramètres IPsec et IKE ?

En ce qui concerne les paramètres IPsec/IKE, consultez la page [Paramètres](vpn-gateway-about-vpn-devices.md#ipsec).

### <a name="why-does-my-policy-based-vpn-tunnel-go-down-when-traffic-is-idle"></a>Pourquoi mon tunnel VPN basé sur une stratégie tombe-t-il en panne lorsque le trafic est inactif ?

Il s’agit du comportement attendu pour les passerelles VPN basées sur une stratégie (également appelé routage statique). Lorsque le trafic de hello via le tunnel de hello est inactif pendant plus de 5 minutes, tunnel de hello sera détruit. Lorsque le trafic recommence à circuler dans les deux sens, tunnel de hello sera rétablie immédiatement.

### <a name="can-i-use-software-vpns-tooconnect-tooazure"></a>Puis-je utiliser les logiciels VPN tooconnect tooAzure ?

Nous prenons en charge les serveurs de routage et d’accès distant (RRAS) Windows Server 2012 pour la configuration site à site entre différents locaux.

Autres solutions VPN logicielles doivent fonctionner avec notre passerelle tant qu’elles sont conformes tooindustry les implémentations IPsec standard. Contactez le fournisseur hello du logiciel de hello pour obtenir des instructions de configuration et de prise en charge.

## <a name="P2S"></a>Connexions de point à site

[!INCLUDE [vpn-gateway-point-to-site-faq-include](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="V2VMulti"></a>Connexions multi-sites et réseau virtuel à réseau virtuel

[!INCLUDE [vpn-gateway-vnet-vnet-faq-include](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

### <a name="can-i-use-azure-vpn-gateway-tootransit-traffic-between-my-on-premises-sites-or-tooanother-virtual-network"></a>Puis-je utiliser le trafic tootransit de passerelle VPN Azure entre mes sites locaux ou d’un réseau virtuel de tooanother ?

**Modèle de déploiement de Resource Manager**<br>
Oui. Consultez hello [BGP](#bgp) section pour plus d’informations.

**Modèle de déploiement classique**<br>
Faire transiter le trafic via la passerelle VPN Azure est possible à l’aide du modèle de déploiement classique de hello, mais s’appuie sur les espaces d’adressage définis statiquement dans le fichier de configuration de réseau hello. BGP n’est pas encore pris en charge avec les passerelles VPN et les réseaux virtuels Azure à l’aide du modèle de déploiement classique hello. Sans BGP, la définition manuelle des espaces d’adressage de transit peut entraîner des erreurs et n’est pas recommandée.

### <a name="does-azure-generate-hello-same-ipsecike-pre-shared-key-for-all-my-vpn-connections-for-hello-same-virtual-network"></a>Azure génère-t-il hello même IPsec/IKE prépartagée de clé pour toutes les connexions de mon VPN pour hello même réseau virtuel ?

Non, Azure génère par défaut différentes clés prépartagées pour différentes connexions VPN. Toutefois, vous pouvez utiliser hello API de REST Set VPN Gateway Key ou PowerShell applet de commande tooset hello valeur de clé de que votre choix. clé de Hello doit être une chaîne alphanumérique d’une longueur comprise entre 1 too128 caractères.

### <a name="do-i-get-more-bandwidth-with-more-site-to-site-vpns-than-for-a-single-virtual-network"></a>Puis-je obtenir plus de bande passante avec un plus grand nombre de réseaux VPN site à site que si j’utilise un seul réseau virtuel ?

Non, tous les tunnels VPN, y compris les Point-to-Site VPN, partagent hello même VPN Azure passerelle et hello la bande passante disponible.

### <a name="can-i-configure-multiple-tunnels-between-my-virtual-network-and-my-on-premises-site-using-multi-site-vpn"></a>Puis-je configurer plusieurs tunnels entre mon réseau virtuel et mon site local à l'aide d’un VPN multisite ?

Oui, mais vous devez configurer BGP sur les deux toohello tunnels même emplacement.

### <a name="can-i-use-point-to-site-vpns-with-my-virtual-network-with-multiple-vpn-tunnels"></a>Puis-je utiliser des réseaux VPN point à site avec mon réseau virtuel comportant plusieurs tunnels VPN ?

Oui, VPN Point à Site (P2S) peut être utilisé avec les passerelles VPN hello connexion toomultiple des sites locaux et autres réseaux virtuels.

### <a name="can-i-connect-a-virtual-network-with-ipsec-vpns-toomy-expressroute-circuit"></a>Puis-je connecter un réseau virtuel avec des VPN IPsec toomy circuit ExpressRoute ?

Oui, cette méthode est prise en charge. Pour plus d’informations, consultez [Configurer des connexions ExpressRoute et VPN de site à site pour qu’elles coexistent pour un réseau virtuel](../expressroute/expressroute-howto-coexist-classic.md).

## <a name="ipsecike"></a>Stratégie IPsec/IKE

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="bgp"></a>BGP

[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="vms"></a>Connectivité entre locaux et machines virtuelles

### <a name="if-my-virtual-machine-is-in-a-virtual-network-and-i-have-a-cross-premises-connection-how-should-i-connect-toohello-vm"></a>Si mon ordinateur virtuel est dans un réseau virtuel et que j’ai une connexion intersite, comment dois-je connecter toohello machine virtuelle ?

Vous disposez de plusieurs options. Si vous avez activé pour votre machine virtuelle le protocole RDP, vous pouvez vous connecter à tooyour virtual machine en utilisant l’adresse IP privée de hello. Dans ce cas, vous devez spécifier les adresses IP privées hello et port hello que vous souhaitez tooconnect trop (généralement 3389). Vous avez besoin du port de hello tooconfigure sur votre machine virtuelle pour le trafic de hello.

Vous pouvez également connecter tooyour virtuels par adresse IP privée à partir d’un autre ordinateur virtuel qui est située sur hello même réseau virtuel. Vous ne pouvez pas la machine virtuelle de tooyour RDP en utilisant l’adresse IP privée de hello si vous vous connectez à partir d’un emplacement en dehors de votre réseau virtuel. Par exemple, si vous avez un réseau virtuel Point-to-Site configuré et que vous n’établissez une connexion à partir de votre ordinateur, vous ne peut pas se connecter à toohello virtual machine par adresse IP privée.

### <a name="if-my-virtual-machine-is-in-a-virtual-network-with-cross-premises-connectivity-does-all-hello-traffic-from-my-vm-go-through-that-connection"></a>Si mon ordinateur virtuel est dans un réseau virtuel avec connectivité intersite, tout le trafic de hello de ma machine virtuelle passe via cette connexion ?

Non. Uniquement le trafic hello qui possède une destination IP qui figure dans les plages d’adresses hello réseau virtuel IP de réseau Local que vous avez spécifiée passera via la passerelle de réseau virtuel hello. Trafic présente une destination IP qui se trouve dans le réseau virtuel de hello reste dans le réseau virtuel de hello. Tout autre trafic est envoyé via des réseaux publics hello charge équilibrage toohello ou si le tunneling forcé est utilisé, envoyé via la passerelle VPN Azure de hello.

### <a name="how-do-i-troubleshoot-an-rdp-connection-tooa-vm"></a>Comment résoudre les un tooa de connexion RDP machine virtuelle

[!INCLUDE [Troubleshoot VM connection](../../includes/vpn-gateway-connect-vm-troubleshoot-include.md)]


## <a name="faq"></a>Forum aux questions sur le réseau virtuel

Vous affichez les informations de réseau virtuel supplémentaire dans hello [FAQ sur le réseau virtuel](../virtual-network/virtual-networks-faq.md).

## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur la passerelle VPN, consultez [À propos de la passerelle VPN](vpn-gateway-about-vpngateways.md).
* Pour plus d’informations sur les paramètres de configuration de la passerelle VPN, consultez [À propos des paramètres de configuration de la passerelle VPN](vpn-gateway-about-vpn-gateway-settings.md).
