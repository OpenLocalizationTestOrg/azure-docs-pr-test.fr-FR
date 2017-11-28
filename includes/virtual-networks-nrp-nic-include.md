## <a name="nic"></a><span data-ttu-id="690ae-101">Carte d'interface réseau</span><span class="sxs-lookup"><span data-stu-id="690ae-101">NIC</span></span>
<span data-ttu-id="690ae-102">Une ressource de carte d’interface réseau fournit la connectivité à un sous-réseau existant dans une ressource de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="690ae-102">A network interface card (NIC) resource provides network connectivity to an existing subnet in a VNet resource.</span></span> <span data-ttu-id="690ae-103">Bien que vous puissiez créer une carte d’interface réseau en tant qu’objet autonome, vous devez l’associer à un autre objet pour fournir réellement la connectivité.</span><span class="sxs-lookup"><span data-stu-id="690ae-103">Although you can create a NIC as a stand alone object, you need to associate it to another object to actually provide connectivity.</span></span> <span data-ttu-id="690ae-104">Une carte d’interface réseau permet de connecter une machine virtuelle à un sous-réseau, à une adresse IP publique ou à un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="690ae-104">A NIC can be used to connect a VM to a subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="690ae-105">Propriété</span><span class="sxs-lookup"><span data-stu-id="690ae-105">Property</span></span> | <span data-ttu-id="690ae-106">Description</span><span class="sxs-lookup"><span data-stu-id="690ae-106">Description</span></span> | <span data-ttu-id="690ae-107">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="690ae-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="690ae-108">**virtualMachine**</span><span class="sxs-lookup"><span data-stu-id="690ae-108">**virtualMachine**</span></span> |<span data-ttu-id="690ae-109">Machine virtuelle à laquelle est associée la carte d’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="690ae-109">VM the NIC is associated with.</span></span> |<span data-ttu-id="690ae-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="690ae-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="690ae-111">**macAddress**</span><span class="sxs-lookup"><span data-stu-id="690ae-111">**macAddress**</span></span> |<span data-ttu-id="690ae-112">Adresse MAC de la carte d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="690ae-112">MAC address for the NIC</span></span> |<span data-ttu-id="690ae-113">Toute valeur aléatoire comprise entre 4 et 30.</span><span class="sxs-lookup"><span data-stu-id="690ae-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="690ae-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="690ae-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="690ae-115">Groupe de sécurité réseau associé à la carte d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="690ae-115">NSG associated to the NIC</span></span> |<span data-ttu-id="690ae-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="690ae-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="690ae-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="690ae-117">**dnsSettings**</span></span> |<span data-ttu-id="690ae-118">Paramètres DNS pour la carte d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="690ae-118">DNS settings for the NIC</span></span> |<span data-ttu-id="690ae-119">Consultez [Adresse IP publique](#Public-IP-address)</span><span class="sxs-lookup"><span data-stu-id="690ae-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="690ae-120">La carte d'interface réseau, ou NIC, représente une interface réseau qui peut être associée à une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="690ae-120">A Network Interface Card, or NIC, represents a network interface that can be associated to a virtual machine (VM).</span></span> <span data-ttu-id="690ae-121">Une machine virtuelle peut comporter une ou plusieurs cartes d'interface réseau.</span><span class="sxs-lookup"><span data-stu-id="690ae-121">A VM can have one or more NICs.</span></span>

