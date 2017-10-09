Azure offre hello suivant SKU de passerelle VPN :

|**Référence (SKU)**   | **S2S/VNet-to-VNet<br>Tunnels** | **P2S<br>Connexions** | **Agrégat<br>Référence de débit** |
|---       | ---                             | ---                    | ---                         |
|**VpnGw1**| Bande passante 30                         | Bande passante 128               | 650 Mbits/s                    |
|**VpnGw2**| Bande passante 30                         | Bande passante 128               | 1 Gbit/s                      |
|**VpnGw3**| Bande passante 30                         | Bande passante 128               | 1,25 Gbits/s                   |
|**De base** | Bande passante 10                         | Bande passante 128               | 100 Mbits/s                    | 
|          |                                 |                        |                             | 

- La référence de débit agrégée est basée sur les mesures de plusieurs tunnels agrégés via une passerelle unique. Il n’est pas un débit garanti en raison des conditions de trafic tooInternet et comportements de votre application.

- Informations de tarification se trouvent sur hello [tarification](https://azure.microsoft.com/pricing/details/vpn-gateway) page.

- Vous trouverez des informations de contrat SLA (Service Level Agreement) sur hello [SLA](https://azure.microsoft.com/support/legal/sla/vpn-gateway/) page.
