## <a name="nic"></a><span data-ttu-id="625bb-101">Carte d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="625bb-101">NIC</span></span>
<span data-ttu-id="625bb-102">Une ressource de carte d’interface réseau fournit un sous-réseau existant tooan connectivité réseau dans une ressource de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="625bb-102">A network interface card (NIC) resource provides network connectivity tooan existing subnet in a VNet resource.</span></span> <span data-ttu-id="625bb-103">Vous pouvez créer une carte réseau en tant qu’objet autonome, vous devez tooassociate il tooanother objet tooactually fournir la connectivité.</span><span class="sxs-lookup"><span data-stu-id="625bb-103">Although you can create a NIC as a stand alone object, you need tooassociate it tooanother object tooactually provide connectivity.</span></span> <span data-ttu-id="625bb-104">Une carte réseau peut être utilisé tooconnect tooa sous-réseau d’ordinateurs virtuels, une adresse IP publique ou un équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="625bb-104">A NIC can be used tooconnect a VM tooa subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="625bb-105">Propriété</span><span class="sxs-lookup"><span data-stu-id="625bb-105">Property</span></span> | <span data-ttu-id="625bb-106">Description</span><span class="sxs-lookup"><span data-stu-id="625bb-106">Description</span></span> | <span data-ttu-id="625bb-107">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="625bb-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="625bb-108">**virtualMachine**</span><span class="sxs-lookup"><span data-stu-id="625bb-108">**virtualMachine**</span></span> |<span data-ttu-id="625bb-109">Hello de machine virtuelle carte réseau est associé.</span><span class="sxs-lookup"><span data-stu-id="625bb-109">VM hello NIC is associated with.</span></span> |<span data-ttu-id="625bb-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="625bb-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="625bb-111">**macAddress**</span><span class="sxs-lookup"><span data-stu-id="625bb-111">**macAddress**</span></span> |<span data-ttu-id="625bb-112">Adresse MAC pour hello NIC</span><span class="sxs-lookup"><span data-stu-id="625bb-112">MAC address for hello NIC</span></span> |<span data-ttu-id="625bb-113">Toute valeur aléatoire comprise entre 4 et 30.</span><span class="sxs-lookup"><span data-stu-id="625bb-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="625bb-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="625bb-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="625bb-115">Groupe de sécurité réseau associé toohello carte réseau</span><span class="sxs-lookup"><span data-stu-id="625bb-115">NSG associated toohello NIC</span></span> |<span data-ttu-id="625bb-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="625bb-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="625bb-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="625bb-117">**dnsSettings**</span></span> |<span data-ttu-id="625bb-118">Paramètres DNS pour hello NIC</span><span class="sxs-lookup"><span data-stu-id="625bb-118">DNS settings for hello NIC</span></span> |<span data-ttu-id="625bb-119">Consultez [Adresse IP publique](#Public-IP-address)</span><span class="sxs-lookup"><span data-stu-id="625bb-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="625bb-120">Une carte d’Interface réseau ou NIC, représente une interface réseau qui peut être associés tooa virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="625bb-120">A Network Interface Card, or NIC, represents a network interface that can be associated tooa virtual machine (VM).</span></span> <span data-ttu-id="625bb-121">Une machine virtuelle peut comporter une ou plusieurs cartes d'interface réseau.</span><span class="sxs-lookup"><span data-stu-id="625bb-121">A VM can have one or more NICs.</span></span>

