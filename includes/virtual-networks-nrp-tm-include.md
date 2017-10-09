## <a name="traffic-manager-profile"></a><span data-ttu-id="5b78b-101">Profil Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="5b78b-101">Traffic Manager Profile</span></span>
<span data-ttu-id="5b78b-102">Traffic manager et ses ressources de point de terminaison enfant activer tooendpoints de routage DNS dans Azure et en dehors d’Azure.</span><span class="sxs-lookup"><span data-stu-id="5b78b-102">Traffic manager and its child endpoint resource enable DNS routing tooendpoints in Azure and outside of Azure.</span></span> <span data-ttu-id="5b78b-103">Cette répartition du trafic est régie par des stratégies de routage.</span><span class="sxs-lookup"><span data-stu-id="5b78b-103">Such traffic distribution is governed by routing  policy methods.</span></span> <span data-ttu-id="5b78b-104">Traffic manager permet également de point de terminaison d’intégrité toobe analysée et le trafic détourné de manière appropriée en fonction d’intégrité de hello du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="5b78b-104">Traffic manager also allows endpoint health toobe monitored, and traffic diverted appropriately based on hello health of an endpoint.</span></span> 

| <span data-ttu-id="5b78b-105">Propriété</span><span class="sxs-lookup"><span data-stu-id="5b78b-105">Property</span></span> | <span data-ttu-id="5b78b-106">Description</span><span class="sxs-lookup"><span data-stu-id="5b78b-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5b78b-107">**trafficRoutingMethod**</span><span class="sxs-lookup"><span data-stu-id="5b78b-107">**trafficRoutingMethod**</span></span> |<span data-ttu-id="5b78b-108">Les valeurs possibles sont *Performances*, *Pondéré* et *Priorité*.</span><span class="sxs-lookup"><span data-stu-id="5b78b-108">possible values are *Performance*, *Weighted*, and *Priority*</span></span> |
| <span data-ttu-id="5b78b-109">**dnsConfig**</span><span class="sxs-lookup"><span data-stu-id="5b78b-109">**dnsConfig**</span></span> |<span data-ttu-id="5b78b-110">Nom de domaine complet pour le profil de hello</span><span class="sxs-lookup"><span data-stu-id="5b78b-110">FQDN for hello profile</span></span> |
| <span data-ttu-id="5b78b-111">**Protocole**</span><span class="sxs-lookup"><span data-stu-id="5b78b-111">**Protocol**</span></span> |<span data-ttu-id="5b78b-112">Protocole de surveillance. Les valeurs possibles sont *HTTP* et *HTTPS*.</span><span class="sxs-lookup"><span data-stu-id="5b78b-112">monitoring protocol, possible values are *HTTP* and *HTTPS*</span></span> |
| <span data-ttu-id="5b78b-113">**Port**</span><span class="sxs-lookup"><span data-stu-id="5b78b-113">**Port**</span></span> |<span data-ttu-id="5b78b-114">Port de surveillance</span><span class="sxs-lookup"><span data-stu-id="5b78b-114">monitoring port</span></span> |
| <span data-ttu-id="5b78b-115">**Chemin d’accès**</span><span class="sxs-lookup"><span data-stu-id="5b78b-115">**Path**</span></span> |<span data-ttu-id="5b78b-116">Chemin d’accès de surveillance</span><span class="sxs-lookup"><span data-stu-id="5b78b-116">monitoring path</span></span> |
| <span data-ttu-id="5b78b-117">**Points de terminaison**</span><span class="sxs-lookup"><span data-stu-id="5b78b-117">**Endpoints**</span></span> |<span data-ttu-id="5b78b-118">Conteneur pour les ressources des points de terminaison</span><span class="sxs-lookup"><span data-stu-id="5b78b-118">container for endpoint resources</span></span> |

### <a name="endpoint"></a><span data-ttu-id="5b78b-119">Point de terminaison</span><span class="sxs-lookup"><span data-stu-id="5b78b-119">Endpoint</span></span>
<span data-ttu-id="5b78b-120">Un point de terminaison est une ressource enfant d'un profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="5b78b-120">An endpoint is a child resource of a Traffic Manager Profile.</span></span> <span data-ttu-id="5b78b-121">Il représente un service ou le trafic des utilisateurs web point de terminaison toowhich est distribué selon la stratégie hello configuré Bonjour ressource du profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="5b78b-121">It represents a service or web endpoint toowhich user traffic is distributed based on hello configured policy in hello Traffic Manager Profile resource.</span></span> 

| <span data-ttu-id="5b78b-122">Propriété</span><span class="sxs-lookup"><span data-stu-id="5b78b-122">Property</span></span> | <span data-ttu-id="5b78b-123">Description</span><span class="sxs-lookup"><span data-stu-id="5b78b-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5b78b-124">**Type**</span><span class="sxs-lookup"><span data-stu-id="5b78b-124">**Type**</span></span> |<span data-ttu-id="5b78b-125">Hello du type de point de terminaison hello, les valeurs possibles sont *point de terminaison d’Azure*, *point de terminaison externe*, et *le point de terminaison imbriqués*</span><span class="sxs-lookup"><span data-stu-id="5b78b-125">hello type of hello endpoint, possible values are *Azure End point*, *External Endpoint*, and  *Nested Endpoint*</span></span> |
| <span data-ttu-id="5b78b-126">**targetResourceId**</span><span class="sxs-lookup"><span data-stu-id="5b78b-126">**targetResourceId**</span></span> |<span data-ttu-id="5b78b-127">Adresse IP publique d’un service ou d’un point de terminaison web.</span><span class="sxs-lookup"><span data-stu-id="5b78b-127">public IP address of a service or web endpoint.</span></span> <span data-ttu-id="5b78b-128">Ce peut être un point de terminaison Azure ou un point de terminaison externe.</span><span class="sxs-lookup"><span data-stu-id="5b78b-128">This can be an Azure or external endpoint.</span></span> |
| <span data-ttu-id="5b78b-129">**Poids**</span><span class="sxs-lookup"><span data-stu-id="5b78b-129">**Weight**</span></span> |<span data-ttu-id="5b78b-130">Poids du point de terminaison utilisé dans la gestion du trafic.</span><span class="sxs-lookup"><span data-stu-id="5b78b-130">endpoint weight used in traffic management.</span></span> |
| <span data-ttu-id="5b78b-131">**Priorité**</span><span class="sxs-lookup"><span data-stu-id="5b78b-131">**Priority**</span></span> |<span data-ttu-id="5b78b-132">priorité du point de terminaison hello, toodefine utilisé une action de basculement</span><span class="sxs-lookup"><span data-stu-id="5b78b-132">priority of hello endpoint, used toodefine a failover action</span></span> |

<span data-ttu-id="5b78b-133">Exemple Traffic Manager au format Json :</span><span class="sxs-lookup"><span data-stu-id="5b78b-133">Sample of Traffic Manager in Json format:</span></span> 

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


## <a name="additional-resources"></a><span data-ttu-id="5b78b-134">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5b78b-134">Additional resources</span></span>
<span data-ttu-id="5b78b-135">Lisez la [documentation sur l’API REST pour Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="5b78b-135">Read [REST API documentation for Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) for more information.</span></span>

