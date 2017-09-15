## <a name="traffic-manager-profile"></a><span data-ttu-id="db1a9-101">Profil Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="db1a9-101">Traffic Manager Profile</span></span>
<span data-ttu-id="db1a9-102">Traffic Manager et ses ressources de point de terminaison enfant activent le routage DNS vers les points de terminaison dans Azure et en dehors d’Azure.</span><span class="sxs-lookup"><span data-stu-id="db1a9-102">Traffic manager and its child endpoint resource enable DNS routing to endpoints in Azure and outside of Azure.</span></span> <span data-ttu-id="db1a9-103">Cette répartition du trafic est régie par des stratégies de routage.</span><span class="sxs-lookup"><span data-stu-id="db1a9-103">Such traffic distribution is governed by routing  policy methods.</span></span> <span data-ttu-id="db1a9-104">Traffic Manager permet également de surveiller l'intégrité des points de terminaison, ainsi que le trafic dévié de manière appropriée en fonction de l'intégrité d'un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="db1a9-104">Traffic manager also allows endpoint health to be monitored, and traffic diverted appropriately based on the health of an endpoint.</span></span> 

| <span data-ttu-id="db1a9-105">Propriété</span><span class="sxs-lookup"><span data-stu-id="db1a9-105">Property</span></span> | <span data-ttu-id="db1a9-106">Description</span><span class="sxs-lookup"><span data-stu-id="db1a9-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="db1a9-107">**trafficRoutingMethod**</span><span class="sxs-lookup"><span data-stu-id="db1a9-107">**trafficRoutingMethod**</span></span> |<span data-ttu-id="db1a9-108">Les valeurs possibles sont *Performances*, *Pondéré* et *Priorité*.</span><span class="sxs-lookup"><span data-stu-id="db1a9-108">possible values are *Performance*, *Weighted*, and *Priority*</span></span> |
| <span data-ttu-id="db1a9-109">**dnsConfig**</span><span class="sxs-lookup"><span data-stu-id="db1a9-109">**dnsConfig**</span></span> |<span data-ttu-id="db1a9-110">Nom de domaine complet du profil</span><span class="sxs-lookup"><span data-stu-id="db1a9-110">FQDN for the profile</span></span> |
| <span data-ttu-id="db1a9-111">**Protocole**</span><span class="sxs-lookup"><span data-stu-id="db1a9-111">**Protocol**</span></span> |<span data-ttu-id="db1a9-112">Protocole de surveillance. Les valeurs possibles sont *HTTP* et *HTTPS*.</span><span class="sxs-lookup"><span data-stu-id="db1a9-112">monitoring protocol, possible values are *HTTP* and *HTTPS*</span></span> |
| <span data-ttu-id="db1a9-113">**Port**</span><span class="sxs-lookup"><span data-stu-id="db1a9-113">**Port**</span></span> |<span data-ttu-id="db1a9-114">Port de surveillance</span><span class="sxs-lookup"><span data-stu-id="db1a9-114">monitoring port</span></span> |
| <span data-ttu-id="db1a9-115">**Chemin d’accès**</span><span class="sxs-lookup"><span data-stu-id="db1a9-115">**Path**</span></span> |<span data-ttu-id="db1a9-116">Chemin d’accès de surveillance</span><span class="sxs-lookup"><span data-stu-id="db1a9-116">monitoring path</span></span> |
| <span data-ttu-id="db1a9-117">**Points de terminaison**</span><span class="sxs-lookup"><span data-stu-id="db1a9-117">**Endpoints**</span></span> |<span data-ttu-id="db1a9-118">Conteneur pour les ressources des points de terminaison</span><span class="sxs-lookup"><span data-stu-id="db1a9-118">container for endpoint resources</span></span> |

### <a name="endpoint"></a><span data-ttu-id="db1a9-119">Point de terminaison</span><span class="sxs-lookup"><span data-stu-id="db1a9-119">Endpoint</span></span>
<span data-ttu-id="db1a9-120">Un point de terminaison est une ressource enfant d'un profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="db1a9-120">An endpoint is a child resource of a Traffic Manager Profile.</span></span> <span data-ttu-id="db1a9-121">Il représente un service ou un point de terminaison web vers lequel le trafic est réparti en fonction de la stratégie configurée dans la ressource de profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="db1a9-121">It represents a service or web endpoint to which user traffic is distributed based on the configured policy in the Traffic Manager Profile resource.</span></span> 

| <span data-ttu-id="db1a9-122">Propriété</span><span class="sxs-lookup"><span data-stu-id="db1a9-122">Property</span></span> | <span data-ttu-id="db1a9-123">Description</span><span class="sxs-lookup"><span data-stu-id="db1a9-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="db1a9-124">**Type**</span><span class="sxs-lookup"><span data-stu-id="db1a9-124">**Type**</span></span> |<span data-ttu-id="db1a9-125">Type du point de terminaison. Les valeurs possibles sont *Point de terminaison Azure*, *Point de terminaison externe* et *Point de terminaison imbriqué*.</span><span class="sxs-lookup"><span data-stu-id="db1a9-125">the type of the endpoint, possible values are *Azure End point*, *External Endpoint*, and  *Nested Endpoint*</span></span> |
| <span data-ttu-id="db1a9-126">**targetResourceId**</span><span class="sxs-lookup"><span data-stu-id="db1a9-126">**targetResourceId**</span></span> |<span data-ttu-id="db1a9-127">Adresse IP publique d’un service ou d’un point de terminaison web.</span><span class="sxs-lookup"><span data-stu-id="db1a9-127">public IP address of a service or web endpoint.</span></span> <span data-ttu-id="db1a9-128">Ce peut être un point de terminaison Azure ou un point de terminaison externe.</span><span class="sxs-lookup"><span data-stu-id="db1a9-128">This can be an Azure or external endpoint.</span></span> |
| <span data-ttu-id="db1a9-129">**Poids**</span><span class="sxs-lookup"><span data-stu-id="db1a9-129">**Weight**</span></span> |<span data-ttu-id="db1a9-130">Poids du point de terminaison utilisé dans la gestion du trafic.</span><span class="sxs-lookup"><span data-stu-id="db1a9-130">endpoint weight used in traffic management.</span></span> |
| <span data-ttu-id="db1a9-131">**Priorité**</span><span class="sxs-lookup"><span data-stu-id="db1a9-131">**Priority**</span></span> |<span data-ttu-id="db1a9-132">Priorité du point de terminaison, utilisée pour définir une action de basculement.</span><span class="sxs-lookup"><span data-stu-id="db1a9-132">priority of the endpoint, used to define a failover action</span></span> |

<span data-ttu-id="db1a9-133">Exemple Traffic Manager au format Json :</span><span class="sxs-lookup"><span data-stu-id="db1a9-133">Sample of Traffic Manager in Json format:</span></span> 

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


## <a name="additional-resources"></a><span data-ttu-id="db1a9-134">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="db1a9-134">Additional resources</span></span>
<span data-ttu-id="db1a9-135">Lisez la [documentation sur l’API REST pour Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="db1a9-135">Read [REST API documentation for Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) for more information.</span></span>