![Cartes d'interface réseau sur une seule machine virtuelle](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="625bb-123">Configurations IP</span><span class="sxs-lookup"><span data-stu-id="625bb-123">IP configurations</span></span>
<span data-ttu-id="625bb-124">Cartes réseau disposent d’un objet enfant nommé **ipConfigurations** contenant hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="625bb-124">NICs have a child object named **ipConfigurations** containing hello following properties:</span></span>

| <span data-ttu-id="625bb-125">Propriété</span><span class="sxs-lookup"><span data-stu-id="625bb-125">Property</span></span> | <span data-ttu-id="625bb-126">Description</span><span class="sxs-lookup"><span data-stu-id="625bb-126">Description</span></span> | <span data-ttu-id="625bb-127">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="625bb-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="625bb-128">**subnet**</span><span class="sxs-lookup"><span data-stu-id="625bb-128">**subnet**</span></span> |<span data-ttu-id="625bb-129">Hello de sous-réseau carte réseau est connectée à.</span><span class="sxs-lookup"><span data-stu-id="625bb-129">Subnet hello NIC is onnected to.</span></span> |<span data-ttu-id="625bb-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="625bb-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="625bb-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="625bb-131">**privateIPAddress**</span></span> |<span data-ttu-id="625bb-132">Adresse IP pour hello carte réseau dans un sous-réseau de hello</span><span class="sxs-lookup"><span data-stu-id="625bb-132">IP address for hello NIC in hello subnet</span></span> |<span data-ttu-id="625bb-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="625bb-133">10.0.0.8</span></span> |
| <span data-ttu-id="625bb-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="625bb-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="625bb-135">Méthode d’allocation des adresses IP</span><span class="sxs-lookup"><span data-stu-id="625bb-135">IP allocation method</span></span> |<span data-ttu-id="625bb-136">Dynamic ou Static</span><span class="sxs-lookup"><span data-stu-id="625bb-136">Dynamic or Static</span></span> |
| <span data-ttu-id="625bb-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="625bb-137">**enableIPForwarding**</span></span> |<span data-ttu-id="625bb-138">Si hello carte réseau peut être utilisé pour le routage</span><span class="sxs-lookup"><span data-stu-id="625bb-138">Whether hello NIC can be used for routing</span></span> |<span data-ttu-id="625bb-139">true ou false</span><span class="sxs-lookup"><span data-stu-id="625bb-139">true or false</span></span> |
| <span data-ttu-id="625bb-140">**primary**</span><span class="sxs-lookup"><span data-stu-id="625bb-140">**primary**</span></span> |<span data-ttu-id="625bb-141">Si hello NIC est hello carte réseau principale pour hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="625bb-141">Whether hello NIC is hello primary NIC for hello VM</span></span> |<span data-ttu-id="625bb-142">true ou false</span><span class="sxs-lookup"><span data-stu-id="625bb-142">true or false</span></span> |
| <span data-ttu-id="625bb-143">**publicIPAddress**</span><span class="sxs-lookup"><span data-stu-id="625bb-143">**publicIPAddress**</span></span> |<span data-ttu-id="625bb-144">PIP associé hello NIC</span><span class="sxs-lookup"><span data-stu-id="625bb-144">PIP associated with hello NIC</span></span> |<span data-ttu-id="625bb-145">Consultez [Paramètres DNS](#DNS-settings)</span><span class="sxs-lookup"><span data-stu-id="625bb-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="625bb-146">**loadBalancerBackendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="625bb-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="625bb-147">Sauvegarder hello de pools fin adresse que NIC est associé</span><span class="sxs-lookup"><span data-stu-id="625bb-147">Back end address pools hello NIC is associated with</span></span> | |
| <span data-ttu-id="625bb-148">**loadBalancerInboundNatRules**</span><span class="sxs-lookup"><span data-stu-id="625bb-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="625bb-149">Trafic entrant charge hello du règles NAT d’équilibrage de la que carte réseau est associé</span><span class="sxs-lookup"><span data-stu-id="625bb-149">Inbound load balancer NAT rules hello NIC is associated with</span></span> | |

<span data-ttu-id="625bb-150">Exemple d’adresse IP publique au format JSON :</span><span class="sxs-lookup"><span data-stu-id="625bb-150">Sample public IP address in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="625bb-151">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="625bb-151">Additional resources</span></span>
* <span data-ttu-id="625bb-152">Hello de lecture [documentation de référence API REST](https://msdn.microsoft.com/library/azure/mt163579.aspx) pour les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="625bb-152">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

