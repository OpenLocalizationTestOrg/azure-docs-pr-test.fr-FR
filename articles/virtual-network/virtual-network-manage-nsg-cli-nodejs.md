---
title: "Gérer les groupes de sécurité réseau - Azure CLI 1.0 | Microsoft Docs"
description: "Découvrez comment gérer les groupes de sécurité réseau à l’aide d’Azure CLI 1.0."
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
ms.openlocfilehash: 2e53c3ff2ffbef95d6b72ca6afb3b4de377f0389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-the-azure-cli-10"></a><span data-ttu-id="daabf-103">Gérer les groupes de sécurité réseau avec Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="daabf-103">Manage network security groups using the Azure CLI 1.0</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="daabf-104">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="daabf-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="daabf-105">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="daabf-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="daabf-106">[Azure CLI 1.0](#View-existing-NSGs) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager</span><span class="sxs-lookup"><span data-stu-id="daabf-106">[Azure CLI 1.0](#View-existing-NSGs) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="daabf-107">[Azure CLI 2.0 ](virtual-network-manage-nsg-arm-cli.md) : notre interface Azure CLI nouvelle génération pour le modèle de déploiement Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="daabf-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="daabf-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="daabf-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="daabf-109">Cet article traite de l’utilisation du modèle de déploiement Resource Manager que Microsoft recommande pour la plupart des nouveaux déploiements à la place du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="daabf-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="daabf-110">Récupérer des informations</span><span class="sxs-lookup"><span data-stu-id="daabf-110">Retrieve Information</span></span>
<span data-ttu-id="daabf-111">Vous pouvez afficher vos groupes de sécurité réseau existants, récupérer des règles pour un groupe de sécurité réseau existant et découvrir quelles sont les ressources associées à un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="daabf-111">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="daabf-112">Afficher les groupes de sécurité réseau existants</span><span class="sxs-lookup"><span data-stu-id="daabf-112">View existing NSGs</span></span>
<span data-ttu-id="daabf-113">Pour afficher la liste des groupes de sécurité réseau dans un groupe de ressources spécifique, exécutez la commande `azure network nsg list` , comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="daabf-113">To view the list of NSGs in a specific resource group, run the `azure network nsg list` command as shown below.</span></span>

```azurecli
azure network nsg list --resource-group RG-NSG
```

<span data-ttu-id="daabf-114">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="daabf-114">Expected output:</span></span>

    info:    Executing command network nsg list
    + Getting the network security groups
    data:    Name          Location
    data:    ------------  --------
    data:    NSG-BackEnd   westus
    data:    NSG-FrontEnd  westus
    info:    network nsg list command OK

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="daabf-115">Répertorier toutes les règles pour un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="daabf-115">List all rules for an NSG</span></span>
<span data-ttu-id="daabf-116">Pour afficher les règles d’un groupe de sécurité réseau nommé **NSG-FrontEnd**, exécutez la commande `azure network nsg show`, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="daabf-116">To view the rules of an NSG named **NSG-FrontEnd**, run the `azure network nsg show` command as shown below.</span></span> 

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd
```

<span data-ttu-id="daabf-117">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="daabf-117">Expected output:</span></span>

    info:    Executing command network nsg show
    + Looking up the network security group "NSG-FrontEnd"
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
> <span data-ttu-id="daabf-118">Vous pouvez aussi utiliser `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` pour répertorier les règles du groupe de sécurité réseau **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="daabf-118">You can also use `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` to list the rules from the **NSG-FrontEnd** NSG.</span></span>
>

### <a name="view-nsg-associations"></a><span data-ttu-id="daabf-119">Afficher les associations de groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="daabf-119">View NSG associations</span></span>

<span data-ttu-id="daabf-120">Pour afficher les ressources associées au groupe de sécurité réseau **NSG-FrontEnd**, exécutez la commande `azure network nsg show`, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="daabf-120">To view what resources the **NSG-FrontEnd** NSG is associate with, run the `azure network nsg show` command as shown below.</span></span> <span data-ttu-id="daabf-121">Notez que la seule différence est l’utilisation du paramètre **--json** .</span><span class="sxs-lookup"><span data-stu-id="daabf-121">Notice that the only difference is the use of the **--json** parameter.</span></span>

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json
```

<span data-ttu-id="daabf-122">Recherchez les propriétés **networkInterfaces** et **subnets**, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="daabf-122">Look for the **networkInterfaces** and **subnets** properties as shown below:</span></span>

    "networkInterfaces": [],
    ...
    "subnets": [
        {
            "id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
        }
    ],
    ...

<span data-ttu-id="daabf-123">Dans l’exemple ci-dessus, le groupe de sécurité réseau n’est associé à aucune interface réseau, mais à un sous-réseau nommé **FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="daabf-123">In the example above, the NSG is not associated to any network interfaces (NICs), and it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="daabf-124">Gérer les règles</span><span class="sxs-lookup"><span data-stu-id="daabf-124">Manage rules</span></span>
<span data-ttu-id="daabf-125">Vous pouvez ajouter des règles à un groupe de sécurité réseau existant, modifier des règles existantes et supprimer des règles.</span><span class="sxs-lookup"><span data-stu-id="daabf-125">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="daabf-126">Ajouter une règle</span><span class="sxs-lookup"><span data-stu-id="daabf-126">Add a rule</span></span>
<span data-ttu-id="daabf-127">Pour ajouter une règle autorisant le trafic **entrant** sur le port **443** d’une machine vers le groupe de sécurité réseau **NSG-FrontEnd**, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="daabf-127">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, enter the following command:</span></span>

