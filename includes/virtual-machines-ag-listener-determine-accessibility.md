Il est important toorealize qu’il existe deux façons tooconfigure un écouteur de groupe de disponibilité dans Azure. Hello méthodes diffèrent par type hello d’équilibrage de charge Azure que vous utilisez lorsque vous créez l’écouteur de hello. Hello tableau suivant décrit les différences de hello :

| Type d’équilibrage de charge | Implémentation | Utilisez-la quand : |
| --- | --- | --- |
| **Externe** |Utilise hello *adresse IP virtuelle publique* du service de cloud hello qui héberge des ordinateurs virtuels de hello (VM). |Vous avez besoin d’écouteur de hello tooaccess à partir du réseau virtuel externe hello, y compris de hello Internet. |
| **Interne** |Utilise un *équilibreur de charge interne* avec une adresse privée pour le port d’écoute hello. |Vous pouvez accéder à d’écouteur de hello uniquement à partir de hello même réseau virtuel. Cet accès inclut un réseau privé virtuel de site à site dans des scénarios hybrides. |

> [!IMPORTANT]
> Pour un port d’écoute qu’utilise adresse VIP publique du service de cloud hello (équilibrage de charge externe), tant que hello client, le port d’écoute et bases de données se trouvent dans hello même région Azure, vous ne mobilise pas les frais de sortie. Dans le cas contraire, toutes les données retournées par le biais hello écouteur est considéré comme sortie, et elle est facturée au taux de transfert de données normale. 
> 
> 

Un équilibrage de charge interne ne peut être configuré que dans des réseaux virtuels à portée régionale. Les réseaux virtuels existants qui ont été configurés pour un groupe d’affinités ne peuvent pas utiliser un équilibrage de charge interne. Pour plus d’informations, voir [Présentation de l’équilibrage de charge interne](../articles/load-balancer/load-balancer-internal-overview.md).

