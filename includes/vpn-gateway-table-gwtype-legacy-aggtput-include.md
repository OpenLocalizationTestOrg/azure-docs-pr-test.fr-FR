Hello tableau suivant répertorie les types de passerelles hello et débit estimé hello par référence (SKU) de passerelle. Ce tableau s’applique toohello Gestionnaire de ressources et les modèles de déploiement classique. 

La tarification varie en fonction des différentes références de passerelle. Pour plus d’informations, consultez [Passerelle VPN Tarification](https://azure.microsoft.com/pricing/details/vpn-gateway).

Notez la passerelle UltraPerformance hello que référence (SKU) n’est pas représentée dans cette table. Pour plus d’informations sur hello UltraPerformance SKU, consultez hello [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) documentation.

|  | **Débit de passerelle VPN (1)** | **Tunnels IPsec max de passerelle VPN (2)** | **Débit de passerelle ExpressRoute** | **Passerelle VPN et ExpressRoute coexistants** |
| --- | --- | --- | --- | --- |
| **Référence de base (3)(5)(6)** |100 Mbits/s |10 |500 Mbits/s (6) |Non |
| **Référence SKU Standard (4) (5)** |100 Mbits/s |10 |1 000 Mbits/s |Oui |
| **Référence SKU Hautes performances (4)** |200 Mbits/s |30 |2 000 Mbits/s |Oui |


(1) débit VPN hello est une estimation basée sur des mesures de hello entre réseaux virtuels Bonjour même région Azure. Il n’est pas un débit garanti pour les connexions entre différents locaux sur hello Internet. Il s’agit de mesure du débit maximal possible hello.

(2) nombre de hello des tunnels reportez-vous tooRouteBased VPN. Un VPN basé sur des stratégies peut uniquement prendre en charge un seul tunnel VPN de site à site.

(3) BGP n’est pas prise en charge pour l’édition Basic de hello.

(4) Les VPN basés sur des stratégies ne sont pas pris en charge pour cette référence SKU. Elles sont prises en charge pour hello base de référence (SKU).

(5) Les connexions VPN S2S en mode actif-actif avec des passerelles ne sont pas prises en charge pour cette référence SKU. Actif / actif est pris en charge sur hello HighPerformance SKU.

(6) La référence SKU de base est déconseillée pour une utilisation avec Expressroute.
