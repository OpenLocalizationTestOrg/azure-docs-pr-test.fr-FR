## <a name="network-security-group"></a><span data-ttu-id="069e3-101">Groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="069e3-101">Network Security Group</span></span>
<span data-ttu-id="069e3-102">Une ressource de groupe de sécurité réseau permet de créer des limites de sécurité pour les charges de travail, en implémentant des règles d'autorisation et de refus.</span><span class="sxs-lookup"><span data-stu-id="069e3-102">An NSG resource enables the creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="069e3-103">Ces règles peuvent être appliquées à une machine virtuelle, une carte réseau ou un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="069e3-103">Such rules can be applied to a VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="069e3-104">Propriété</span><span class="sxs-lookup"><span data-stu-id="069e3-104">Property</span></span> | <span data-ttu-id="069e3-105">Description</span><span class="sxs-lookup"><span data-stu-id="069e3-105">Description</span></span> | <span data-ttu-id="069e3-106">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="069e3-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="069e3-107">**Sous-réseaux**</span><span class="sxs-lookup"><span data-stu-id="069e3-107">**subnets**</span></span> |<span data-ttu-id="069e3-108">Liste des ID de sous-réseau auxquels le groupe de sécurité réseau s'applique.</span><span class="sxs-lookup"><span data-stu-id="069e3-108">List of subnet ids the NSG is applied to.</span></span> |<span data-ttu-id="069e3-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="069e3-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="069e3-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="069e3-110">**securityRules**</span></span> |<span data-ttu-id="069e3-111">Liste des règles de sécurité qui composent le groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="069e3-111">List of security rules that make up the NSG</span></span> |<span data-ttu-id="069e3-112">Voir [Règle de sécurité](#Security-rule) ci-dessous</span><span class="sxs-lookup"><span data-stu-id="069e3-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="069e3-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="069e3-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="069e3-114">Liste des règles de sécurité par défaut présentes dans chaque groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="069e3-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="069e3-115">Voir [Règles de sécurité par défaut](#Default-security-rules) ci-dessous</span><span class="sxs-lookup"><span data-stu-id="069e3-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="069e3-116">**Règle de sécurité** : plusieurs règles de sécurité peuvent être définies pour un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="069e3-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="069e3-117">Chaque règle peut autoriser ou refuser différents types de trafic.</span><span class="sxs-lookup"><span data-stu-id="069e3-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="069e3-118">Règle de sécurité</span><span class="sxs-lookup"><span data-stu-id="069e3-118">Security rule</span></span>
<span data-ttu-id="069e3-119">Une règle de sécurité est une ressource enfant d'un groupe de sécurité réseau qui contient les propriétés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="069e3-119">A security rule is a child resource of an NSG containing the properties below.</span></span>

