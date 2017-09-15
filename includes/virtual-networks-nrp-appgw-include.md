## <a name="application-gateway"></a><span data-ttu-id="6048f-101">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="6048f-101">Application Gateway</span></span>
<span data-ttu-id="6048f-102">Application Gateway fournit une solution d'équilibrage de la charge HTTP gérée par Azure et basée sur l'équilibrage de la charge de couche 7.</span><span class="sxs-lookup"><span data-stu-id="6048f-102">Application Gateway provides an Azure-managed HTTP load balancing solution based on layer 7 load balancing.</span></span> <span data-ttu-id="6048f-103">L'équilibrage de la charge de l'application permet l'utilisation de règles de routage pour le trafic réseau basé sur HTTP.</span><span class="sxs-lookup"><span data-stu-id="6048f-103">Application load balancing allows the use of routing rules for network traffic based on HTTP.</span></span> 
<BR>

| <span data-ttu-id="6048f-104">Propriété</span><span class="sxs-lookup"><span data-stu-id="6048f-104">Property</span></span> | <span data-ttu-id="6048f-105">Description</span><span class="sxs-lookup"><span data-stu-id="6048f-105">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6048f-106">**backendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="6048f-106">**backendAddressPools**</span></span> |<span data-ttu-id="6048f-107">Liste des adresses IP des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="6048f-107">The list of IP addresses of the back end servers.</span></span> <span data-ttu-id="6048f-108">Les adresses IP répertoriées doivent appartenir au sous-réseau de réseau virtuel, sinon elles doivent être une adresse IP/VIP publique ou une adresse IP privée.</span><span class="sxs-lookup"><span data-stu-id="6048f-108">The IP addresses listed should either belong to the virtual network subnet, or should be a public IP/VIP or private IP</span></span> |
| <span data-ttu-id="6048f-109">**backendHttpSettingsCollection**</span><span class="sxs-lookup"><span data-stu-id="6048f-109">**backendHttpSettingsCollection**</span></span> |<span data-ttu-id="6048f-110">Chaque pool a des paramètres comme le port, le protocole et une affinité basée sur les cookies.</span><span class="sxs-lookup"><span data-stu-id="6048f-110">Every pool has settings like port, protocol, and cookie based affinity.</span></span> <span data-ttu-id="6048f-111">Ces paramètres sont liés à un pool et sont appliqués à tous les serveurs du pool.</span><span class="sxs-lookup"><span data-stu-id="6048f-111">These settings are tied to a pool and are applied to all servers within the pool</span></span> |
| <span data-ttu-id="6048f-112">**frontendPorts**</span><span class="sxs-lookup"><span data-stu-id="6048f-112">**frontendPorts**</span></span> |<span data-ttu-id="6048f-113">Ce port est le port public ouvert sur la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="6048f-113">This port is the public port opened on the application gateway.</span></span> <span data-ttu-id="6048f-114">Le trafic atteint ce port, puis il est redirigé vers l’un des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="6048f-114">Traffic hits this port, and then gets redirected to one of the back end servers</span></span> |
| <span data-ttu-id="6048f-115">**httpListeners**</span><span class="sxs-lookup"><span data-stu-id="6048f-115">**httpListeners**</span></span> |<span data-ttu-id="6048f-116">L'écouteur a un port frontal, un protocole (Http ou Https, avec respect de la casse) et le nom du certificat SSL (en cas de configuration du déchargement SSL).</span><span class="sxs-lookup"><span data-stu-id="6048f-116">Listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload)</span></span> |
| <span data-ttu-id="6048f-117">**requestRoutingRules**</span><span class="sxs-lookup"><span data-stu-id="6048f-117">**requestRoutingRules**</span></span> |<span data-ttu-id="6048f-118">La règle lie l’écouteur et le pool de serveurs principaux et définit le pool de serveurs principaux vers lequel le trafic doit être dirigé.</span><span class="sxs-lookup"><span data-stu-id="6048f-118">The rule binds the listener and the back end server pool and defines which back end server pool the traffic should be directed.</span></span> <span data-ttu-id="6048f-119">Travaille actuellement uniquement en tant que Round-robin</span><span class="sxs-lookup"><span data-stu-id="6048f-119">Currently works only as Round-robin</span></span> |

