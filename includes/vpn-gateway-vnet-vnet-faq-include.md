Hello FAQ sur le réseau à applique des connexions de la passerelle tooVPN. Si vous recherchez des informations sur l’homologation de réseaux virtuels, voir [Homologation de réseaux virtuels](../articles/virtual-network/virtual-network-peering-overview.md).

### <a name="does-azure-charge-for-traffic-between-vnets"></a>Le trafic entre réseaux virtuels est-il facturé par Azure ?

Réseau pour le trafic au sein de hello même région est gratuite pour les deux sens lors de l’utilisation d’une connexion de passerelle VPN. Cross-sortie de réseau pour la région, le trafic est facturé avec un taux de transfert données sortantes entre réseaux virtuels-réseau virtuel hello selon les régions de code source hello. Consultez toohello [passerelle VPN page de tarification](https://azure.microsoft.com/pricing/details/vpn-gateway/) pour plus d’informations. Si vous vous connectez vos réseaux virtuels à l’aide du réseau virtuel d’homologation, plutôt que passerelle VPN, consultez hello [page de tarification de réseau virtuel](https://azure.microsoft.com/pricing/details/virtual-network/).

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a>Le trafic de réseau virtuel à réseau virtuel circulent entre hello Internet ?

Non. Réseau pour trafic transite sur hello backbone Microsoft Azure, pas hello Internet.

### <a name="is-vnet-to-vnet-traffic-secure"></a>Le trafic de réseau virtuel à réseau virtuel est-il sécurisé ?

Oui, il est protégé par le chiffrement IPsec/IKE.

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a>Ai-je besoin une tooconnect de périphérique VPN réseaux virtuels ensemble ?

Non. L’interconnexion de plusieurs réseaux virtuels Azure ne requiert pas de périphérique VPN, sauf si une connectivité intersite est nécessaire.

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a>Mes réseaux virtuels doivent-elles toobe Bonjour même région ?

Non. les réseaux virtuels Hello peuvent être Bonjour identiques ou différentes régions (emplacements) Azure.

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a>Si hello réseaux virtuels n’est pas dans hello même abonnement, les abonnements hello doivent-elles toobe associé hello AD même client ?

Non.

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a>Puis-je utiliser une connexion de réseau virtuel à réseau virtuel en plus de connexions multisites ?

Oui. Une connectivité réseau virtuelle peut être utilisée en même temps que des VPN multisites.

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a>À combien de sites locaux et de réseaux virtuels peut se connecter un réseau virtuel ?

Consultez le tableau [Conditions requises de la passerelle](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements).

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a>Puis-je utiliser tooconnect de réseau de machines virtuelles ou services en dehors d’un réseau virtuel cloud ?

Non. La connexion de réseau virtuel à réseau virtuel prend en charge la connexion de réseaux virtuels. Elle ne prend pas en charge la connexion de machines virtuelles ou de services cloud qui ne se trouvent pas dans un réseau virtuel.

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a>Un service cloud ou un point de terminaison d’équilibrage de charge peut-il s’étendre sur différents réseaux virtuels ?

Non. Un service cloud ou un point de terminaison d’équilibrage de charge ne peut pas s’étendre sur différents réseaux virtuels, même si ces derniers sont interconnectés.

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a>Puis-je utiliser un type de réseau VPN basé sur des stratégies pour les connexions de réseau virtuel à réseau virtuel ou multisites ?

Non. Les connexions de réseau virtuel à réseau virtuel et multisites nécessitent des passerelles VPN Azure avec des types de VPN basés sur des itinéraires (dits auparavant de routage dynamique).

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a>Puis-je connecter un réseau virtuel avec un Type de VPN RouteBased de tooanother réseau virtuel avec un type PolicyBased VPN ?

Non, les deux réseaux virtuels DOIVENT utiliser des réseaux VPN basés sur des itinéraires (dits auparavant de routage dynamique).

### <a name="do-vpn-tunnels-share-bandwidth"></a>Les tunnels VPN se partagent-ils la bande passante ?

Oui. Tous les tunnels VPN de réseau virtuel de hello partagent la bande passante disponible de hello sur la passerelle VPN Azure hello et hello même SLA de disponibilité de la passerelle VPN dans Azure.

### <a name="are-redundant-tunnels-supported"></a>Les tunnels redondants sont pris en charge ?

Les tunnels redondants entre deux réseaux virtuels sont pris en charge lorsqu’une passerelle de réseau virtuel est configurée comme active/active.

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a>Des espaces d’adressage peuvent-ils se chevaucher pour les configurations de réseau virtuel à réseau virtuel ?

Non. Il ne peut pas y avoir de chevauchement entre des plages d’adresses IP.

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a>Des espaces d’adressage peuvent-ils se chevaucher entre les réseaux virtuels connectés et les sites locaux ?

Non. Il ne peut pas y avoir de chevauchement entre des plages d’adresses IP.



