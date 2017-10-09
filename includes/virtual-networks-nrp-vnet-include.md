## <a name="virtual-network"></a><span data-ttu-id="1a9cb-101">Réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="1a9cb-101">Virtual Network</span></span>
<span data-ttu-id="1a9cb-102">Les ressources de réseaux virtuels et de sous-réseaux permettent de définir une limite de sécurité pour les charges de travail s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-102">Virtual Networks (VNET) and subnets resources help define a security boundary for workloads running in Azure.</span></span> <span data-ttu-id="1a9cb-103">Un réseau virtuel est caractérisé par une collection d’espaces d’adressage, appelés blocs CIDR.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-103">A VNet is characterized by a collection of address spaces, defined as CIDR blocks.</span></span> 

> [!NOTE]
> <span data-ttu-id="1a9cb-104">Les administrateurs réseau sont familiarisés avec la notation CIDR.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-104">Network administrators are familiar with CIDR notation.</span></span> <span data-ttu-id="1a9cb-105">Si vous n’êtes pas familiarisé avec CIDR, [obtenez davantage d’informations](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="1a9cb-105">If you are not familiar with CIDR, [learn more about it](http://whatismyipaddress.com/cidr).</span></span>
> 
> 

![Réseau virtuel avec plusieurs sous-réseaux](./media/resource-groups-networking/Figure4.png)

<span data-ttu-id="1a9cb-107">Réseaux virtuels contiennent hello propriétés suivantes.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-107">VNets contain hello following properties.</span></span>

| <span data-ttu-id="1a9cb-108">Propriété</span><span class="sxs-lookup"><span data-stu-id="1a9cb-108">Property</span></span> | <span data-ttu-id="1a9cb-109">Description</span><span class="sxs-lookup"><span data-stu-id="1a9cb-109">Description</span></span> | <span data-ttu-id="1a9cb-110">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="1a9cb-110">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a9cb-111">**addressSpace**</span><span class="sxs-lookup"><span data-stu-id="1a9cb-111">**addressSpace**</span></span> |<span data-ttu-id="1a9cb-112">Collection de préfixes d’adresses qui composent hello réseau virtuel en notation CIDR</span><span class="sxs-lookup"><span data-stu-id="1a9cb-112">Collection of address prefixes that make up hello VNet in CIDR notation</span></span> |<span data-ttu-id="1a9cb-113">192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="1a9cb-113">192.168.0.0/16</span></span> |
| <span data-ttu-id="1a9cb-114">**Sous-réseaux**</span><span class="sxs-lookup"><span data-stu-id="1a9cb-114">**subnets**</span></span> |<span data-ttu-id="1a9cb-115">Collection des sous-réseaux qui composent hello réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="1a9cb-115">Collection of subnets that make up hello VNet</span></span> |<span data-ttu-id="1a9cb-116">voir [sous-réseaux](#Subnets) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-116">see [subnets](#Subnets) below.</span></span> |
| <span data-ttu-id="1a9cb-117">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="1a9cb-117">**ipAddress**</span></span> |<span data-ttu-id="1a9cb-118">Adresse IP affectée tooobject.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-118">IP address assigned tooobject.</span></span> <span data-ttu-id="1a9cb-119">Il s’agit d’une propriété en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-119">This is a read-only property.</span></span> |<span data-ttu-id="1a9cb-120">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="1a9cb-120">104.42.233.77</span></span> |

### <a name="subnets"></a><span data-ttu-id="1a9cb-121">Sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="1a9cb-121">Subnets</span></span>
<span data-ttu-id="1a9cb-122">Un sous-réseau est une ressource enfant d’un réseau virtuel, et permet de définir des segments d’espaces d’adressage dans un bloc CIDR, à l’aide de préfixes d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-122">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="1a9cb-123">Cartes réseau peut être ajoutés toosubnets et tooVMs connecté, en offrant une connectivité pour différentes charges de travail.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-123">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="1a9cb-124">Sous-réseaux contiennent hello propriétés suivantes.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-124">Subnets contain hello following properties.</span></span> 

| <span data-ttu-id="1a9cb-125">Propriété</span><span class="sxs-lookup"><span data-stu-id="1a9cb-125">Property</span></span> | <span data-ttu-id="1a9cb-126">Description</span><span class="sxs-lookup"><span data-stu-id="1a9cb-126">Description</span></span> | <span data-ttu-id="1a9cb-127">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="1a9cb-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a9cb-128">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="1a9cb-128">**addressPrefix**</span></span> |<span data-ttu-id="1a9cb-129">Préfixe d’adresse unique qui composent le sous-réseau hello dans la notation CIDR</span><span class="sxs-lookup"><span data-stu-id="1a9cb-129">Single address prefix that make up hello subnet in CIDR notation</span></span> |<span data-ttu-id="1a9cb-130">192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="1a9cb-130">192.168.1.0/24</span></span> |
| <span data-ttu-id="1a9cb-131">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="1a9cb-131">**networkSecurityGroup**</span></span> |<span data-ttu-id="1a9cb-132">Groupe de sécurité réseau appliqué toohello sous-réseau</span><span class="sxs-lookup"><span data-stu-id="1a9cb-132">NSG applied toohello subnet</span></span> |<span data-ttu-id="1a9cb-133">voir [Groupes de sécurité réseau](#Network-Security-Group)</span><span class="sxs-lookup"><span data-stu-id="1a9cb-133">see [NSGs](#Network-Security-Group)</span></span> |
| <span data-ttu-id="1a9cb-134">**routeTable**</span><span class="sxs-lookup"><span data-stu-id="1a9cb-134">**routeTable**</span></span> |<span data-ttu-id="1a9cb-135">Table d’itinéraires appliqué toohello sous-réseau</span><span class="sxs-lookup"><span data-stu-id="1a9cb-135">Route table applied toohello subnet</span></span> |<span data-ttu-id="1a9cb-136">voir [itinéraires définis par l’utilisateur](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="1a9cb-136">see [UDR](#Route-table)</span></span> |
| <span data-ttu-id="1a9cb-137">**ipConfigurations**</span><span class="sxs-lookup"><span data-stu-id="1a9cb-137">**ipConfigurations**</span></span> |<span data-ttu-id="1a9cb-138">Collection d’objets de configuration IP utilisés par les cartes réseau connectées toohello sous-réseau</span><span class="sxs-lookup"><span data-stu-id="1a9cb-138">Collection of IP configruation objects used by NICs connected toohello subnet</span></span> |<span data-ttu-id="1a9cb-139">voir [itinéraires définis par l’utilisateur](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="1a9cb-139">see [UDR](#Route-table)</span></span> |

<span data-ttu-id="1a9cb-140">Exemple de réseau virtuel au format JSON :</span><span class="sxs-lookup"><span data-stu-id="1a9cb-140">Sample VNet in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="1a9cb-141">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1a9cb-141">Additional resources</span></span>
* <span data-ttu-id="1a9cb-142">Obtenez davantage d’informations sur les [réseaux virtuels](../articles/virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1a9cb-142">Get more information about [VNet](../articles/virtual-network/virtual-networks-overview.md).</span></span>
* <span data-ttu-id="1a9cb-143">Hello de lecture [documentation de référence API REST](https://msdn.microsoft.com/library/azure/mt163650.aspx) pour les réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-143">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163650.aspx) for VNets.</span></span>
* <span data-ttu-id="1a9cb-144">Hello de lecture [documentation de référence API REST](https://msdn.microsoft.com/library/azure/mt163618.aspx) des sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="1a9cb-144">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163618.aspx) for Subnets.</span></span>

