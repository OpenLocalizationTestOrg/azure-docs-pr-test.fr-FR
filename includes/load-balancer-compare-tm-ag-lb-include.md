## <a name="load-balancer-differences"></a>Différences d’équilibrage de charge

Il existe différentes options toodistribute le trafic à l’aide de Microsoft Azure. Ces options fonctionnent différemment, car elles disposent d’un ensemble de fonctionnalités différent et prennent en charge différents scénarios. Elles peuvent être utilisées de manière isolée ou en les combinant.

* **Équilibrage de charge Azure** fonctionne au niveau de la couche de transport hello (couche 4 dans la pile de référence hello OSI réseau). Il fournit une distribution au niveau du réseau du trafic entre les instances d’une application en cours d’exécution dans hello même centre de données Azure.
* **Passerelle d’application** fonctionne au niveau de la couche d’application hello (couche 7 dans la pile de référence hello OSI réseau). Elle agit comme un service de proxy inverse, termine hello client connexion et points de terminaison tooback-fin des demandes de transfert.
* **Traffic Manager** fonctionne au niveau DNS de hello.  Elle s’utilise de DNS, les réponses toodirect par l’utilisateur le trafic tooglobally distribué points de terminaison. Les clients, connecteront les points de terminaison toothose directement.

Hello tableau suivant récapitule les fonctionnalités de hello offertes par chaque service :

| Service | Azure Load Balancer | Application Gateway | Traffic Manager |
| --- | --- | --- | --- |
| Technology |Niveau Transport (couche 4) |Niveau Application (couche 7) |Niveau DNS |
| Protocoles d’applications pris en charge |Quelconque |HTTP, HTTPS et les méthodes de transport WebSockets |N’importe quelle option (un point de terminaison HTTP est requis pour l’analyse du point de terminaison) |
| Points de terminaison |Instances de rôle de services cloud et de machines virtuelles Azure |N’importe quelle adresse IP interne Azure, adresse IP Internet publique, machine virtuelle Azure ou Azure Cloud Service |Machines virtuelles Azure, Cloud Services, Azure Web Apps et points de terminaison externes |
| Prise en charge de réseau virtuel |Peut être utilisé pour les applications internes (réseau virtuel)  et les applications accessibles via Internet |Peut être utilisé pour les applications internes (réseau virtuel)  et les applications accessibles via Internet |Prend uniquement en charge les applications accessibles via Internet |
| Surveillance de point de terminaison |Prise en charge via les sondes |Prise en charge via les sondes |Prise en charge via HTTP/HTTPS GET |

Azure équilibrage de charge et passerelle d’Application itinéraire réseau trafic tooendpoints mais qu’elles ont l’utilisation de différents scénarios toowhich trafic toohandle. Hello tableau suivant permet de différence de hello compréhension entre les programmes d’équilibrage de charge deux hello :

| Type | Azure Load Balancer | Application Gateway |
| --- | --- | --- |
| Protocoles |UDP/TCP |HTTP, HTTPS et les méthodes de transport WebSockets |
| Réservation IP |Pris en charge |Non pris en charge |
| Mode d’équilibrage de charge |5 tuples (IP source, port source, adresse IP de destination, port de destination, type de protocole) |Tourniquet<br>Routage basé sur l’URL |
| Mode d’équilibrage de charge (adresse IP source / sessions rémanentes) |2 tuples (adresse IP source et adresse IP de destination), 3 tuples (adresse IP source, adresse IP de destination et port). Peut augmenter ou diminuer en fonction de nombre hello de machines virtuelles |Affinité basée sur les cookies<br>Routage basé sur l’URL |
| Sondes d’intégrité |Par défaut : intervalle de sondage - 15 secondes. Mise hors service : 2 échecs continus. Prise en charge des sondes définies par l’utilisateur |Intervalle de sondage inactif - 30 secondes. Mise hors service après 5 échecs consécutifs trafic sur le trafic en direct ou un seul échec de sonde en mode inactif. Prise en charge des sondes définies par l’utilisateur |
| Déchargement SSL |Non pris en charge |Pris en charge |
| Routage basé sur des URL | Non pris en charge | Pris en charge|
| Stratégie SSL | Non pris en charge | Pris en charge|
