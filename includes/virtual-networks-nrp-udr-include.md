## <a name="route-tables"></a>Tables de routage
Ressources de table de routage contient toodefine itinéraires utilisés comment le trafic est acheminé au sein de votre infrastructure Windows Azure. Tout le trafic à partir d’un sous-réseau donné tooa appliance virtuelle telles qu’un système de détection des intrusions ou de pare-feu (ID), vous pouvez utiliser toosend d’itinéraires (UDR) défini par l’utilisateur. Vous pouvez associer un toosubnets de table de routage. 

Tables d’itinéraires contiennent hello propriétés suivantes.

| Propriété | Description | Exemples de valeurs |
| --- | --- | --- |
| **itinéraires** |Collection d’utilisateurs définis itinéraires dans la table d’itinéraires hello |voir [itinéraires définis par l’utilisateur](#User-defined-routes) |
| **Sous-réseaux** |Collection de table d’itinéraires de sous-réseaux hello est appliquée trop|voir [sous-réseaux](#Subnets) |

### <a name="user-defined-routes"></a>itinéraires définis par l’utilisateur
Vous pouvez créer toospecify UDRs où le trafic doit être envoyé, en fonction de son adresse de destination. Vous pouvez considérer un itinéraire en tant que définition de passerelle par défaut hello basée sur l’adresse de destination hello du paquet réseau.

UDRs contenir hello propriétés suivantes. 

| Propriété | Description | Exemples de valeurs |
| --- | --- | --- |
| **addressPrefix** |Préfixe d’adresse ou une adresse IP complète pour la destination de hello |192.168.1.0/24, 192.168.1.101 |
| **nextHopType** |Type de périphérique hello trafic sera envoyé trop|VirtualAppliance, passerelle VPN, Internet |
| **nextHopIpAddress** |Adresse IP de tronçon suivant de hello |192.168.1.4 |

Exemple de table de routage au format JSON :

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a>Ressources supplémentaires
* Obtenez davantage d’informations sur les [itinéraires définis par l’utilisateur](../articles/virtual-network/virtual-networks-udr-overview.md).
* Hello de lecture [documentation de référence API REST](https://msdn.microsoft.com/library/azure/mt502549.aspx) pour les tables d’itinéraires.
* Hello de lecture [documentation de référence API REST](https://msdn.microsoft.com/library/azure/mt502539.aspx) pour utilisateur défini itinéraires (UDRs).

