## <a name="nic"></a>Carte d’interface réseau
Une ressource de carte d’interface réseau fournit un sous-réseau existant tooan connectivité réseau dans une ressource de réseau virtuel. Vous pouvez créer une carte réseau en tant qu’objet autonome, vous devez tooassociate il tooanother objet tooactually fournir la connectivité. Une carte réseau peut être utilisé tooconnect tooa sous-réseau d’ordinateurs virtuels, une adresse IP publique ou un équilibrage de charge.  

| Propriété | Description | Exemples de valeurs |
| --- | --- | --- |
| **virtualMachine** |Hello de machine virtuelle carte réseau est associé. |/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1 |
| **macAddress** |Adresse MAC pour hello NIC |Toute valeur aléatoire comprise entre 4 et 30. |
| **networkSecurityGroup** |Groupe de sécurité réseau associé toohello carte réseau |/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1 |
| **dnsSettings** |Paramètres DNS pour hello NIC |Consultez [Adresse IP publique](#Public-IP-address) |

Une carte d’Interface réseau ou NIC, représente une interface réseau qui peut être associés tooa virtual machine (VM). Une machine virtuelle peut comporter une ou plusieurs cartes d'interface réseau.

![Cartes d'interface réseau sur une seule machine virtuelle](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a>Configurations IP
Cartes réseau disposent d’un objet enfant nommé **ipConfigurations** contenant hello propriétés suivantes :

| Propriété | Description | Exemples de valeurs |
| --- | --- | --- |
| **subnet** |Hello de sous-réseau carte réseau est connectée à. |/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1 |
| **privateIPAddress** |Adresse IP pour hello carte réseau dans un sous-réseau de hello |10.0.0.8 |
| **privateIPAllocationMethod** |Méthode d’allocation des adresses IP |Dynamic ou Static |
| **enableIPForwarding** |Si hello carte réseau peut être utilisé pour le routage |true ou false |
| **primary** |Si hello NIC est hello carte réseau principale pour hello machine virtuelle |true ou false |
| **publicIPAddress** |PIP associé hello NIC |Consultez [Paramètres DNS](#DNS-settings) |
| **loadBalancerBackendAddressPools** |Sauvegarder hello de pools fin adresse que NIC est associé | |
| **loadBalancerInboundNatRules** |Trafic entrant charge hello du règles NAT d’équilibrage de la que carte réseau est associé | |

Exemple d’adresse IP publique au format JSON :

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a>Ressources supplémentaires
* Hello de lecture [documentation de référence API REST](https://msdn.microsoft.com/library/azure/mt163579.aspx) pour les cartes réseau.

