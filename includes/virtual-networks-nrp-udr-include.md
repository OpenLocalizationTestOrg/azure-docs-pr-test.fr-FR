## <a name="route-tables"></a><span data-ttu-id="91a52-101">Tables de routage</span><span class="sxs-lookup"><span data-stu-id="91a52-101">Route tables</span></span>
<span data-ttu-id="91a52-102">Ressources de table de routage contient toodefine itinéraires utilisés comment le trafic est acheminé au sein de votre infrastructure Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="91a52-102">Route table resources contains routes used toodefine how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="91a52-103">Tout le trafic à partir d’un sous-réseau donné tooa appliance virtuelle telles qu’un système de détection des intrusions ou de pare-feu (ID), vous pouvez utiliser toosend d’itinéraires (UDR) défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="91a52-103">You can use user defined routes (UDR) toosend all traffic from a given subnet tooa virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="91a52-104">Vous pouvez associer un toosubnets de table de routage.</span><span class="sxs-lookup"><span data-stu-id="91a52-104">You can associate a route table toosubnets.</span></span> 

<span data-ttu-id="91a52-105">Tables d’itinéraires contiennent hello propriétés suivantes.</span><span class="sxs-lookup"><span data-stu-id="91a52-105">Route tables contain hello following properties.</span></span>

| <span data-ttu-id="91a52-106">Propriété</span><span class="sxs-lookup"><span data-stu-id="91a52-106">Property</span></span> | <span data-ttu-id="91a52-107">Description</span><span class="sxs-lookup"><span data-stu-id="91a52-107">Description</span></span> | <span data-ttu-id="91a52-108">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="91a52-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="91a52-109">**itinéraires**</span><span class="sxs-lookup"><span data-stu-id="91a52-109">**routes**</span></span> |<span data-ttu-id="91a52-110">Collection d’utilisateurs définis itinéraires dans la table d’itinéraires hello</span><span class="sxs-lookup"><span data-stu-id="91a52-110">Collection of user defined routes in hello route table</span></span> |<span data-ttu-id="91a52-111">voir [itinéraires définis par l’utilisateur](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="91a52-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="91a52-112">**Sous-réseaux**</span><span class="sxs-lookup"><span data-stu-id="91a52-112">**subnets**</span></span> |<span data-ttu-id="91a52-113">Collection de table d’itinéraires de sous-réseaux hello est appliquée trop</span><span class="sxs-lookup"><span data-stu-id="91a52-113">Collection of subnets hello route table is applied too</span></span>|<span data-ttu-id="91a52-114">voir [sous-réseaux](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="91a52-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="91a52-115">itinéraires définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="91a52-115">User defined routes</span></span>
<span data-ttu-id="91a52-116">Vous pouvez créer toospecify UDRs où le trafic doit être envoyé, en fonction de son adresse de destination.</span><span class="sxs-lookup"><span data-stu-id="91a52-116">You can create UDRs toospecify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="91a52-117">Vous pouvez considérer un itinéraire en tant que définition de passerelle par défaut hello basée sur l’adresse de destination hello du paquet réseau.</span><span class="sxs-lookup"><span data-stu-id="91a52-117">You can think of a route as hello default gateway definition based on hello destination address of a network packet.</span></span>

<span data-ttu-id="91a52-118">UDRs contenir hello propriétés suivantes.</span><span class="sxs-lookup"><span data-stu-id="91a52-118">UDRs contain hello following properties.</span></span> 

| <span data-ttu-id="91a52-119">Propriété</span><span class="sxs-lookup"><span data-stu-id="91a52-119">Property</span></span> | <span data-ttu-id="91a52-120">Description</span><span class="sxs-lookup"><span data-stu-id="91a52-120">Description</span></span> | <span data-ttu-id="91a52-121">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="91a52-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="91a52-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="91a52-122">**addressPrefix**</span></span> |<span data-ttu-id="91a52-123">Préfixe d’adresse ou une adresse IP complète pour la destination de hello</span><span class="sxs-lookup"><span data-stu-id="91a52-123">Address prefix, or full IP address for hello destination</span></span> |<span data-ttu-id="91a52-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="91a52-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="91a52-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="91a52-125">**nextHopType**</span></span> |<span data-ttu-id="91a52-126">Type de périphérique hello trafic sera envoyé trop</span><span class="sxs-lookup"><span data-stu-id="91a52-126">Type of device hello traffic will be sent too</span></span>|<span data-ttu-id="91a52-127">VirtualAppliance, passerelle VPN, Internet</span><span class="sxs-lookup"><span data-stu-id="91a52-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="91a52-128">**nextHopIpAddress**</span><span class="sxs-lookup"><span data-stu-id="91a52-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="91a52-129">Adresse IP de tronçon suivant de hello</span><span class="sxs-lookup"><span data-stu-id="91a52-129">IP address for hello next hop</span></span> |<span data-ttu-id="91a52-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="91a52-130">192.168.1.4</span></span> |

<span data-ttu-id="91a52-131">Exemple de table de routage au format JSON :</span><span class="sxs-lookup"><span data-stu-id="91a52-131">Sample route table in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="91a52-132">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="91a52-132">Additional resources</span></span>
* <span data-ttu-id="91a52-133">Obtenez davantage d’informations sur les [itinéraires définis par l’utilisateur](../articles/virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="91a52-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="91a52-134">Hello de lecture [documentation de référence API REST](https://msdn.microsoft.com/library/azure/mt502549.aspx) pour les tables d’itinéraires.</span><span class="sxs-lookup"><span data-stu-id="91a52-134">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="91a52-135">Hello de lecture [documentation de référence API REST](https://msdn.microsoft.com/library/azure/mt502539.aspx) pour utilisateur défini itinéraires (UDRs).</span><span class="sxs-lookup"><span data-stu-id="91a52-135">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

