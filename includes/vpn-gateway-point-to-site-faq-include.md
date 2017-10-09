### <a name="what-client-operating-systems-can-i-use-with-point-to-site"></a>Quels systèmes d’exploitation clients puis-je utiliser avec une connexion de point à site ?

Hello suivant des systèmes d’exploitation clients est pris en charge :

* Windows 7 (32 bits et 64 bits)
* Windows Server 2008 R2 (64 bits uniquement)
* Windows 8 (32 bits et 64 bits)
* Windows 8.1 (32 bits et 64 bits)
* Windows Server 2012 (64 bits uniquement)
* Windows Server 2012 R2 (64 bits uniquement)
* Windows 10

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a>Puis-je utiliser un client VPN logiciel pour une connexion point à site qui prend en charge le protocole SSTP ?

Non. Prise en charge est limitée uniquement toohello système d’exploitation versions de Windows répertoriées ci-dessus.

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a>Combien de points de terminaison clients VPN puis-je avoir dans ma configuration point à site ?

Nous prenons en charge des too128 toobe tooconnect en mesure de tooa virtuel réseau de clients VPN à hello même temps.

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a>Puis-je utiliser ma propre AC racine PKI interne pour une connectivité point à site ?

Oui. Auparavant, seuls les certificats racines auto-signés pouvaient être utilisés. Vous pouvez toujours charger 20 certificats racine.

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a>Puis-je parcourir les serveurs proxy et les pare-feu à l’aide de la fonctionnalité point à site ?

Oui. Nous utilisons tootunnel SSTP (Secure Socket Tunneling Protocol) à travers des pare-feu. Ce tunnel apparaît comme une connexion HTTPS.

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-hello-vpn-automatically-reconnect"></a>Si vous redémarrez un ordinateur client configuré pour le Point-to-Site, hello VPN reconnectera automatiquement ?

Par défaut, ordinateur de client hello ne rétablit pas automatiquement de connexion VPN de hello.

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-hello-vpn-clients"></a>Prise en charge de Point-to-Site la reconnexion automatique et DDNS sur hello clients VPN ?

La reconnexion automatique et DDNS ne sont actuellement pas pris en charge dans les configurations VPN point à site.

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-hello-same-virtual-network"></a>Puis-je avoir Site à Site et les configurations de Point-to-Site coexistent hello même réseau virtuel ?

Oui. Ces deux solutions fonctionnent si vous avez un type de réseau VPN basé sur un itinéraire pour votre passerelle. Pour le modèle de déploiement classique de hello, vous avez besoin d’une passerelle dynamique. Nous ne faisons pas prise en charge de Point-to-Site pour les passerelles VPN de routage statiques ou des passerelles à l’aide de hello `-VpnType PolicyBased` applet de commande.

### <a name="can-i-configure-a-point-to-site-client-tooconnect-toomultiple-virtual-networks-at-hello-same-time"></a>Puis-je configurer un réseau virtuel de Point-to-Site client tooconnect toomultiple à hello même temps ?

Oui, vous pouvez. Mais les réseaux virtuels hello ne peut pas avoir de préfixes IP qui se chevauchent et espaces d’adressage hello Point-to-Site ne doivent pas se chevaucher entre les réseaux virtuels hello.

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a>Quel débit puis-je attendre des connexions site à site ou point à site ?

Il est difficile toomaintain le débit exact hello des tunnels VPN de hello. IPsec et SSTP sont des protocoles VPN de chiffrement lourd. Débit est également limité par la latence hello et la bande passante entre votre environnement local et le hello Internet.
