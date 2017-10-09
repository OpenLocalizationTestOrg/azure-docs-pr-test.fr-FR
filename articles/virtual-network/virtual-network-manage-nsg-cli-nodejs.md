---
title: "aaaManage réseau des groupes de sécurité - Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment les groupes de sécurité réseau toomanage à l’aide de hello Azure interface de ligne de commande (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9a429f947abbcb5fa6adb40c84504f68efd5e20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="07b91-103">Gérer les groupes de sécurité réseau à l’aide de hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="07b91-103">Manage network security groups using hello Azure CLI 1.0</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="07b91-104">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="07b91-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="07b91-105">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="07b91-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="07b91-106">[Azure CLI 1.0](#View-existing-NSGs) – notre CLI pour les modèles de déploiement gestion classique et les ressources des hello</span><span class="sxs-lookup"><span data-stu-id="07b91-106">[Azure CLI 1.0](#View-existing-NSGs) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="07b91-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion hello de ressource (cet article)</span><span class="sxs-lookup"><span data-stu-id="07b91-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="07b91-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="07b91-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="07b91-109">Cet article décrit à l’aide du modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="07b91-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="07b91-110">Récupérer des informations</span><span class="sxs-lookup"><span data-stu-id="07b91-110">Retrieve Information</span></span>
<span data-ttu-id="07b91-111">Vous pouvez afficher vos groupes de sécurité réseau existants, récupérer des règles pour un groupe de sécurité réseau existant et découvrir quelles sont les ressources associées à un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="07b91-111">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="07b91-112">Afficher les groupes de sécurité réseau existants</span><span class="sxs-lookup"><span data-stu-id="07b91-112">View existing NSGs</span></span>
<span data-ttu-id="07b91-113">liste de hello tooview de groupes de sécurité réseau dans un groupe de ressources spécifique, exécutez hello `azure network nsg list` commande comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="07b91-113">tooview hello list of NSGs in a specific resource group, run hello `azure network nsg list` command as shown below.</span></span>

```azurecli
azure network nsg list --resource-group RG-NSG
```

<span data-ttu-id="07b91-114">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="07b91-114">Expected output:</span></span>

    info:    Executing command network nsg list
    + Getting hello network security groups
    data:    Name          Location
    data:    ------------  --------
    data:    NSG-BackEnd   westus
    data:    NSG-FrontEnd  westus
    info:    network nsg list command OK

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="07b91-115">Répertorier toutes les règles pour un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="07b91-115">List all rules for an NSG</span></span>
<span data-ttu-id="07b91-116">règles de hello tooview d’un groupe de sécurité réseau nommé **NSG-FrontEnd**, hello exécutez `azure network nsg show` commande comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="07b91-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello `azure network nsg show` command as shown below.</span></span> 

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd
```

<span data-ttu-id="07b91-117">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="07b91-117">Expected output:</span></span>

    info:    Executing command network nsg show
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Name                            : NSG-FrontEnd
    data:    Type                            : Microsoft.Network/networkSecurityGroups
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    Tags                            : displayName=NSG - Front End
    data:    Security group rules:
    data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
    data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
    data:    rdp-rule                       Internet           *            *               3389              Tcp       Inbound    Allow   100
    data:    web-rule                       Internet           *            *               80                Tcp       Inbound    Allow   101
    data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000
    data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001
    data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500
    data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000
    data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001
    data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500
    info:    network nsg show command OK

> [!NOTE]
> <span data-ttu-id="07b91-118">Vous pouvez également utiliser `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` règles hello toolist hello **NSG-FrontEnd** groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="07b91-118">You can also use `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` toolist hello rules from hello **NSG-FrontEnd** NSG.</span></span>
>

### <a name="view-nsg-associations"></a><span data-ttu-id="07b91-119">Afficher les associations de groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="07b91-119">View NSG associations</span></span>

<span data-ttu-id="07b91-120">tooview hello de quelles ressources **NSG-FrontEnd** groupe de sécurité réseau est hello associez, exécutez `azure network nsg show` commande comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="07b91-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `azure network nsg show` command as shown below.</span></span> <span data-ttu-id="07b91-121">Notez que hello seule différence est utilisation hello Hello **--json** paramètre.</span><span class="sxs-lookup"><span data-stu-id="07b91-121">Notice that hello only difference is hello use of hello **--json** parameter.</span></span>

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json
```

<span data-ttu-id="07b91-122">Recherchez hello **networkInterfaces** et **sous-réseaux** propriétés comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="07b91-122">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

    "networkInterfaces": [],
    ...
    "subnets": [
        {
            "id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
        }
    ],
    ...

