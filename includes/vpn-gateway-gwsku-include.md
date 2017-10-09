Lorsque vous créez une passerelle de réseau virtuel, vous avez besoin de passerelle de hello toospecify référence (SKU) que vous souhaitez toouse. Sélectionnez les références (SKU) hello qui répondent à vos besoins selon les types de charges de travail, les débits, fonctionnalités et contrats SLA hello.

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <a name="workloads"></a>Production *par rapport aux* charges de travail de développement et de test

En raison de différences toohello dans les contrats SLA et les ensembles de fonctionnalités, nous vous recommandons de hello suit les références (SKU) pour la production *et* développement et de test :

| **Charge de travail**                       | **Références SKU**               |
| ---                                | ---                    |
| **Production, charges de travail critiques** | VpnGw1, VpnGw2, VpnGw3 |
| **Développement-Test ou preuve de concept**   | De base                  |
|                                    |                        |

Si vous utilisez hello anciennes références (SKU), les recommandations de référence (SKU) de production hello est Standard et les références (SKU) hautes performances. Pour plus d’informations sur hello anciennes références, consultez [passerelle références (SKU hérités)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).

###  <a name="feature"></a>Ensembles de fonctionnalités de référence SKU de passerelle

Hello nouvelle passerelle SKU simplifiée hello ensembles de fonctionnalités proposées sur les passerelles hello :

| **Référence (SKU)**| **Caractéristiques**|
| ---    | ---         |
|**De base**   | **VPN basés sur le routage** : 10 itinéraires avec P2S<br><br>**VPN basés sur les stratégies** : (IKEv1) : 1 itinéraire; aucune P2S|
| **VpnGw1, VpnGw2 et VpnGw3** | **VPN basée sur un itinéraire**: des tunnels too30 (*), P2S, BGP, stratégie IPsec/IKE personnalisée actif / actif, coexistence ExpressRoute/VPN |
|        |             |

(*) Vous pouvez configurer « PolicyBasedTrafficSelectors » tooconnect une basée sur un itinéraire VPN passerelle (VpnGw1, VpnGw2, VpnGw3) toomultiple basée sur des stratégies de pare-feu appareils locaux. Consultez trop[toomultiple des passerelles VPN de se connecter localement basée sur des stratégies de périphériques VPN à l’aide de PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) pour plus d’informations.

###  <a name="resize"></a>Redimensionnement des références SKU de passerelle

1. Vous pouvez effectuer un redimensionnement entre les références SKU VpnGw1, VpnGw2 et VpnGw3.
2. Lorsque vous travaillez avec la passerelle de hello anciennes références (SKU), vous pouvez redimensionner entre Basic, Standard et références (SKU) hautes performances.
2. Vous **ne peut pas** redimensionner à partir de références (SKU) de base/Standard/hautes performances toohello nouvelles références SKU de VpnGw1/VpnGw2/VpnGw3. Au lieu de cela, vous devez [migrer](#migrate) toohello nouvelles références SKU.

###  <a name="migrate"></a>Migration à partir d’anciennes références (SKU) toohello nouvelles références SKU

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
