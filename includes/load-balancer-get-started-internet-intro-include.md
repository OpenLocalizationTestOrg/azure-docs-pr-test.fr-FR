Un équilibrage de charge Azure est de type Couche 4 (TCP, UDP). équilibrage de charge Hello offre une haute disponibilité en répartissant le trafic entrant entre les instances de service intègre dans les services de cloud computing ou les machines virtuelles dans un jeu d’équilibrage de charge. Azure Load Balancer peut également présenter ces services sur plusieurs ports, plusieurs adresses IP ou les deux.

Vous pouvez configurer un équilibrage de charge pour :

* Charger le solde entrant Internet trafic toovirtual des machines virtuelles. Nous nous référons tooa équilibrage de charge dans ce scénario comme une [équilibrage de charge connecté à Internet](../articles/load-balancer/load-balancer-internet-overview.md).
* Il équilibre le trafic entre des machines virtuelles dans un réseau virtuel (VNet), entre des machines virtuelles dans les services cloud ou entre des ordinateurs locaux et des machines virtuelles dans un réseau virtuel entre différents locaux. Nous nous référons tooa équilibrage de charge dans ce scénario comme une [équilibreur de charge interne (ILB)](../articles/load-balancer/load-balancer-internal-overview.md).
* Transférer le trafic externe tooa spécifique instance de machine virtuelle.