<span data-ttu-id="07b91-123">Dans l’exemple hello ci-dessus, hello groupe de sécurité réseau n’est pas associé tooany les interfaces réseau (NIC), et il s’agit de sous-réseau associé tooa nommé **frontal**.</span><span class="sxs-lookup"><span data-stu-id="07b91-123">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="07b91-124">Gérer les règles</span><span class="sxs-lookup"><span data-stu-id="07b91-124">Manage rules</span></span>
<span data-ttu-id="07b91-125">Vous pouvez ajouter tooan règles existants du groupe de sécurité réseau, modifier les règles existantes et supprimer des règles.</span><span class="sxs-lookup"><span data-stu-id="07b91-125">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="07b91-126">Ajouter une règle</span><span class="sxs-lookup"><span data-stu-id="07b91-126">Add a rule</span></span>
<span data-ttu-id="07b91-127">tooadd une règle autorisant **entrant** trafic tooport **443** à partir de n’importe quel ordinateur toohello **NSG-FrontEnd** groupe de sécurité réseau, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07b91-127">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
azure network nsg rule create --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --description "Allow access tooport 443 for HTTPS" \
    --protocol Tcp \
    --source-address-prefix * \
    --source-port-range * \
    --destination-address-prefix * \
    --destination-port-range 443 \
    --access Allow \
    --priority 102 \
    --direction Inbound
```

<span data-ttu-id="07b91-128">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="07b91-128">Expected output:</span></span>

    info:    Executing command network nsg rule create
    + Looking up hello network security rule "allow-https"
    + Creating a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : *
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule create command OK

### <a name="change-a-rule"></a><span data-ttu-id="07b91-129">Modifier une règle</span><span class="sxs-lookup"><span data-stu-id="07b91-129">Change a rule</span></span>
<span data-ttu-id="07b91-130">règle de hello toochange créé ci-dessus tooallow le trafic entrant provenance hello **Internet** uniquement, exécutez hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07b91-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello following command:</span></span>

```azurecli
azure network nsg rule set --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --source-address-prefix Internet
```

<span data-ttu-id="07b91-131">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="07b91-131">Expected output:</span></span>

    info:    Executing command network nsg rule set
    + Looking up hello network security group "NSG-FrontEnd"
    + Setting a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : Internet
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule set command OK

### <a name="delete-a-rule"></a><span data-ttu-id="07b91-132">Supprimer une règle</span><span class="sxs-lookup"><span data-stu-id="07b91-132">Delete a rule</span></span>
<span data-ttu-id="07b91-133">règle de hello toodelete créé ci-dessus, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07b91-133">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
azure network nsg rule delete --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --quiet
```

> [!NOTE]
> <span data-ttu-id="07b91-134">Hello `--quiet` paramètre garantit que vous n’avez pas besoin de tooconfirm la suppression hello.</span><span class="sxs-lookup"><span data-stu-id="07b91-134">hello `--quiet` parameter ensures you don't need tooconfirm hello deletion.</span></span>
>

<span data-ttu-id="07b91-135">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="07b91-135">Expected output:</span></span>

    info:    Executing command network nsg rule delete
    + Looking up hello network security group "NSG-FrontEnd"
    + Deleting network security rule "allow-https"
    info:    network nsg rule delete command OK

## <a name="manage-associations"></a><span data-ttu-id="07b91-136">Gérer les associations</span><span class="sxs-lookup"><span data-stu-id="07b91-136">Manage associations</span></span>
<span data-ttu-id="07b91-137">Vous pouvez associer un toosubnets du groupe de sécurité réseau et les cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="07b91-137">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="07b91-138">Vous pouvez également dissocier un groupe de sécurité réseau de n’importe quelle ressource à laquelle il est associé.</span><span class="sxs-lookup"><span data-stu-id="07b91-138">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="07b91-139">Associer un groupe de sécurité réseau de tooa carte réseau</span><span class="sxs-lookup"><span data-stu-id="07b91-139">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="07b91-140">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** carte réseau, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07b91-140">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG \
    --name TestNICWeb1 \
    --network-security-group-name NSG-FrontEnd
```

<span data-ttu-id="07b91-141">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="07b91-141">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Looking up hello network security group "NSG-FrontEnd"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Network security group          : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Virtual machine                 : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="07b91-142">Dissocier un groupe de sécurité réseau d’une carte réseau</span><span class="sxs-lookup"><span data-stu-id="07b91-142">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="07b91-143">toodissociate hello **NSG-FrontEnd** groupe de sécurité réseau à partir de hello **TestNICWeb1** carte réseau, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07b91-143">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG --name TestNICWeb1 --network-security-group-id ""
```

> [!NOTE]
> <span data-ttu-id="07b91-144">Hello d’avis » « valeur (vide) pour hello `network-security-group-id` paramètre.</span><span class="sxs-lookup"><span data-stu-id="07b91-144">Notice hello "" (empty) value for hello `network-security-group-id` parameter.</span></span> <span data-ttu-id="07b91-145">Voilà comment supprimer un groupe de sécurité réseau de tooan association.</span><span class="sxs-lookup"><span data-stu-id="07b91-145">That is how you remove an association tooan NSG.</span></span> <span data-ttu-id="07b91-146">Vous ne pouvez pas faire même hello avec hello `network-security-group-name` paramètre.</span><span class="sxs-lookup"><span data-stu-id="07b91-146">You can't do hello same with hello `network-security-group-name` parameter.</span></span>
> 

