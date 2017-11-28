---
title: "aaaControl équipements virtuels et de routage à l’aide de hello Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment toocontrol équipements virtuels et de routage à l’aide de hello Azure CLI 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 1c8a552d949521fa554880c00405e65fa47a8162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-10"></a><span data-ttu-id="76ef4-103">Créer des itinéraires définis par l’utilisateur (UDR) à l’aide de hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="76ef4-103">Create User-Defined Routes (UDR) using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="76ef4-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="76ef4-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="76ef4-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="76ef4-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="76ef4-106">Modèle</span><span class="sxs-lookup"><span data-stu-id="76ef4-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="76ef4-107">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="76ef4-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="76ef4-108">Interface de ligne de commande (classique)</span><span class="sxs-lookup"><span data-stu-id="76ef4-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="76ef4-109">Créer un routage personnalisé et des équipements virtuels à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="76ef4-109">Create custom routing and virtual appliances using hello Azure CLI.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="76ef4-110">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="76ef4-110">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="76ef4-111">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="76ef4-111">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="76ef4-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="76ef4-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="76ef4-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="76ef4-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="76ef4-114">commandes de CLI d’Azure Hello exemple ci-dessous s’attendre à un environnement simple déjà créé en fonction de scénario hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="76ef4-114">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="76ef4-115">Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, tout d’abord créer des environnement de test hello en déployant [ce modèle](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), cliquez sur **déployer tooAzure**, remplacez les valeurs de paramètre par défaut hello Si nécessaire et suivez les instructions hello dans hello portal.</span><span class="sxs-lookup"><span data-stu-id="76ef4-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="76ef4-116">Créer hello UDR pour le sous-réseau frontal de hello</span><span class="sxs-lookup"><span data-stu-id="76ef4-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="76ef4-117">table d’itinéraires toocreate hello et d’itinéraire nécessaire pour le sous-réseau frontal de hello selon le scénario de hello ci-dessus, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="76ef4-117">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="76ef4-118">Exécutez hello suivant commande toocreate une table d’itinéraires pour le sous-réseau frontal de hello :</span><span class="sxs-lookup"><span data-stu-id="76ef4-118">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="76ef4-119">Output:</span><span class="sxs-lookup"><span data-stu-id="76ef4-119">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    <span data-ttu-id="76ef4-120">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="76ef4-120">Parameters:</span></span>
   
   * <span data-ttu-id="76ef4-121">**-g (ou --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="76ef4-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="76ef4-122">Nom du groupe de ressources hello où hello UDR sera créé.</span><span class="sxs-lookup"><span data-stu-id="76ef4-122">Name of hello resource group where hello UDR will be created.</span></span> <span data-ttu-id="76ef4-123">Pour notre scénario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="76ef4-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="76ef4-124">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="76ef4-124">**-l (or --location)**.</span></span> <span data-ttu-id="76ef4-125">Région Azure où hello UDR nouvelle sera créée.</span><span class="sxs-lookup"><span data-stu-id="76ef4-125">Azure region where hello new UDR will be created.</span></span> <span data-ttu-id="76ef4-126">Pour notre scénario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="76ef4-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="76ef4-127">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="76ef4-127">**-n (or --name)**.</span></span> <span data-ttu-id="76ef4-128">Nom de hello UDR de nouveau.</span><span class="sxs-lookup"><span data-stu-id="76ef4-128">Name for hello new UDR.</span></span> <span data-ttu-id="76ef4-129">Pour notre scénario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="76ef4-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="76ef4-130">Exécutez hello suivant commande toocreate un itinéraire dans hello itinéraire table toosend tout le trafic destiné toohello le sous-réseau principal (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) :</span><span class="sxs-lookup"><span data-stu-id="76ef4-130">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="76ef4-131">Output:</span><span class="sxs-lookup"><span data-stu-id="76ef4-131">Output:</span></span>
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    <span data-ttu-id="76ef4-132">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="76ef4-132">Parameters:</span></span>
   
   * <span data-ttu-id="76ef4-133">**-r (ou --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="76ef4-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="76ef4-134">Nom de la table d’itinéraires hello où itinéraire de hello sera ajouté.</span><span class="sxs-lookup"><span data-stu-id="76ef4-134">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="76ef4-135">Pour notre scénario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="76ef4-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="76ef4-136">**-a (ou --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="76ef4-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="76ef4-137">Préfixe d’adresse de sous-réseau hello où les paquets sont destinés à.</span><span class="sxs-lookup"><span data-stu-id="76ef4-137">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="76ef4-138">Pour notre scénario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="76ef4-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="76ef4-139">**-y (ou --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="76ef4-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="76ef4-140">Type d'objet vers lequel le trafic sera envoyé.</span><span class="sxs-lookup"><span data-stu-id="76ef4-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="76ef4-141">Les valeurs possibles sont *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* ou *None*.</span><span class="sxs-lookup"><span data-stu-id="76ef4-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="76ef4-142">**-p (ou --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="76ef4-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="76ef4-143">Adresse IP de saut suivant.</span><span class="sxs-lookup"><span data-stu-id="76ef4-143">IP address for next hop.</span></span> <span data-ttu-id="76ef4-144">Pour notre scénario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="76ef4-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="76ef4-145">Table d’itinéraires hello tooassociate créé ci-dessus hello de commandes suivante d’exécution hello **frontal** sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="76ef4-145">Run hello following command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="76ef4-146">Output:</span><span class="sxs-lookup"><span data-stu-id="76ef4-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    <span data-ttu-id="76ef4-147">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="76ef4-147">Parameters:</span></span>
   
   * <span data-ttu-id="76ef4-148">**-e (ou --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="76ef4-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="76ef4-149">Nom de réseau virtuel où se trouve le sous-réseau de hello de hello.</span><span class="sxs-lookup"><span data-stu-id="76ef4-149">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="76ef4-150">Pour notre scénario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="76ef4-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="76ef4-151">Créer hello UDR pour le sous-réseau principal de hello</span><span class="sxs-lookup"><span data-stu-id="76ef4-151">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="76ef4-152">toocreate hello table d’itinéraires et Router nécessaires pour le sous-réseau principal de hello selon le scénario hello ci-dessus, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="76ef4-152">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="76ef4-153">Exécutez hello suivant commande toocreate une table d’itinéraires pour le sous-réseau principal de hello :</span><span class="sxs-lookup"><span data-stu-id="76ef4-153">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="76ef4-154">Exécutez hello suivant commande toocreate un itinéraire dans hello itinéraire table toosend tout le trafic destiné toohello sous-réseau frontal (192.168.1.0/24) toohello **FW1** VM (192.168.0.4) :</span><span class="sxs-lookup"><span data-stu-id="76ef4-154">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="76ef4-155">Exécution hello suivant tooassociate commande hello une table d’itinéraires par hello **principal** sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="76ef4-155">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="76ef4-156">Activer le transfert IP sur FW1</span><span class="sxs-lookup"><span data-stu-id="76ef4-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="76ef4-157">le transfert IP tooenable Bonjour carte réseau utilisée par **FW1**complète hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="76ef4-157">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="76ef4-158">Exécutez la commande hello qui suit et notez la valeur hello pour **transfert activer une IP**.</span><span class="sxs-lookup"><span data-stu-id="76ef4-158">Run hello command that follows and notice hello value for **Enable IP forwarding**.</span></span> <span data-ttu-id="76ef4-159">Il doit être défini trop*false*.</span><span class="sxs-lookup"><span data-stu-id="76ef4-159">It should be set too*false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="76ef4-160">Output:</span><span class="sxs-lookup"><span data-stu-id="76ef4-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. <span data-ttu-id="76ef4-161">Exécutez hello après le transfert IP commande tooenable :</span><span class="sxs-lookup"><span data-stu-id="76ef4-161">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="76ef4-162">Output:</span><span class="sxs-lookup"><span data-stu-id="76ef4-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up hello network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    <span data-ttu-id="76ef4-163">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="76ef4-163">Parameters:</span></span>
   
   * <span data-ttu-id="76ef4-164">**-f (ou --enable-ip-forwarding)**.</span><span class="sxs-lookup"><span data-stu-id="76ef4-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="76ef4-165">*true* ou *false*.</span><span class="sxs-lookup"><span data-stu-id="76ef4-165">*true* or *false*.</span></span>

