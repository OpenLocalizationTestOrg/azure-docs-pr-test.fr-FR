## <a name="load-balancer"></a><span data-ttu-id="2ecbb-101">Load Balancer</span><span class="sxs-lookup"><span data-stu-id="2ecbb-101">Load Balancer</span></span>
<span data-ttu-id="2ecbb-102">Un équilibreur de charge est utilisé lorsque vous souhaitez tooscale vos applications.</span><span class="sxs-lookup"><span data-stu-id="2ecbb-102">A load balancer is used when you want tooscale your applications.</span></span> <span data-ttu-id="2ecbb-103">Les scénarios de déploiement classiques impliquent des applications s'exécutant sur plusieurs instances de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2ecbb-103">Typical deployment scenarios involve applications running on multiple VM instances.</span></span> <span data-ttu-id="2ecbb-104">les instances de machine virtuelle Hello sont fronted par un équilibrage de charge qui vous aide à toohello de trafic réseau toodistribute plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="2ecbb-104">hello VM instances are fronted by a load balancer that helps toodistribute network traffic toohello various instances.</span></span> 

![Cartes d'interface réseau sur une seule machine virtuelle](./media/resource-groups-networking/figure8.png)

| <span data-ttu-id="2ecbb-106">Propriété</span><span class="sxs-lookup"><span data-stu-id="2ecbb-106">Property</span></span> | <span data-ttu-id="2ecbb-107">Description</span><span class="sxs-lookup"><span data-stu-id="2ecbb-107">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2ecbb-108">*frontendIPConfigurations*</span><span class="sxs-lookup"><span data-stu-id="2ecbb-108">*frontendIPConfigurations*</span></span> |<span data-ttu-id="2ecbb-109">un équilibrage de charge peut inclure une ou plusieurs adresses IP frontales, également appelées « adresses IP virtuelles ».</span><span class="sxs-lookup"><span data-stu-id="2ecbb-109">a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="2ecbb-110">Ces adresses IP servent d’entrée pour le trafic de hello et peuvent être adresse IP publique ou privée</span><span class="sxs-lookup"><span data-stu-id="2ecbb-110">These IP addresses serve as ingress for hello traffic and can be public IP or private IP</span></span> |
| <span data-ttu-id="2ecbb-111">*backendAddressPools*</span><span class="sxs-lookup"><span data-stu-id="2ecbb-111">*backendAddressPools*</span></span> |<span data-ttu-id="2ecbb-112">Il s’agit des adresses IP associées hello NIC de machine virtuelle toowhich charge est distribuée</span><span class="sxs-lookup"><span data-stu-id="2ecbb-112">these are IP addresses associated with hello VM NICs toowhich load will be distributed</span></span> |
| <span data-ttu-id="2ecbb-113">*loadBalancingRules*</span><span class="sxs-lookup"><span data-stu-id="2ecbb-113">*loadBalancingRules*</span></span> |<span data-ttu-id="2ecbb-114">une propriété de règle mappe une adresse IP donnée frontal et le port jeu tooa de combinaison d’adresses IP de serveur principal et combinaison de port.</span><span class="sxs-lookup"><span data-stu-id="2ecbb-114">a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="2ecbb-115">Avec une seule définition d'une ressource d'équilibrage de charge, vous pouvez définir plusieurs règles d'équilibrage de charge, chaque règle reflétant une combinaison d'une adresse IP et d'un port frontaux d'une part, et d'une adresse IP et d'un port principaux d'autre part, associés à des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2ecbb-115">With a single definition of a load balancer resource, you can define multiple load balancing rules, each rule reflecting a combination of a front end IP and port and back end IP and port associated with virtual machines.</span></span> <span data-ttu-id="2ecbb-116">règle de Hello est un port dans hello frontal pool réduire des machines virtuelles dans le pool de back-end hello</span><span class="sxs-lookup"><span data-stu-id="2ecbb-116">hello rule is one port in hello front end pool toomany virtual machines in hello back end pool</span></span> |
| <span data-ttu-id="2ecbb-117">*Sondes*</span><span class="sxs-lookup"><span data-stu-id="2ecbb-117">*Probes*</span></span> |<span data-ttu-id="2ecbb-118">sondes permettent de suivre tookeep d’intégrité hello des instances de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2ecbb-118">probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="2ecbb-119">Si une sonde d’intégrité échoue, instance de machine virtuelle hello est mis hors rotation automatiquement</span><span class="sxs-lookup"><span data-stu-id="2ecbb-119">If a health probe fails, hello virtual machine instance will be taken out of rotation automatically</span></span> |
| <span data-ttu-id="2ecbb-120">*inboundNatRules*</span><span class="sxs-lookup"><span data-stu-id="2ecbb-120">*inboundNatRules*</span></span> |<span data-ttu-id="2ecbb-121">Les règles NAT définition hello entrant qui traversent hello frontal IP et distributed instance de machine virtuelle spécifique tooa toohello back-end IP.</span><span class="sxs-lookup"><span data-stu-id="2ecbb-121">NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP tooa specific virtual machine instance.</span></span> <span data-ttu-id="2ecbb-122">Règle NAT est un port dans hello frontal pool tooone virtuels dans le pool de back-end hello</span><span class="sxs-lookup"><span data-stu-id="2ecbb-122">NAT rule is one port in hello front end pool tooone virtual machine in hello back end pool</span></span> |

<span data-ttu-id="2ecbb-123">Exemple de modèle d'équilibrage de charge au format Json :</span><span class="sxs-lookup"><span data-stu-id="2ecbb-123">Example of load balancer template in Json format:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "dnsNameforLBIP": {
          "type": "string",
          "metadata": {
            "description": "Unique DNS name"
          }
        },
        "location": {
          "type": "string",
          "allowedValues": [
            "East US",
            "West US",
            "West Europe",
            "East Asia",
            "Southeast Asia"
          ],
          "metadata": {
            "description": "Location toodeploy"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address Prefix"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/24",
          "metadata": {
            "description": "Subnet Prefix"
          }
        },
        "publicIPAddressType": {
          "type": "string",
          "defaultValue": "Dynamic",
          "allowedValues": [
            "Dynamic",
            "Static"
          ],
          "metadata": {
            "description": "Public IP type"
          }
        }
      },
      "variables": {
        "virtualNetworkName": "virtualNetwork1",
        "publicIPAddressName": "publicIp1",
        "subnetName": "subnet1",
        "loadBalancerName": "loadBalancer1",
        "nicName": "networkInterface1",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
        "nicId": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
        "backEndIPConfigID": "[concat(variables('nicId'),'/ipConfigurations/ipconfig1')]"
      },
      "resources": [
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[parameters('location')]",
      "properties": {
        "publicIPAllocationMethod": "[parameters('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsNameforLBIP')]"
        }
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
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
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "subnet": {
                "id": "[variables('subnetRef')]"
              },
              "loadBalancerBackendAddressPools": [
                {
                  "id": "[concat(variables('lbID'), '/backendAddressPools/LoadBalancerBackend')]"
                }
              ],
              "loadBalancerInboundNatRules": [
                {
                  "id": "[concat(variables('lbID'),'/inboundNatRules/RDP')]"
                }
              ]
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[variables('publicIPAddressID')]"
              }
            }
          }
        ],
        "backendAddressPools": [
          {
            "name": "loadBalancerBackEnd"
          }
        ],
        "inboundNatRules": [
          {
            "name": "RDP",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPort": 3389,
              "backendPort": 3389,
              "enableFloatingIP": false
            }
          }
        ]
      }
    }
      ]
    }

### <a name="additional-resources"></a><span data-ttu-id="2ecbb-124">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2ecbb-124">Additional resources</span></span>
<span data-ttu-id="2ecbb-125">Pour plus d’informations, consultez la page [API REST d’équilibrage de charge](https://msdn.microsoft.com/library/azure/mt163651.aspx) .</span><span class="sxs-lookup"><span data-stu-id="2ecbb-125">Read [load balancer REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx) for more information.</span></span>