<span data-ttu-id="6048f-120">Exemple d'un modèle de passerelle Application Gateway Json :</span><span class="sxs-lookup"><span data-stu-id="6048f-120">Example of an application gateway Json template:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "location": {
          "type": "string",
          "metadata": {
            "description": "Location to deploy to"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address prefix for the Virtual Network"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/28",
          "metadata": {
            "description": "Subnet prefix"
          }
        },
        "skuName": {
          "type": "string",
          "allowedValues": [
            "Standard_Small",
            "Standard_Medium",
            "Standard_Large"
          ],
          "defaultValue": "Standard_Medium",
          "metadata": {
            "description": "Sku Name"
          }
        },
        "capacity": {
          "type": "int",
          "defaultValue": 2,
          "metadata": {
            "description": "Number of instances"
          }
        },
        "backendIpAddress1": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 1"
          }
        },
        "backendIpAddress2": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 2"
          }
        }
      },
      "variables": {
        "applicationGatewayName": "applicationGateway1",
        "publicIPAddressName": "publicIp1",
        "virtualNetworkName": "virtualNetwork1",
        "subnetName": "appGatewaySubnet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPRef": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "applicationGatewayID": "[resourceId('Microsoft.Network/applicationGateways',variables('applicationGatewayName'))]",
        "apiVersion": "2015-05-01-preview"
      },
      "resources": [
        {
          "apiVersion": "[variables('apiVersion')]",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "[variables('publicIPAddressName')]",
          "location": "[parameters('location')]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic"
          }
        },
        {
          "apiVersion": "[variables('apiVersion')]",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[variables('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[variables('subnetName')]",
                "properties": {
                  "addressPrefix": "[parameters('subnetPrefix')]"
                }
              }
            ]
          }
        },
        {
          "apiVersion": "[variables('apiVersion')]",
          "name": "[variables('applicationGatewayName')]",
          "type": "Microsoft.Network/applicationGateways",
          "location": "[parameters('location')]",
          "dependsOn": [
            "[concat('Microsoft.Network/virtualNetworks/', variables    ('virtualNetworkName'))]",
            "[concat('Microsoft.Network/publicIPAddresses/', variables    ('publicIPAddressName'))]"
          ],
          "properties": {
            "sku": {
              "name": "[parameters('skuName')]",
              "tier": "Standard",
              "capacity": "[parameters('capacity')]"
            },
            "gatewayIPConfigurations": [
              {
                "name": "appGatewayIpConfig",
                "properties": {
                  "subnet": {
                    "id": "[variables('subnetRef')]"
                  }
                }
              }
            ],
            "frontendIPConfigurations": [
              {
                "name": "appGatewayFrontendIP",
                "properties": {
                  "PublicIPAddress": {
                    "id": "[variables('publicIPRef')]"
                  }
                }
              }
            ],
            "frontendPorts": [
              {
                "name": "appGatewayFrontendPort",
                "properties": {
                  "Port": 80
                }
              }
            ],
            "backendAddressPools": [
              {
                "name": "appGatewayBackendPool",
                "properties": {
                  "BackendAddresses": [
                    {
                      "IpAddress": "[parameters('backendIpAddress1')]"
                    },
                    {
                      "IpAddress": "[parameters('backendIpAddress2')]"
                    }
                  ]
                }
              }
            ],
            "backendHttpSettingsCollection": [
              {
                "name": "appGatewayBackendHttpSettings",
                "properties": {
                  "Port": 80,
                  "Protocol": "Http",
                  "CookieBasedAffinity": "Disabled"
                }
              }
            ],
            "httpListeners": [
              {
                "name": "appGatewayHttpListener",
                "properties": {
                  "FrontendIPConfiguration": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendIPConfigurations/appGatewayFrontendIP')]"
                  },
                  "FrontendPort": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendPorts/appGatewayFrontendPort')]"
                  },
                  "Protocol": "Http",
                  "SslCertificate": null
                }
              }
            ],
            "requestRoutingRules": [
              {
                "Name": "rule1",
                "properties": {
                  "RuleType": "Basic",
                  "httpListener": {
                    "id": "[concat(variables('applicationGatewayID'), '/    httpListeners/appGatewayHttpListener')]"
                  },
                  "backendAddressPool": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendAddressPools/appGatewayBackendPool')]"
                  },
                  "backendHttpSettings": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendHttpSettingsCollection/    appGatewayBackendHttpSettings')]"
                  }
                }
              }
            ]
          }
        }
      ]    
    }


### <a name="additional-resources"></a><span data-ttu-id="6048f-121">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6048f-121">Additional resources</span></span>
<span data-ttu-id="6048f-122">Lisez [ API REST Application Gateway](https://msdn.microsoft.com/library/azure/mt299388.aspx) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="6048f-122">Read [ application gateway REST API](https://msdn.microsoft.com/library/azure/mt299388.aspx) for more information.</span></span>

