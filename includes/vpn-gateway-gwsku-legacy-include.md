références (SKU) de la passerelle VPN héritée (ancienne) Hello est :

* De base
* Standard
* HighPerformance

Passerelle VPN n’utilise pas de passerelle de UltraPerformance hello référence (SKU). Pour plus d’informations sur hello UltraPerformance SKU, consultez hello [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentation.

Lorsque vous travaillez avec hello SKU hérités, tenez compte hello qui suit :

* Si vous voulez toouse un type PolicyBased VPN, vous devez utiliser hello base de référence (SKU). Les VPN basés sur une stratégie (précédemment appelés « routage statique ») ne sont pas pris en charge sur une autre SKU.
* BGP n’est pas pris en charge sur l’édition Basic de hello.
* Passerelle VPN de ExpressRoute coexister configurations ne sont pas prises en charge sur hello base de référence (SKU).
* Connexions de passerelle du VPN S2S actif peuvent être configurées sur hello HighPerformance SKU.