<span data-ttu-id="07b91-147">Résultat attendu :</span><span class="sxs-lookup"><span data-stu-id="07b91-147">Expected result:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="07b91-148">Dissocier un groupe de sécurité réseau d’un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="07b91-148">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="07b91-149">toodissociate hello **NSG-FrontEnd** groupe de sécurité réseau à partir de hello **frontal** sous-réseau, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07b91-149">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-id ""
```

<span data-ttu-id="07b91-150">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="07b91-150">Expected output:</span></span>

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "FrontEnd"
    + Setting subnet "FrontEnd"
    + Looking up hello subnet "FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:    Type                            : Microsoft.Network/virtualNetworks/subnets
    data:    ProvisioningState               : Succeeded
    data:    Name                            : FrontEnd
    data:    Address prefix                  : 192.168.1.0/24
    data:    IP configurations:
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
    data:
    info:    network vnet subnet set command OK

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="07b91-151">Associez un sous-réseau de tooa du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="07b91-151">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="07b91-152">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** sous-réseau exécuter à nouveau, hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07b91-152">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-name NSG-FronEnd
```

> [!NOTE]
> <span data-ttu-id="07b91-153">Hello commande ci-dessus fonctionne uniquement car hello **NSG-FrontEnd** groupe de sécurité réseau est Bonjour même groupe de ressources en tant que réseau virtuel de hello **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="07b91-153">hello command above only works because hello **NSG-FrontEnd** NSG is in hello same resource group as hello virtual network **TestVNet**.</span></span> <span data-ttu-id="07b91-154">Si hello NSG se trouve dans un autre groupe de ressources, vous devez toouse hello `--network-security-group-id` paramètre à la place et indiquez l’id complet de hello pour hello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="07b91-154">If hello NSG is in a different resource group, you need toouse hello `--network-security-group-id` parameter instead, and provide hello full id for hello NSG.</span></span> <span data-ttu-id="07b91-155">Vous pouvez récupérer l’id de hello en exécutant `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` et en recherchant hello **id** propriété.</span><span class="sxs-lookup"><span data-stu-id="07b91-155">You can retrieve hello id by running `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` and looking for hello **id** property.</span></span> 
> 

<span data-ttu-id="07b91-156">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="07b91-156">Expected output:</span></span>

        info:    Executing command network vnet subnet set
        + Looking up hello subnet "FrontEnd"
        + Looking up hello network security group "NSG-FrontEnd"
        + Setting subnet "FrontEnd"
        + Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
        data:
        info:    network vnet subnet set command OK

## <a name="delete-an-nsg"></a><span data-ttu-id="07b91-157">Suppression d'un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="07b91-157">Delete an NSG</span></span>
<span data-ttu-id="07b91-158">Vous ne pouvez supprimer un groupe de sécurité réseau si elle n’est pas associé à tooany ressource.</span><span class="sxs-lookup"><span data-stu-id="07b91-158">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="07b91-159">toodelete un groupe de sécurité réseau, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="07b91-159">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="07b91-160">ressources de hello toocheck associés tooan NSG, exécutez hello `azure network nsg show` comme indiqué dans [associations de groupes de sécurité réseau vue](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="07b91-160">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="07b91-161">Si hello NSG est associé tooany cartes réseau, exécutez hello `azure network nic set` comme indiqué dans [dissocier un groupe de sécurité réseau à partir d’une carte réseau](#Dissociate-an-NSG-from-a-NIC) pour chaque carte réseau.</span><span class="sxs-lookup"><span data-stu-id="07b91-161">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="07b91-162">Si hello NSG est associé tooany sous-réseau, exécutez hello `azure network vnet subnet set` comme indiqué dans [dissocier un groupe de sécurité réseau à partir d’un sous-réseau](#Dissociate-an-NSG-from-a-subnet) pour chaque sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="07b91-162">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="07b91-163">toodelete hello NSG, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07b91-163">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    azure network nsg delete --resource-group RG-NSG --name NSG-FrontEnd --quiet
    ```

    <span data-ttu-id="07b91-164">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="07b91-164">Expected output:</span></span>

        info:    Executing command network nsg delete
        + Looking up hello network security group "NSG-FrontEnd"
        + Deleting network security group "NSG-FrontEnd"
        info:    network nsg delete command OK

## <a name="next-steps"></a><span data-ttu-id="07b91-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="07b91-165">Next steps</span></span>
* <span data-ttu-id="07b91-166">[Activez la journalisation](virtual-network-nsg-manage-log.md) des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="07b91-166">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

