## <a name="application-gateway"></a><span data-ttu-id="05c95-101">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="05c95-101">Application Gateway</span></span>
<span data-ttu-id="05c95-102">Application Gateway fournit une solution d'équilibrage de la charge HTTP gérée par Azure et basée sur l'équilibrage de la charge de couche 7.</span><span class="sxs-lookup"><span data-stu-id="05c95-102">Application Gateway provides an Azure-managed HTTP load balancing solution based on layer 7 load balancing.</span></span> <span data-ttu-id="05c95-103">Application de l’équilibrage de charge permet hello de règles de routage pour le trafic de réseau basée sur HTTP.</span><span class="sxs-lookup"><span data-stu-id="05c95-103">Application load balancing allows hello use of routing rules for network traffic based on HTTP.</span></span> 
<BR>

| <span data-ttu-id="05c95-104">Propriété</span><span class="sxs-lookup"><span data-stu-id="05c95-104">Property</span></span> | <span data-ttu-id="05c95-105">Description</span><span class="sxs-lookup"><span data-stu-id="05c95-105">Description</span></span> |
| --- | --- |
| <span data-ttu-id="05c95-106">**backendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="05c95-106">**backendAddressPools**</span></span> |<span data-ttu-id="05c95-107">liste de Hello des adresses IP des serveurs principaux de hello.</span><span class="sxs-lookup"><span data-stu-id="05c95-107">hello list of IP addresses of hello back end servers.</span></span> <span data-ttu-id="05c95-108">adresses IP de Hello répertoriés doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être un IP public/adresse IP virtuelle ou une adresse IP privée</span><span class="sxs-lookup"><span data-stu-id="05c95-108">hello IP addresses listed should either belong toohello virtual network subnet, or should be a public IP/VIP or private IP</span></span> |
| <span data-ttu-id="05c95-109">**backendHttpSettingsCollection**</span><span class="sxs-lookup"><span data-stu-id="05c95-109">**backendHttpSettingsCollection**</span></span> |<span data-ttu-id="05c95-110">Chaque pool a des paramètres comme le port, le protocole et une affinité basée sur les cookies.</span><span class="sxs-lookup"><span data-stu-id="05c95-110">Every pool has settings like port, protocol, and cookie based affinity.</span></span> <span data-ttu-id="05c95-111">Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello</span><span class="sxs-lookup"><span data-stu-id="05c95-111">These settings are tied tooa pool and are applied tooall servers within hello pool</span></span> |
| <span data-ttu-id="05c95-112">**frontendPorts**</span><span class="sxs-lookup"><span data-stu-id="05c95-112">**frontendPorts**</span></span> |<span data-ttu-id="05c95-113">Ce port est le port public de hello ouvert sur la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="05c95-113">This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="05c95-114">Le trafic atteint ce port et obtient redirigés tooone de serveurs principaux de hello</span><span class="sxs-lookup"><span data-stu-id="05c95-114">Traffic hits this port, and then gets redirected tooone of hello back end servers</span></span> |
| <span data-ttu-id="05c95-115">**httpListeners**</span><span class="sxs-lookup"><span data-stu-id="05c95-115">**httpListeners**</span></span> |<span data-ttu-id="05c95-116">Écouteur possède un port de serveur frontal, un protocole (Http ou Https, ils respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL)</span><span class="sxs-lookup"><span data-stu-id="05c95-116">Listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload)</span></span> |
| <span data-ttu-id="05c95-117">**requestRoutingRules**</span><span class="sxs-lookup"><span data-stu-id="05c95-117">**requestRoutingRules**</span></span> |<span data-ttu-id="05c95-118">règle de Hello lie hello écouteur et hello back-end server pool et définit le principal serveur pool hello trafic doit être dirigé.</span><span class="sxs-lookup"><span data-stu-id="05c95-118">hello rule binds hello listener and hello back end server pool and defines which back end server pool hello traffic should be directed.</span></span> <span data-ttu-id="05c95-119">Travaille actuellement uniquement en tant que Round-robin</span><span class="sxs-lookup"><span data-stu-id="05c95-119">Currently works only as Round-robin</span></span> |

<span data-ttu-id="05c95-120">Exemple d'un modèle de passerelle Application Gateway Json :</span><span class="sxs-lookup"><span data-stu-id="05c95-120">Example of an application gateway Json template:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "location": {
          "type": "string",
          "metadata": {
            "description": "Location toodeploy to"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address prefix for hello Virtual Network"
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


### <a name="additional-resources"></a><span data-ttu-id="05c95-121">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="05c95-121">Additional resources</span></span>
<span data-ttu-id="05c95-122">Lisez [ API REST Application Gateway](https://msdn.microsoft.com/library/azure/mt299388.aspx) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="05c95-122">Read [ application gateway REST API](https://msdn.microsoft.com/library/azure/mt299388.aspx) for more information.</span></span>

