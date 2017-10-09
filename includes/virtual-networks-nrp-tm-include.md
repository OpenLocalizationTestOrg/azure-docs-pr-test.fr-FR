## <a name="traffic-manager-profile"></a>Profil Traffic Manager
Traffic manager et ses ressources de point de terminaison enfant activer tooendpoints de routage DNS dans Azure et en dehors d’Azure. Cette répartition du trafic est régie par des stratégies de routage. Traffic manager permet également de point de terminaison d’intégrité toobe analysée et le trafic détourné de manière appropriée en fonction d’intégrité de hello du point de terminaison. 

| Propriété | Description |
| --- | --- |
| **trafficRoutingMethod** |Les valeurs possibles sont *Performances*, *Pondéré* et *Priorité*. |
| **dnsConfig** |Nom de domaine complet pour le profil de hello |
| **Protocole** |Protocole de surveillance. Les valeurs possibles sont *HTTP* et *HTTPS*. |
| **Port** |Port de surveillance |
| **Chemin d’accès** |Chemin d’accès de surveillance |
| **Points de terminaison** |Conteneur pour les ressources des points de terminaison |

### <a name="endpoint"></a>Point de terminaison
Un point de terminaison est une ressource enfant d'un profil Traffic Manager. Il représente un service ou le trafic des utilisateurs web point de terminaison toowhich est distribué selon la stratégie hello configuré Bonjour ressource du profil Traffic Manager. 

| Propriété | Description |
| --- | --- |
| **Type** |Hello du type de point de terminaison hello, les valeurs possibles sont *point de terminaison d’Azure*, *point de terminaison externe*, et *le point de terminaison imbriqués* |
| **targetResourceId** |Adresse IP publique d’un service ou d’un point de terminaison web. Ce peut être un point de terminaison Azure ou un point de terminaison externe. |
| **Poids** |Poids du point de terminaison utilisé dans la gestion du trafic. |
| **Priorité** |priorité du point de terminaison hello, toodefine utilisé une action de basculement |

Exemple Traffic Manager au format Json : 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a>Ressources supplémentaires
Lisez la [documentation sur l’API REST pour Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) pour plus d’informations.