![Cartes d'interface réseau sur une seule machine virtuelle](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="690ae-123">Configurations IP</span><span class="sxs-lookup"><span data-stu-id="690ae-123">IP configurations</span></span>
<span data-ttu-id="690ae-124">Les cartes d’interface réseau ont un objet enfant nommé **ipConfigurations** qui contient les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="690ae-124">NICs have a child object named **ipConfigurations** containing the following properties:</span></span>

| <span data-ttu-id="690ae-125">Propriété</span><span class="sxs-lookup"><span data-stu-id="690ae-125">Property</span></span> | <span data-ttu-id="690ae-126">Description</span><span class="sxs-lookup"><span data-stu-id="690ae-126">Description</span></span> | <span data-ttu-id="690ae-127">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="690ae-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="690ae-128">**subnet**</span><span class="sxs-lookup"><span data-stu-id="690ae-128">**subnet**</span></span> |<span data-ttu-id="690ae-129">Sous-réseau auquel est connectée la carte d’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="690ae-129">Subnet the NIC is onnected to.</span></span> |<span data-ttu-id="690ae-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="690ae-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="690ae-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="690ae-131">**privateIPAddress**</span></span> |<span data-ttu-id="690ae-132">Adresse IP de la carte d’interface réseau dans le sous-réseau</span><span class="sxs-lookup"><span data-stu-id="690ae-132">IP address for the NIC in the subnet</span></span> |<span data-ttu-id="690ae-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="690ae-133">10.0.0.8</span></span> |
| <span data-ttu-id="690ae-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="690ae-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="690ae-135">Méthode d’allocation des adresses IP</span><span class="sxs-lookup"><span data-stu-id="690ae-135">IP allocation method</span></span> |<span data-ttu-id="690ae-136">Dynamic ou Static</span><span class="sxs-lookup"><span data-stu-id="690ae-136">Dynamic or Static</span></span> |
| <span data-ttu-id="690ae-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="690ae-137">**enableIPForwarding**</span></span> |<span data-ttu-id="690ae-138">Détermine si la carte d’interface réseau peut être utilisée pour le routage</span><span class="sxs-lookup"><span data-stu-id="690ae-138">Whether the NIC can be used for routing</span></span> |<span data-ttu-id="690ae-139">true ou false</span><span class="sxs-lookup"><span data-stu-id="690ae-139">true or false</span></span> |
| <span data-ttu-id="690ae-140">**primary**</span><span class="sxs-lookup"><span data-stu-id="690ae-140">**primary**</span></span> |<span data-ttu-id="690ae-141">Détermine si la carte d’interface réseau est la carte d’interface réseau principale de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="690ae-141">Whether the NIC is the primary NIC for the VM</span></span> |<span data-ttu-id="690ae-142">true ou false</span><span class="sxs-lookup"><span data-stu-id="690ae-142">true or false</span></span> |
| <span data-ttu-id="690ae-143">**publicIPAddress**</span><span class="sxs-lookup"><span data-stu-id="690ae-143">**publicIPAddress**</span></span> |<span data-ttu-id="690ae-144">Adresse IP publique associée à la carte d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="690ae-144">PIP associated with the NIC</span></span> |<span data-ttu-id="690ae-145">Consultez [Paramètres DNS](#DNS-settings)</span><span class="sxs-lookup"><span data-stu-id="690ae-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="690ae-146">**loadBalancerBackendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="690ae-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="690ae-147">Pools d’adresses principaux auxquels la carte d’interface réseau est associée</span><span class="sxs-lookup"><span data-stu-id="690ae-147">Back end address pools the NIC is associated with</span></span> | |
| <span data-ttu-id="690ae-148">**loadBalancerInboundNatRules**</span><span class="sxs-lookup"><span data-stu-id="690ae-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="690ae-149">Règles NAT de trafic entrant de l’équilibreur de charge auxquelles est associée la carte d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="690ae-149">Inbound load balancer NAT rules the NIC is associated with</span></span> | |

<span data-ttu-id="690ae-150">Exemple d’adresse IP publique au format JSON :</span><span class="sxs-lookup"><span data-stu-id="690ae-150">Sample public IP address in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="690ae-151">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="690ae-151">Additional resources</span></span>
* <span data-ttu-id="690ae-152">Consultez la [documentation de référence d’API REST](https://msdn.microsoft.com/library/azure/mt163579.aspx) pour les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="690ae-152">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