```azurecli
azure network nsg rule create --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --description "Allow access to port 443 for HTTPS" \
    --protocol Tcp \
    --source-address-prefix * \
    --source-port-range * \
    --destination-address-prefix * \
    --destination-port-range 443 \
    --access Allow \
    --priority 102 \
    --direction Inbound
```

<span data-ttu-id="daabf-128">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="daabf-128">Expected output:</span></span>

    info:    Executing command network nsg rule create
    + Looking up the network security rule "allow-https"
    + Creating a network security rule "allow-https"
    + Looking up the network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access to port 443 for HTTPS
    data:    Source IP                       : *
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule create command OK

### <a name="change-a-rule"></a><span data-ttu-id="daabf-129">Modifier une règle</span><span class="sxs-lookup"><span data-stu-id="daabf-129">Change a rule</span></span>
<span data-ttu-id="daabf-130">Pour modifier la règle créée précédemment pour autoriser le trafic entrant en provenance d’**Internet** uniquement, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="daabf-130">To change the rule created above to allow inbound traffic from the **Internet** only, run the following command:</span></span>

```azurecli
azure network nsg rule set --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --source-address-prefix Internet
```

<span data-ttu-id="daabf-131">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="daabf-131">Expected output:</span></span>

    info:    Executing command network nsg rule set
    + Looking up the network security group "NSG-FrontEnd"
    + Setting a network security rule "allow-https"
    + Looking up the network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access to port 443 for HTTPS
    data:    Source IP                       : Internet
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule set command OK

### <a name="delete-a-rule"></a><span data-ttu-id="daabf-132">Supprimer une règle</span><span class="sxs-lookup"><span data-stu-id="daabf-132">Delete a rule</span></span>
<span data-ttu-id="daabf-133">Pour supprimer la règle créée précédemment, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="daabf-133">To delete the rule created above, run the following command:</span></span>

```azurecli
azure network nsg rule delete --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --quiet
```

> [!NOTE]
> <span data-ttu-id="daabf-134">Le paramètre `--quiet` garantit que vous n’avez pas besoin de confirmer la suppression.</span><span class="sxs-lookup"><span data-stu-id="daabf-134">The `--quiet` parameter ensures you don't need to confirm the deletion.</span></span>
>

<span data-ttu-id="daabf-135">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="daabf-135">Expected output:</span></span>

    info:    Executing command network nsg rule delete
    + Looking up the network security group "NSG-FrontEnd"
    + Deleting network security rule "allow-https"
    info:    network nsg rule delete command OK

## <a name="manage-associations"></a><span data-ttu-id="daabf-136">Gérer les associations</span><span class="sxs-lookup"><span data-stu-id="daabf-136">Manage associations</span></span>
<span data-ttu-id="daabf-137">Vous pouvez associer un groupe de sécurité réseau à des cartes réseau et des sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="daabf-137">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="daabf-138">Vous pouvez également dissocier un groupe de sécurité réseau de n’importe quelle ressource à laquelle il est associé.</span><span class="sxs-lookup"><span data-stu-id="daabf-138">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="daabf-139">Associer un groupe de sécurité réseau à une carte réseau</span><span class="sxs-lookup"><span data-stu-id="daabf-139">Associate an NSG to a NIC</span></span>
<span data-ttu-id="daabf-140">Pour associer le groupe de sécurité réseau **NSG-FrontEnd** à la carte réseau **TestNICWeb1**, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="daabf-140">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, run the following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG \
    --name TestNICWeb1 \
    --network-security-group-name NSG-FrontEnd
```

<span data-ttu-id="daabf-141">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="daabf-141">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up the network interface "TestNICWeb1"
    + Looking up the network security group "NSG-FrontEnd"
    + Updating network interface "TestNICWeb1"
    + Looking up the network interface "TestNICWeb1"
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

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="daabf-142">Dissocier un groupe de sécurité réseau d’une carte réseau</span><span class="sxs-lookup"><span data-stu-id="daabf-142">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="daabf-143">Pour dissocier le groupe de sécurité réseau **NSG-FrontEnd** de la carte réseau **TestNICWeb1**, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="daabf-143">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, run the following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG --name TestNICWeb1 --network-security-group-id ""
```

> [!NOTE]
> <span data-ttu-id="daabf-144">Notez que le paramètre `network-security-group-id` a la valeur "" (vide).</span><span class="sxs-lookup"><span data-stu-id="daabf-144">Notice the "" (empty) value for the `network-security-group-id` parameter.</span></span> <span data-ttu-id="daabf-145">Voilà comment supprimer une association d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="daabf-145">That is how you remove an association to an NSG.</span></span> <span data-ttu-id="daabf-146">Vous ne pouvez pas faire la même chose avec le paramètre `network-security-group-name`.</span><span class="sxs-lookup"><span data-stu-id="daabf-146">You can't do the same with the `network-security-group-name` parameter.</span></span>
> 

