### <a name="is-bgp-supported-on-all-azure-vpn-gateway-skus"></a>Le protocole BGP est-il pris en charge sur toutes les références de passerelle VPN Azure ?
Non. Le protocole BGP est pris en charge sur les passerelles VPN Azure **Standard** et **HighPerformance**. La référence **De base** N’EST PAS prise en charge.

### <a name="can-i-use-bgp-with-azure-policy-based-vpn-gateways"></a>Puis-je utiliser le protocole BGP avec les passerelles VPN Azure basées sur des stratégies ?
Non. Le protocole BGP est pris en charge uniquement sur les passerelles VPN basées sur des itinéraires.

### <a name="can-i-use-private-asns-autonomous-system-numbers"></a>Puis-je utiliser des NSA (numéros de système autonomes) privés ?
Oui, vous pouvez utiliser vos propres NSA publics ou privés pour vos réseaux locaux et les réseaux virtuels Azure.

### <a name="are-there-asns-reserved-by-azure"></a>Existe-t-il des NSA réservés par Azure ?
Oui, hello homologations suivantes sont réservées par Azure pour homologations internes et externes :

* NSA publics : 8075, 8076, 12076
* NSA privés : 65515, 65517, 65518, 65519, 65520

Vous ne pouvez pas spécifier ces homologations pour vos périphériques VPN locaux lors de la connexion des passerelles VPN tooAzure.

