## <a name="network-security-group"></a><span data-ttu-id="89bd6-101">Groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="89bd6-101">Network Security Group</span></span>
<span data-ttu-id="89bd6-102">Une ressource de groupe de sécurité réseau permet la création de hello de limite de sécurité pour les charges de travail, en implémentant autoriser et refuser des règles.</span><span class="sxs-lookup"><span data-stu-id="89bd6-102">An NSG resource enables hello creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="89bd6-103">Ces règles peuvent être appliquées tooa machine virtuelle, une carte réseau ou un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="89bd6-103">Such rules can be applied tooa VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="89bd6-104">Propriété</span><span class="sxs-lookup"><span data-stu-id="89bd6-104">Property</span></span> | <span data-ttu-id="89bd6-105">Description</span><span class="sxs-lookup"><span data-stu-id="89bd6-105">Description</span></span> | <span data-ttu-id="89bd6-106">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="89bd6-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="89bd6-107">**Sous-réseaux**</span><span class="sxs-lookup"><span data-stu-id="89bd6-107">**subnets**</span></span> |<span data-ttu-id="89bd6-108">Liste des ID de sous-réseau hello NSG est appliquée à.</span><span class="sxs-lookup"><span data-stu-id="89bd6-108">List of subnet ids hello NSG is applied to.</span></span> |<span data-ttu-id="89bd6-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="89bd6-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="89bd6-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="89bd6-110">**securityRules**</span></span> |<span data-ttu-id="89bd6-111">Liste des règles de sécurité qui composent hello NSG</span><span class="sxs-lookup"><span data-stu-id="89bd6-111">List of security rules that make up hello NSG</span></span> |<span data-ttu-id="89bd6-112">Voir [Règle de sécurité](#Security-rule) ci-dessous</span><span class="sxs-lookup"><span data-stu-id="89bd6-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="89bd6-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="89bd6-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="89bd6-114">Liste des règles de sécurité par défaut présentes dans chaque groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="89bd6-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="89bd6-115">Voir [Règles de sécurité par défaut](#Default-security-rules) ci-dessous</span><span class="sxs-lookup"><span data-stu-id="89bd6-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="89bd6-116">**Règle de sécurité** : plusieurs règles de sécurité peuvent être définies pour un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="89bd6-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="89bd6-117">Chaque règle peut autoriser ou refuser différents types de trafic.</span><span class="sxs-lookup"><span data-stu-id="89bd6-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="89bd6-118">Règle de sécurité</span><span class="sxs-lookup"><span data-stu-id="89bd6-118">Security rule</span></span>
<span data-ttu-id="89bd6-119">Une règle de sécurité est une ressource de l’enfant d’un groupe de sécurité réseau qui contient les propriétés hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="89bd6-119">A security rule is a child resource of an NSG containing hello properties below.</span></span>

| <span data-ttu-id="89bd6-120">Propriété</span><span class="sxs-lookup"><span data-stu-id="89bd6-120">Property</span></span> | <span data-ttu-id="89bd6-121">Description</span><span class="sxs-lookup"><span data-stu-id="89bd6-121">Description</span></span> | <span data-ttu-id="89bd6-122">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="89bd6-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="89bd6-123">**description**</span><span class="sxs-lookup"><span data-stu-id="89bd6-123">**description**</span></span> |<span data-ttu-id="89bd6-124">Description de règle de hello</span><span class="sxs-lookup"><span data-stu-id="89bd6-124">Description for hello rule</span></span> |<span data-ttu-id="89bd6-125">Autoriser le trafic entrant pour toutes les machines virtuelles dans un sous-réseau X</span><span class="sxs-lookup"><span data-stu-id="89bd6-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="89bd6-126">**protocol**</span><span class="sxs-lookup"><span data-stu-id="89bd6-126">**protocol**</span></span> |<span data-ttu-id="89bd6-127">Toomatch de protocole pour la règle de hello</span><span class="sxs-lookup"><span data-stu-id="89bd6-127">Protocol toomatch for hello rule</span></span> |<span data-ttu-id="89bd6-128">TCP, UDP ou *</span><span class="sxs-lookup"><span data-stu-id="89bd6-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="89bd6-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="89bd6-129">**sourcePortRange**</span></span> |<span data-ttu-id="89bd6-130">Toomatch de plage de port source pour la règle de hello</span><span class="sxs-lookup"><span data-stu-id="89bd6-130">Source port range toomatch for hello rule</span></span> |<span data-ttu-id="89bd6-131">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="89bd6-131">80, 100-200, *</span></span> |
| <span data-ttu-id="89bd6-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="89bd6-132">**destinationPortRange**</span></span> |<span data-ttu-id="89bd6-133">Toomatch de plage de port de destination pour la règle de hello</span><span class="sxs-lookup"><span data-stu-id="89bd6-133">Destination port range toomatch for hello rule</span></span> |<span data-ttu-id="89bd6-134">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="89bd6-134">80, 100-200, *</span></span> |
| <span data-ttu-id="89bd6-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="89bd6-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="89bd6-136">Toomatch de préfixe d’adresse source pour la règle de hello</span><span class="sxs-lookup"><span data-stu-id="89bd6-136">Source address prefix toomatch for hello rule</span></span> |<span data-ttu-id="89bd6-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="89bd6-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="89bd6-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="89bd6-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="89bd6-139">Toomatch de préfixe d’adresse destination pour la règle de hello</span><span class="sxs-lookup"><span data-stu-id="89bd6-139">Destination address prefix toomatch for hello rule</span></span> |<span data-ttu-id="89bd6-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="89bd6-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="89bd6-141">**direction**</span><span class="sxs-lookup"><span data-stu-id="89bd6-141">**direction**</span></span> |<span data-ttu-id="89bd6-142">Direction de toomatch le trafic pour la règle de hello</span><span class="sxs-lookup"><span data-stu-id="89bd6-142">Direction of traffic toomatch for hello rule</span></span> |<span data-ttu-id="89bd6-143">entrant ou sortant</span><span class="sxs-lookup"><span data-stu-id="89bd6-143">inbound or outbound</span></span> |
| <span data-ttu-id="89bd6-144">**priority**</span><span class="sxs-lookup"><span data-stu-id="89bd6-144">**priority**</span></span> |<span data-ttu-id="89bd6-145">Priorité de la règle de hello.</span><span class="sxs-lookup"><span data-stu-id="89bd6-145">Priority for hello rule.</span></span> <span data-ttu-id="89bd6-146">Les règles sont vérifiées dans l'ordre de priorité ; une fois qu'une règle s'applique, plus aucune règle n'est testée pour la correspondance.</span><span class="sxs-lookup"><span data-stu-id="89bd6-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="89bd6-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="89bd6-147">10, 100, 65000</span></span> |
| <span data-ttu-id="89bd6-148">**access**</span><span class="sxs-lookup"><span data-stu-id="89bd6-148">**access**</span></span> |<span data-ttu-id="89bd6-149">Type d’accès tooapply si hello règle correspond à</span><span class="sxs-lookup"><span data-stu-id="89bd6-149">Type of access tooapply if hello rule matches</span></span> |<span data-ttu-id="89bd6-150">autoriser ou refuser</span><span class="sxs-lookup"><span data-stu-id="89bd6-150">allow or deny</span></span> |

<span data-ttu-id="89bd6-151">Exemple de groupe de sécurité réseau au format JSON :</span><span class="sxs-lookup"><span data-stu-id="89bd6-151">Sample NSG in JSON format:</span></span>

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a><span data-ttu-id="89bd6-152">Règles de sécurité par défaut</span><span class="sxs-lookup"><span data-stu-id="89bd6-152">Default security rules</span></span>

<span data-ttu-id="89bd6-153">Règles de sécurité par défaut ont hello mêmes propriétés sont disponibles dans les règles de sécurité.</span><span class="sxs-lookup"><span data-stu-id="89bd6-153">Default security rules have hello same properties available in security rules.</span></span> <span data-ttu-id="89bd6-154">Ils existent tooprovide une connectivité de base entre les ressources qui ont des groupes de sécurité réseau appliquées toothem.</span><span class="sxs-lookup"><span data-stu-id="89bd6-154">They exist tooprovide basic connectivity between resources that have NSGs applied toothem.</span></span> <span data-ttu-id="89bd6-155">Vérifiez les [règles de sécurité par défaut](../articles/virtual-network/virtual-networks-nsg.md#default-rules) existantes.</span><span class="sxs-lookup"><span data-stu-id="89bd6-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="89bd6-156">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="89bd6-156">Additional resources</span></span>
* <span data-ttu-id="89bd6-157">Obtenez davantage d'informations sur les [groupes de sécurité réseau](../articles/virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="89bd6-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="89bd6-158">Hello de lecture [documentation de référence API REST](https://msdn.microsoft.com/library/azure/mt163615.aspx) pour les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="89bd6-158">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="89bd6-159">Hello de lecture [documentation de référence API REST](https://msdn.microsoft.com/library/azure/mt163580.aspx) de règles de sécurité.</span><span class="sxs-lookup"><span data-stu-id="89bd6-159">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