<span data-ttu-id="daabf-147">Résultat attendu :</span><span class="sxs-lookup"><span data-stu-id="daabf-147">Expected result:</span></span>

    info:    Executing command network nic set
    + Looking up the network interface "TestNICWeb1"
    + Updating network interface "TestNICWeb1"
    + Looking up the network interface "TestNICWeb1"
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

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="daabf-148">Dissocier un groupe de sécurité réseau d’un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="daabf-148">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="daabf-149">Pour dissocier le groupe de sécurité réseau **NSG-FrontEnd** du sous-réseau **FrontEnd**, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="daabf-149">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, run the following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-id ""
```

<span data-ttu-id="daabf-150">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="daabf-150">Expected output:</span></span>

    info:    Executing command network vnet subnet set
    + Looking up the subnet "FrontEnd"
    + Setting subnet "FrontEnd"
    + Looking up the subnet "FrontEnd"
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

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="daabf-151">Association d’un groupe de sécurité réseau à un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="daabf-151">Associate an NSG to a subnet</span></span>
<span data-ttu-id="daabf-152">Pour associer à nouveau le groupe de sécurité réseau **NSG-FrontEnd** au sous-réseau **FrontEnd**, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="daabf-152">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, run the following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-name NSG-FronEnd
```

> [!NOTE]
> <span data-ttu-id="daabf-153">La commande ci-dessus fonctionne uniquement parce que le groupe de sécurité réseau **NSG-FrontEnd** est dans le même groupe de ressources que le réseau virtuel **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="daabf-153">The command above only works because the **NSG-FrontEnd** NSG is in the same resource group as the virtual network **TestVNet**.</span></span> <span data-ttu-id="daabf-154">Si le groupe de sécurité réseau se trouve dans un autre groupe de ressources, vous devez utiliser le paramètre `--network-security-group-id` à la place et indiquer l’ID complet du groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="daabf-154">If the NSG is in a different resource group, you need to use the `--network-security-group-id` parameter instead, and provide the full id for the NSG.</span></span> <span data-ttu-id="daabf-155">Vous pouvez récupérer l’ID en exécutant `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` et en recherchant la propriété **id**.</span><span class="sxs-lookup"><span data-stu-id="daabf-155">You can retrieve the id by running `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` and looking for the **id** property.</span></span> 
> 

<span data-ttu-id="daabf-156">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="daabf-156">Expected output:</span></span>

        info:    Executing command network vnet subnet set
        + Looking up the subnet "FrontEnd"
        + Looking up the network security group "NSG-FrontEnd"
        + Setting subnet "FrontEnd"
        + Looking up the subnet "FrontEnd"
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

## <a name="delete-an-nsg"></a><span data-ttu-id="daabf-157">Suppression d'un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="daabf-157">Delete an NSG</span></span>
<span data-ttu-id="daabf-158">Vous ne pouvez supprimer un groupe de sécurité réseau que s’il n’est associé à aucune ressource.</span><span class="sxs-lookup"><span data-stu-id="daabf-158">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="daabf-159">Pour supprimer un groupe de sécurité réseau, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="daabf-159">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="daabf-160">Pour consulter les ressources associées à un groupe de sécurité réseau, exécutez `azure network nsg show` comme illustré dans [Afficher les associations de groupes de sécurité réseau](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="daabf-160">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="daabf-161">Si le groupe de sécurité réseau est associé à des cartes réseau, exécutez `azure network nic set` comme illustré dans [Dissocier un groupe de sécurité réseau d’une carte réseau](#Dissociate-an-NSG-from-a-NIC) pour chaque carte réseau.</span><span class="sxs-lookup"><span data-stu-id="daabf-161">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="daabf-162">Si le groupe de sécurité réseau est associé à un sous-réseau, exécutez `azure network vnet subnet set` comme illustré dans [Dissocier un groupe de sécurité réseau d’un sous-réseau](#Dissociate-an-NSG-from-a-subnet) pour chaque sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="daabf-162">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="daabf-163">Pour supprimer le groupe de sécurité réseau, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="daabf-163">To delete the NSG, run the following command:</span></span>

    ```azurecli
    azure network nsg delete --resource-group RG-NSG --name NSG-FrontEnd --quiet
    ```

    <span data-ttu-id="daabf-164">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="daabf-164">Expected output:</span></span>

        info:    Executing command network nsg delete
        + Looking up the network security group "NSG-FrontEnd"
        + Deleting network security group "NSG-FrontEnd"
        info:    network nsg delete command OK

## <a name="next-steps"></a><span data-ttu-id="daabf-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="daabf-165">Next steps</span></span>
* <span data-ttu-id="daabf-166">[Activez la journalisation](virtual-network-nsg-manage-log.md) des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="daabf-166">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