| <span data-ttu-id="069e3-120">Propriété</span><span class="sxs-lookup"><span data-stu-id="069e3-120">Property</span></span> | <span data-ttu-id="069e3-121">Description</span><span class="sxs-lookup"><span data-stu-id="069e3-121">Description</span></span> | <span data-ttu-id="069e3-122">Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="069e3-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="069e3-123">**description**</span><span class="sxs-lookup"><span data-stu-id="069e3-123">**description**</span></span> |<span data-ttu-id="069e3-124">Description de la règle</span><span class="sxs-lookup"><span data-stu-id="069e3-124">Description for the rule</span></span> |<span data-ttu-id="069e3-125">Autoriser le trafic entrant pour toutes les machines virtuelles dans un sous-réseau X</span><span class="sxs-lookup"><span data-stu-id="069e3-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="069e3-126">**protocol**</span><span class="sxs-lookup"><span data-stu-id="069e3-126">**protocol**</span></span> |<span data-ttu-id="069e3-127">Protocole à faire correspondre pour la règle</span><span class="sxs-lookup"><span data-stu-id="069e3-127">Protocol to match for the rule</span></span> |<span data-ttu-id="069e3-128">TCP, UDP ou *</span><span class="sxs-lookup"><span data-stu-id="069e3-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="069e3-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="069e3-129">**sourcePortRange**</span></span> |<span data-ttu-id="069e3-130">Plage de ports source à faire correspondre pour la règle</span><span class="sxs-lookup"><span data-stu-id="069e3-130">Source port range to match for the rule</span></span> |<span data-ttu-id="069e3-131">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="069e3-131">80, 100-200, *</span></span> |
| <span data-ttu-id="069e3-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="069e3-132">**destinationPortRange**</span></span> |<span data-ttu-id="069e3-133">Plage de ports de destination à faire correspondre pour la règle</span><span class="sxs-lookup"><span data-stu-id="069e3-133">Destination port range to match for the rule</span></span> |<span data-ttu-id="069e3-134">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="069e3-134">80, 100-200, *</span></span> |
| <span data-ttu-id="069e3-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="069e3-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="069e3-136">Préfixe d'adresse source à faire correspondre pour la règle</span><span class="sxs-lookup"><span data-stu-id="069e3-136">Source address prefix to match for the rule</span></span> |<span data-ttu-id="069e3-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="069e3-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="069e3-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="069e3-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="069e3-139">Préfixe d'adresse de destination à faire correspondre pour la règle</span><span class="sxs-lookup"><span data-stu-id="069e3-139">Destination address prefix to match for the rule</span></span> |<span data-ttu-id="069e3-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="069e3-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="069e3-141">**direction**</span><span class="sxs-lookup"><span data-stu-id="069e3-141">**direction**</span></span> |<span data-ttu-id="069e3-142">Direction du trafic à faire correspondre pour la règle</span><span class="sxs-lookup"><span data-stu-id="069e3-142">Direction of traffic to match for the rule</span></span> |<span data-ttu-id="069e3-143">entrant ou sortant</span><span class="sxs-lookup"><span data-stu-id="069e3-143">inbound or outbound</span></span> |
| <span data-ttu-id="069e3-144">**priority**</span><span class="sxs-lookup"><span data-stu-id="069e3-144">**priority**</span></span> |<span data-ttu-id="069e3-145">Priorité de la règle.</span><span class="sxs-lookup"><span data-stu-id="069e3-145">Priority for the rule.</span></span> <span data-ttu-id="069e3-146">Les règles sont vérifiées dans l'ordre de priorité ; une fois qu'une règle s'applique, plus aucune règle n'est testée pour la correspondance.</span><span class="sxs-lookup"><span data-stu-id="069e3-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="069e3-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="069e3-147">10, 100, 65000</span></span> |
| <span data-ttu-id="069e3-148">**access**</span><span class="sxs-lookup"><span data-stu-id="069e3-148">**access**</span></span> |<span data-ttu-id="069e3-149">Type d'accès à appliquer si la règle correspond</span><span class="sxs-lookup"><span data-stu-id="069e3-149">Type of access to apply if the rule matches</span></span> |<span data-ttu-id="069e3-150">autoriser ou refuser</span><span class="sxs-lookup"><span data-stu-id="069e3-150">allow or deny</span></span> |

<span data-ttu-id="069e3-151">Exemple de groupe de sécurité réseau au format JSON :</span><span class="sxs-lookup"><span data-stu-id="069e3-151">Sample NSG in JSON format:</span></span>

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

### <a name="default-security-rules"></a><span data-ttu-id="069e3-152">Règles de sécurité par défaut</span><span class="sxs-lookup"><span data-stu-id="069e3-152">Default security rules</span></span>

<span data-ttu-id="069e3-153">Les règles de sécurité par défaut ont les mêmes propriétés que les règles de sécurité.</span><span class="sxs-lookup"><span data-stu-id="069e3-153">Default security rules have the same properties available in security rules.</span></span> <span data-ttu-id="069e3-154">Elles existent pour fournir une connectivité de base entre les ressources qui ont un groupe de sécurité réseau appliqué.</span><span class="sxs-lookup"><span data-stu-id="069e3-154">They exist to provide basic connectivity between resources that have NSGs applied to them.</span></span> <span data-ttu-id="069e3-155">Vérifiez les [règles de sécurité par défaut](../articles/virtual-network/virtual-networks-nsg.md#default-rules) existantes.</span><span class="sxs-lookup"><span data-stu-id="069e3-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="069e3-156">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="069e3-156">Additional resources</span></span>
* <span data-ttu-id="069e3-157">Obtenez davantage d'informations sur les [groupes de sécurité réseau](../articles/virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="069e3-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="069e3-158">Consultez la [documentation de référence d'API REST](https://msdn.microsoft.com/library/azure/mt163615.aspx) pour les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="069e3-158">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="069e3-159">Consultez la [documentation de référence d'API REST](https://msdn.microsoft.com/library/azure/mt163580.aspx) pour les règles de sécurité.</span><span class="sxs-lookup"><span data-stu-id="069e3-159">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
