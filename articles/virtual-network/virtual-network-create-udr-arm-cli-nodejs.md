---
title: "Contrôler le routage et les appliances virtuelles à l’aide d’Azure CLI 1.0 | Microsoft Docs"
description: "Apprenez à contrôler le routage et des appliances virtuelles à l’aide d’Azure CLI 1.0."
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
ms.openlocfilehash: 5f21bc7a4fcd9507ea9d6b2b752a2328a7b834f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-user-defined-routes-udr-using-the-azure-cli-10"></a><span data-ttu-id="fb7bc-103">Créer des routages définis par l’utilisateur à l’aide d’Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="fb7bc-103">Create User-Defined Routes (UDR) using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb7bc-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb7bc-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="fb7bc-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="fb7bc-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="fb7bc-106">Modèle</span><span class="sxs-lookup"><span data-stu-id="fb7bc-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="fb7bc-107">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="fb7bc-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="fb7bc-108">Interface de ligne de commande (classique)</span><span class="sxs-lookup"><span data-stu-id="fb7bc-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="fb7bc-109">Créez un routage personnalisé et des appliances virtuelles à l’aide d’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-109">Create custom routing and virtual appliances using the Azure CLI.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="fb7bc-110">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="fb7bc-110">CLI versions to complete the task</span></span> 

<span data-ttu-id="fb7bc-111">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="fb7bc-111">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="fb7bc-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="fb7bc-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="fb7bc-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) : notre interface de ligne de commande nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fb7bc-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for the resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="fb7bc-114">Les exemples de commandes d’interface de ligne de commande PowerShell ci-dessous supposent qu’un environnement simple a déjà été créé conformément au scénario décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-114">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="fb7bc-115">Si vous souhaitez exécuter les commandes telles qu’elles sont présentées dans ce document, commencez par créer l’environnement de test en déployant [ce modèle](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), cliquez sur **Déployer dans Azure**, remplacez les valeurs des paramètres par défaut si nécessaire, puis suivez les instructions dans le portail.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-115">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>


## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="fb7bc-116">Création de routages définis par l’utilisateur pour le sous-réseau frontal</span><span class="sxs-lookup"><span data-stu-id="fb7bc-116">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="fb7bc-117">Pour créer la table de routage et l'itinéraire nécessaires pour le sous-réseau frontal selon le scénario ci-dessus, suivez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-117">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="fb7bc-118">Exécutez la commande suivante pour créer une table de routage pour le sous-réseau frontal :</span><span class="sxs-lookup"><span data-stu-id="fb7bc-118">Run the following command to create a route table for the front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="fb7bc-119">Output:</span><span class="sxs-lookup"><span data-stu-id="fb7bc-119">Output:</span></span>
   
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
   
    <span data-ttu-id="fb7bc-120">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="fb7bc-120">Parameters:</span></span>
   
   * <span data-ttu-id="fb7bc-121">**-g (ou --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="fb7bc-122">Nom du groupe de ressources dans lequel sera créé l’itinéraire défini par l’utilisateur (UDR).</span><span class="sxs-lookup"><span data-stu-id="fb7bc-122">Name of the resource group where the UDR will be created.</span></span> <span data-ttu-id="fb7bc-123">Pour notre scénario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="fb7bc-124">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-124">**-l (or --location)**.</span></span> <span data-ttu-id="fb7bc-125">Région Azure dans laquelle l’itinéraire défini par l’utilisateur (UDR) sera créé.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-125">Azure region where the new UDR will be created.</span></span> <span data-ttu-id="fb7bc-126">Pour notre scénario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="fb7bc-127">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-127">**-n (or --name)**.</span></span> <span data-ttu-id="fb7bc-128">Nom du nouvel itinéraire défini par l’utilisateur (UDR).</span><span class="sxs-lookup"><span data-stu-id="fb7bc-128">Name for the new UDR.</span></span> <span data-ttu-id="fb7bc-129">Pour notre scénario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="fb7bc-130">Exécutez la commande suivante pour créer un routage dans la table de routage pour envoyer tout le trafic destiné au sous-réseau Backend (192.168.2.0/24) à la machine virtuelle **FW1** (192.168.0.4) :</span><span class="sxs-lookup"><span data-stu-id="fb7bc-130">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="fb7bc-131">Output:</span><span class="sxs-lookup"><span data-stu-id="fb7bc-131">Output:</span></span>
   
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
   
    <span data-ttu-id="fb7bc-132">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="fb7bc-132">Parameters:</span></span>
   
   * <span data-ttu-id="fb7bc-133">**-r (ou --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="fb7bc-134">Nom de la table de routage où l'itinéraire sera ajouté.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-134">Name of the route table where the route will be added.</span></span> <span data-ttu-id="fb7bc-135">Pour notre scénario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="fb7bc-136">**-a (ou --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="fb7bc-137">Préfixe d'adresse pour le sous-réseau auquel les paquets sont destinés.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-137">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="fb7bc-138">Pour notre scénario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="fb7bc-139">**-y (ou --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="fb7bc-140">Type d'objet vers lequel le trafic sera envoyé.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="fb7bc-141">Les valeurs possibles sont *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* ou *None*.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="fb7bc-142">**-p (ou --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="fb7bc-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="fb7bc-143">Adresse IP de saut suivant.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-143">IP address for next hop.</span></span> <span data-ttu-id="fb7bc-144">Pour notre scénario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="fb7bc-145">Exécutez la commande suivante pour associer la table de routage créée ci-dessus au sous-réseau **FrontEnd** :</span><span class="sxs-lookup"><span data-stu-id="fb7bc-145">Run the following command to associate the route table created above with the **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="fb7bc-146">Output:</span><span class="sxs-lookup"><span data-stu-id="fb7bc-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
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
   
    <span data-ttu-id="fb7bc-147">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="fb7bc-147">Parameters:</span></span>
   
   * <span data-ttu-id="fb7bc-148">**-e (ou --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="fb7bc-149">Nom du réseau virtuel où le sous-réseau est situé.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-149">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="fb7bc-150">Pour notre scénario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="fb7bc-151">Créer l’itinéraire défini par l’utilisateur pour le sous-réseau principal</span><span class="sxs-lookup"><span data-stu-id="fb7bc-151">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="fb7bc-152">Pour créer la table de routage et l’itinéraire nécessaires pour le sous-réseau Backend selon le scénario ci-dessus, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="fb7bc-152">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="fb7bc-153">Exécutez la commande suivante pour créer une table d’itinéraires pour le sous-réseau principal :</span><span class="sxs-lookup"><span data-stu-id="fb7bc-153">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="fb7bc-154">Exécutez la commande suivante pour créer un itinéraire dans la table d’itinéraires pour envoyer tout le trafic destiné au sous-réseau frontal (192.168.1.0/24) à la machine virtuelle **FW1** (192.168.0.4) :</span><span class="sxs-lookup"><span data-stu-id="fb7bc-154">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="fb7bc-155">Exécutez la commande suivante pour associer la table de routage créée ci-dessus au sous-réseau **Backend** :</span><span class="sxs-lookup"><span data-stu-id="fb7bc-155">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="fb7bc-156">Activer le transfert IP sur FW1</span><span class="sxs-lookup"><span data-stu-id="fb7bc-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="fb7bc-157">Pour activer le transfert IP sur la carte réseau utilisée par **FW1**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fb7bc-157">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span></span>

1. <span data-ttu-id="fb7bc-158">Exécutez la commande suivante et notez la valeur attribuée à **Activer le transfert IP**.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-158">Run the command that follows and notice the value for **Enable IP forwarding**.</span></span> <span data-ttu-id="fb7bc-159">Cette option doit avoir la valeur *false*.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-159">It should be set to *false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="fb7bc-160">Output:</span><span class="sxs-lookup"><span data-stu-id="fb7bc-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up the network interface "NICFW1"
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
2. <span data-ttu-id="fb7bc-161">Exécutez la commande suivante pour activer le transfert IP :</span><span class="sxs-lookup"><span data-stu-id="fb7bc-161">Run the following command to enable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="fb7bc-162">Output:</span><span class="sxs-lookup"><span data-stu-id="fb7bc-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up the network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up the network interface "NICFW1"
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
   
    <span data-ttu-id="fb7bc-163">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="fb7bc-163">Parameters:</span></span>
   
   * <span data-ttu-id="fb7bc-164">**-f (ou --enable-ip-forwarding)**.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="fb7bc-165">*true* ou *false*.</span><span class="sxs-lookup"><span data-stu-id="fb7bc-165">*true* or *false*.</span></span>