### <a name="are-there-any-other-asns-that-i-cant-use"></a>Existe-t-il d’autres NSA que je ne peux pas utiliser ?
Oui, hello suivant homologations est [réservés par l’IANA](http://www.iana.org/assignments/iana-as-numbers-special-registry/iana-as-numbers-special-registry.xhtml) et ne peut pas être configuré sur votre passerelle VPN de Azure :

23456, 64496-64511, 65535-65551 et 429496729.

### <a name="can-i-use-hello-same-asn-for-both-on-premises-vpn-networks-and-azure-vnets"></a>Puis-je utiliser la fonctionnalité hello ASN même pour les deux local réseaux VPN et les réseaux virtuels Azure ?
Non. Vous devez attribuer des NSA différents à vos réseaux locaux et vos réseaux virtuels Azure si vous les interconnectez avec le protocole BGP. Le NSA 65515 est attribué aux passerelles VPN Azure par défaut, et ce, que le protocole BGP soit activé ou non pour la connectivité entre les sites locaux. Vous pouvez substituer ce comportement par défaut en attribuant un autre ASN lors de la création de passerelle VPN de hello ou modifier hello ASN après la création de passerelle de hello. Vous devez tooassign votre toohello d’APE local correspondant Azure les passerelles de réseau Local.

### <a name="what-address-prefixes-will-azure-vpn-gateways-advertise-toome"></a>Quelle adresse de préfixes sera les passerelles VPN Azure publier toome ?
Passerelle VPN Azure sera publié hello suivant itinéraires tooyour local BGP appareils :

* préfixes d’adresse de votre réseau virtuel ;
* Préfixes d’adresse pour chaque passerelle VPN Azure de toohello connecté les passerelles de réseau Local
* Les itinéraires appris à partir d’autres BGP d’homologation sessions connectées toohello passerelle VPN Azure, **, à l’exception de valeur par défaut ou plusieurs itinéraires avec chevauchement avec n’importe quel préfixe réseau virtuel**.

### <a name="can-i-advertise-default-route-00000-tooazure-vpn-gateways"></a>Puis-je publier des passerelles VPN tooAzure itinéraire (0.0.0.0/0) par défaut ?
Oui.

Notez que cela force toutes les le trafic réseau sortant vers votre site local et empêche les machines virtuelles du réseau virtuel hello d’accepter les communications publiques depuis hello Internet directement, ces RDP ou SSH à partir de hello Internet toohello machines virtuelles.

### <a name="can-i-advertise-hello-exact-prefixes-as-my-virtual-network-prefixes"></a>Puis-je publier les préfixes exacte hello en tant que préfixes de mon réseau virtuel ?

Non, hello publicité mêmes préfixes que l’un des préfixes d’adresse de votre réseau virtuel est bloqué ou filtré par hello plateforme Azure. Toutefois, vous pouvez publier un préfixe qui soit un sur-ensemble des éléments de votre réseau virtuel. 

Par exemple, si votre réseau virtuel utilisé hello adresse espace 10.0.0.0/16, 10.0.0.0/8 pourrait rendre publique. Par contre, vous ne pouvez pas publier 10.0.0.0/16 ou 10.0.0.0/24.

### <a name="can-i-use-bgp-with-my-vnet-to-vnet-connections"></a>Puis-je utiliser le protocole BGP avec des connexions entre réseaux virtuels ?
Oui. Vous pouvez utiliser le protocole BGP pour les connexions entre sites locaux et entre réseaux virtuels.

### <a name="can-i-mix-bgp-with-non-bgp-connections-for-my-azure-vpn-gateways"></a>Puis-je combiner des connexions BGP et non-BGP pour mes passerelles VPN Azure ?
Oui, vous pouvez combiner les deux BGP et les connexions non-BGP pour hello même passerelle VPN Azure.

### <a name="does-azure-vpn-gateway-support-bgp-transit-routing"></a>La passerelle VPN Azure prend-elle en charge le routage de transit BGP ?
Oui, le routage de transit BGP est pris en charge, avec l’exception de hello les passerelles VPN Azure seront **pas** publier par défaut achemine tooother BGP homologues. tooenable transit routage à travers plusieurs passerelles VPN Azure, vous devez activer le protocole BGP sur toutes les connexions réseau à intermédiaires.

### <a name="can-i-have-more-than-one-tunnel-between-azure-vpn-gateway-and-my-on-premises-network"></a>Puis-je créer plusieurs tunnels entre ma passerelle VPN Azure et mon réseau local ?
Oui. Vous pouvez établir plusieurs tunnels VPN S2S entre une passerelle VPN Azure et votre réseau local. Veuillez noter que toutes ces tunnels seront comptabilisées sur le nombre total de hello des tunnels de vos passerelles VPN Azure et que vous devez activer le protocole BGP sur les deux tunnels.

Par exemple, si vous avez deux tunnels redondants entre votre passerelle VPN Azure et un de vos réseaux locaux, ils consommeront 2 tunnels hors quota total de hello pour votre passerelle VPN Azure (10 pour Standard) et 30 pour hautes performances.

### <a name="can-i-have-multiple-tunnels-between-two-azure-vnets-with-bgp"></a>Puis-je avoir plusieurs tunnels entre deux réseaux virtuels Azure avec protocole BGP ?
Oui, mais au moins une des passerelles de réseau virtuel hello doit être dans la configuration active-active.

### <a name="can-i-use-bgp-for-s2s-vpn-in-an-expressroutes2s-vpn-co-existence-configuration"></a>Puis-je utiliser BGP pour les passerelles VPN S2S dans une configuration de coexistence entre des passerelles ExpressRoute/S2S ?
Oui. 

### <a name="what-address-does-azure-vpn-gateway-use-for-bgp-peer-ip"></a>Quelle adresse la passerelle VPN Azure utilise-t-elle pour l’IP d’homologue BGP ?
passerelle VPN Azure de Hello alloue une adresse IP unique à partir de hello plage GatewaySubnet défini pour le réseau virtuel de hello. Par défaut, il est hello deuxième dernière adresse de hello plage. Par exemple, si votre GatewaySubnet est 10.12.255.0/27, allant de 10.12.255.0 too10.12.255.31, hello adresse IP d’homologue BGP sur la passerelle VPN Azure hello sera 10.12.255.30. Vous pouvez trouver ces informations lorsque vous répertoriez les informations de la passerelle VPN Azure hello.

### <a name="what-are-hello-requirements-for-hello-bgp-peer-ip-addresses-on-my-vpn-device"></a>Quelles sont les exigences de hello pour les adresses IP d’homologue BGP hello sur mon appareil VPN ?
Votre adresse de l’homologue BGP locale **ne doit pas** être même hello comme hello adresse IP publique de votre périphérique VPN. Utilisez une autre adresse IP sur le périphérique VPN de hello pour votre adresse IP BGP homologues. Il peut être une adresse attribuée interface de bouclage toohello sur l’appareil de hello. Spécifiez cette adresse de hello passerelle de réseau Local représentant hello emplacement correspondante.

### <a name="what-should-i-specify-as-my-address-prefixes-for-hello-local-network-gateway-when-i-use-bgp"></a>Que dois-je spécifier en tant que mon préfixes d’adresse de passerelle de réseau Local de hello lorsque j’utilise le protocole BGP ?
Passerelle de réseau Local Azure spécifie les préfixes d’adresse initiale hello pour le réseau local de hello. Avec protocole BGP, vous devez allouer le préfixe de l’hôte hello (/ 32 préfixe) de votre adresse IP d’homologue BGP en tant qu’espace d’adressage hello pour ce réseau local. Si votre adresse IP BGP homologues est 10.52.255.254, vous devez spécifier « 10.52.255.254/32 « hello localNetworkAddressSpace Hello passerelle de réseau Local qui représente ce réseau local. Il s’agit de tooensure qui hello VPN Azure passerelle établit la session BGP de hello via un tunnel VPN de S2S de hello.

### <a name="what-should-i-add-toomy-on-premises-vpn-device-for-hello-bgp-peering-session"></a>Que dois-je ajouter appareil VPN toomy local pour la session d’homologation BGP de hello ?
Vous devez ajouter un itinéraire de l’hôte de hello adresse IP d’homologue Azure BGP sur votre périphérique VPN qui pointe de tunnel d’IPsec S2S VPN toohello. Par exemple, si hello Azure VPN homologue IP est « 10.12.255.30 », vous devez ajouter un itinéraire d’hôte pour « 10.12.255.30 » avec une interface de saut suivant de l’interface de tunnel IPsec hello correspondant sur votre périphérique VPN.

