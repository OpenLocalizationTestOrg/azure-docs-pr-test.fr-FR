## <a name="virtual-network"></a>Réseau virtuel
Les ressources de réseaux virtuels et de sous-réseaux permettent de définir une limite de sécurité pour les charges de travail s’exécutant dans Azure. Un réseau virtuel est caractérisé par une collection d’espaces d’adressage, appelés blocs CIDR. 

> [!NOTE]
> Les administrateurs réseau sont familiarisés avec la notation CIDR. Si vous n’êtes pas familiarisé avec CIDR, [obtenez davantage d’informations](http://whatismyipaddress.com/cidr).
> 
> 

![Réseau virtuel avec plusieurs sous-réseaux](./media/resource-groups-networking/Figure4.png)

Réseaux virtuels contiennent hello propriétés suivantes.

| Propriété | Description | Exemples de valeurs |
| --- | --- | --- |
| **addressSpace** |Collection de préfixes d’adresses qui composent hello réseau virtuel en notation CIDR |192.168.0.0/16 |
| **Sous-réseaux** |Collection des sous-réseaux qui composent hello réseau virtuel |voir [sous-réseaux](#Subnets) ci-dessous. |
| **ipAddress** |Adresse IP affectée tooobject. Il s’agit d’une propriété en lecture seule. |104.42.233.77 |

### <a name="subnets"></a>Sous-réseaux
Un sous-réseau est une ressource enfant d’un réseau virtuel, et permet de définir des segments d’espaces d’adressage dans un bloc CIDR, à l’aide de préfixes d’adresses IP. Cartes réseau peut être ajoutés toosubnets et tooVMs connecté, en offrant une connectivité pour différentes charges de travail.

Sous-réseaux contiennent hello propriétés suivantes. 

| Propriété | Description | Exemples de valeurs |
| --- | --- | --- |
| **addressPrefix** |Préfixe d’adresse unique qui composent le sous-réseau hello dans la notation CIDR |192.168.1.0/24 |
| **networkSecurityGroup** |Groupe de sécurité réseau appliqué toohello sous-réseau |voir [Groupes de sécurité réseau](#Network-Security-Group) |
| **routeTable** |Table d’itinéraires appliqué toohello sous-réseau |voir [itinéraires définis par l’utilisateur](#Route-table) |
| **ipConfigurations** |Collection d’objets de configuration IP utilisés par les cartes réseau connectées toohello sous-réseau |voir [itinéraires définis par l’utilisateur](#Route-table) |

Exemple de réseau virtuel au format JSON :

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a>Ressources supplémentaires
* Obtenez davantage d’informations sur les [réseaux virtuels](../articles/virtual-network/virtual-networks-overview.md).
* Hello de lecture [documentation de référence API REST](https://msdn.microsoft.com/library/azure/mt163650.aspx) pour les réseaux virtuels.
* Hello de lecture [documentation de référence API REST](https://msdn.microsoft.com/library/azure/mt163618.aspx) des sous-réseaux.

