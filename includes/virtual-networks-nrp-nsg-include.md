## <a name="network-security-group"></a>Groupe de sécurité réseau
Une ressource de groupe de sécurité réseau permet la création de hello de limite de sécurité pour les charges de travail, en implémentant autoriser et refuser des règles. Ces règles peuvent être appliquées tooa machine virtuelle, une carte réseau ou un sous-réseau.

| Propriété | Description | Exemples de valeurs |
| --- | --- | --- |
| **Sous-réseaux** |Liste des ID de sous-réseau hello NSG est appliquée à. |/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd |
| **securityRules** |Liste des règles de sécurité qui composent hello NSG |Voir [Règle de sécurité](#Security-rule) ci-dessous |
| **defaultSecurityRules** |Liste des règles de sécurité par défaut présentes dans chaque groupe de sécurité réseau |Voir [Règles de sécurité par défaut](#Default-security-rules) ci-dessous |

* **Règle de sécurité** : plusieurs règles de sécurité peuvent être définies pour un groupe de sécurité réseau. Chaque règle peut autoriser ou refuser différents types de trafic.

### <a name="security-rule"></a>Règle de sécurité
Une règle de sécurité est une ressource de l’enfant d’un groupe de sécurité réseau qui contient les propriétés hello ci-dessous.

| Propriété | Description | Exemples de valeurs |
| --- | --- | --- |
| **description** |Description de règle de hello |Autoriser le trafic entrant pour toutes les machines virtuelles dans un sous-réseau X |
| **protocol** |Toomatch de protocole pour la règle de hello |TCP, UDP ou * |
| **sourcePortRange** |Toomatch de plage de port source pour la règle de hello |80, 100-200, * |
| **destinationPortRange** |Toomatch de plage de port de destination pour la règle de hello |80, 100-200, * |
| **sourceAddressPrefix** |Toomatch de préfixe d’adresse source pour la règle de hello |10.10.10.1, 10.10.10.0/24, VirtualNetwork |
| **destinationAddressPrefix** |Toomatch de préfixe d’adresse destination pour la règle de hello |10.10.10.1, 10.10.10.0/24, VirtualNetwork |
| **direction** |Direction de toomatch le trafic pour la règle de hello |entrant ou sortant |
| **priority** |Priorité de la règle de hello. Les règles sont vérifiées dans l'ordre de priorité ; une fois qu'une règle s'applique, plus aucune règle n'est testée pour la correspondance. |10, 100, 65000 |
| **access** |Type d’accès tooapply si hello règle correspond à |autoriser ou refuser |

Exemple de groupe de sécurité réseau au format JSON :

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a>Règles de sécurité par défaut

Règles de sécurité par défaut ont hello mêmes propriétés sont disponibles dans les règles de sécurité. Ils existent tooprovide une connectivité de base entre les ressources qui ont des groupes de sécurité réseau appliquées toothem. Vérifiez les [règles de sécurité par défaut](../articles/virtual-network/virtual-networks-nsg.md#default-rules) existantes.

### <a name="additional-resources"></a>Ressources supplémentaires
* Obtenez davantage d'informations sur les [groupes de sécurité réseau](../articles/virtual-network/virtual-networks-nsg.md).
* Hello de lecture [documentation de référence API REST](https://msdn.microsoft.com/library/azure/mt163615.aspx) pour les groupes de sécurité réseau.
* Hello de lecture [documentation de référence API REST](https://msdn.microsoft.com/library/azure/mt163580.aspx) de règles de sécurité.
