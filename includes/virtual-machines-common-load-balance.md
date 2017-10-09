

Deux niveaux d’équilibrage de charge sont disponibles pour les services d’infrastructure Azure :

* **Au niveau du DNS**: l’équilibrage de charge pour les services de cloud de trafic toodifferent situé dans les données de différents centres de, toodifferent des sites Web Azure situés dans différents centres de données, ou tooexternal points de terminaison. Cette opération est effectuée avec Azure Traffic Manager et méthode d’équilibrage de charge hello tourniquet (Round Robin).
* **Au niveau du réseau**: charger l’équilibrage des entrant Internet trafic toodifferent virtuels d’un service cloud, ou l’équilibrage du trafic entre les machines virtuelles dans un service cloud ou d’un réseau virtuel. Cela est effectué avec équilibrage de charge Azure hello.

## <a name="traffic-manager-load-balancing-for-cloud-services-and-websites"></a>Équilibrage de charge de Traffic Manager pour des services cloud et des sites Web
Traffic Manager vous permet de répartition hello toocontrol tooendpoints de trafic utilisateur, ce qui peut inclure des services de cloud computing, sites Web, des sites externes et des autres profils Traffic Manager. Traffic Manager fonctionne en appliquant une requêtes (nom DNS) tooDomain du moteur de stratégies intelligent pour les noms de domaine hello de vos ressources Internet. Vos services de cloud computing ou les sites Web peuvent être exécutés dans différents centres de données dans Bonjour.

Vous devez utiliser REST ou Windows PowerShell tooconfigure points de terminaison externes ou des profils Traffic Manager comme points de terminaison.

Traffic Manager utilise trois toodistribute le trafic des méthodes de l’équilibrage de charge :

* **Basculement**: utilisez cette méthode lorsque toouse un point de terminaison principal pour tout le trafic, mais vous fournissez des sauvegardes au cas où hello principal devient indisponible.
* **Performances**: utilisez cette méthode lorsque vous avez des points de terminaison dans différents emplacements géographiques et que vous souhaitez demander les clients toouse hello le plus proche » » point de terminaison en termes de latence la plus faible de hello.
* **Tourniquet (Round Robin) :** utiliser cette méthode lorsque vous souhaitez que la charge toodistribute sur un ensemble de cloud services Bonjour même centre de données ou sur les services de cloud computing ou sites Web situés dans différents centres de données.

Pour plus d’informations, consultez la page [À propos des méthodes d’équilibrage de charge dans Traffic Manager](../articles/traffic-manager/traffic-manager-routing-methods.md).

Hello suivant schéma montre un exemple de méthode d’équilibrage de charge tourniquet (Round Robin) pour distribuer le trafic entre les différents services cloud de hello.

![loadbalancing](./media/virtual-machines-common-load-balance/TMSummary.png)

processus de base Hello est suivant de hello :

1. Un client Internet interroge un service web tooa correspondant de domaine nom.
2. DNS transfère hello nom requête demande tooTraffic Manager.
3. Traffic Manager choisit hello suivant cloud service hello liste de tourniquet (Round Robin) et renvoie un hello nom DNS. serveur DNS du client Hello Internet résout l’adresse IP tooan hello et il envoie au client Internet toohello.
4. le client Internet Hello établit une connexion avec le service cloud hello choisi par le Gestionnaire de trafic.

Pour plus d'informations, consultez la rubrique [Traffic Manager](../articles/traffic-manager/traffic-manager-overview.md).

## <a name="azure-load-balancing-for-virtual-machines"></a>Équilibrage de charge Azure pour des machines virtuelles
Machines virtuelles dans hello même service cloud ou réseau virtuel permettre communiquer entre eux directement à l’aide de leurs adresses IP privées. Ordinateurs et les services en dehors de hello service de cloud computing ou réseau virtuel peut communiquer uniquement avec les machines virtuelles dans un service cloud ou d’un réseau virtuel avec un point de terminaison configuré. Un point de terminaison est un mappage d’une adresse IP publique et une adresse IP privée de port toothat et le port d’un ordinateur virtuel ou un rôle web au sein d’un service cloud Azure.

Hello équilibrage de charge Azure distribue aléatoirement un type spécifique de trafic entrant entre plusieurs machines virtuelles ou services dans une configuration appelée un jeu d’équilibrage de charge. Par exemple, vous pouvez répartir la charge hello du trafic de demande web sur plusieurs serveurs web ou les rôles web.

Hello diagramme suivant illustre un point de terminaison avec équilibrage de charge pour le trafic web (non chiffré) standard qui est partagé entre trois machines virtuelles pour hello public et privé le port TCP 80. Celles-ci sont incluses dans un jeu d’équilibrage de la charge.

![loadbalancing](./media/virtual-machines-common-load-balance/LoadBalancing.png)

Pour plus d’informations, consultez la page [Équilibrage de charge Azure](../articles/load-balancer/load-balancer-overview.md). Les étapes de hello toocreate un jeu d’équilibrage de charge, consultez [configurer un jeu d’équilibrage de charge](../articles/load-balancer/load-balancer-get-started-internet-arm-ps.md).

Azure peut également équilibrer la charge au sein d’un service cloud ou réseau virtuel. Cela est connu comme l’équilibrage de charge interne et peut être utilisé dans hello suivant façons :

* Solde tooload entre les serveurs dans les différents niveaux d’une application à plusieurs niveaux (par exemple, entre les couches web et de la base de données).
* tooload solde line-of-business (LOB) applications hébergées dans Azure sans équilibreur de charge supplémentaires ou de logiciels.
* tooinclude serveurs locaux dans l’ensemble de hello d’ordinateurs dont le trafic est à charge équilibrée.

TooAzure équilibrage de charge similaire, équilibrage de charge interne est facilitée par la configuration d’un jeu d’équilibrage de la charge interne.

Hello suivant schéma montre un exemple du point de terminaison avec équilibrage de charge interne pour une application métier (LOB) qui est partagée entre trois machines virtuelles dans un réseau virtuel intersite.

![loadbalancing](./media/virtual-machines-common-load-balance/LOBServers.png)

## <a name="load-balancer-considerations"></a>Considérations relatives à l’équilibreur de charge
Un équilibreur de charge est configuré par défaut tootimeout une session en 4 minutes d’inactivité. Si votre application derrière un équilibreur de charge quitte une connexion inactive pendant plus de 4 minutes et qu’il n’est pas une configuration Keep-Alive, hello est abandonnée. Vous pouvez modifier tooallow de comportement de programme d’équilibrage de charge hello un [paramètre de délai d’attente plus de temps pour l’équilibrage de charge Azure](../articles/load-balancer/load-balancer-tcp-idle-timeout.md).

Autre considération est de type hello du mode de distribution pris en charge par l’équilibrage de charge Azure. Vous pouvez configurer l’affinité d’IP source (adresse IP source, adresse IP de destination) ou le protocole IP source (adresse IP source, adresse IP de destination et protocole). Pour plus d’informations, consultez l’article [Azure Load Balancer distribution mode (source IP affinity)](../articles/load-balancer/load-balancer-distribution-mode.md) (Mode de distribution de l’équilibreur de charge Azure [affinité d’IP source]).

## <a name="next-steps"></a>Étapes suivantes
Les étapes de hello toocreate un jeu d’équilibrage de charge, consultez [configurer un jeu d’équilibrage de la charge interne](../articles/load-balancer/load-balancer-get-started-ilb-arm-ps.md).

Pour plus d’informations sur l’équilibrage de charge, voir l’article [Équilibrage de charge interne](../articles/load-balancer/load-balancer-internal-overview.md).

