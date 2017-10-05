---
title: "Configurer des adresses IP privées pour les machines virtuelles - Azure CLI 1.0 | Microsoft Docs"
description: "Apprenez à configurer des adresses IP privées pour les machines virtuelles à l’aide de l’interface Azure CLI 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9179319095c31d5eb454860e173ffa7c65fc9f73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-cli-10"></a><span data-ttu-id="bb503-103">Configurer des adresses IP privées pour une machine virtuelle à l’aide de l’interface Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bb503-103">Configure private IP addresses for a virtual machine using the Azure CLI 1.0</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="bb503-104">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="bb503-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="bb503-105">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="bb503-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="bb503-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="bb503-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="bb503-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) : notre interface Azure CLI nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bb503-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) - our next-generation CLI for the resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="bb503-108">Cet article traite du modèle de déploiement de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bb503-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="bb503-109">Vous pouvez également [gérer une adresse IP privée statique dans le modèle de déploiement classique](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bb503-109">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="bb503-110">Les commandes d’interface de ligne de commande Azure attendent un environnement simple déjà créé.</span><span class="sxs-lookup"><span data-stu-id="bb503-110">The sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="bb503-111">Si vous souhaitez exécuter les commandes telles qu’elles sont présentées dans ce document, commencez par créer l’environnement de test décrit dans [Créer un réseau virtuel](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bb503-111">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="how-to-specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="bb503-112">Comment spécifier une adresse IP privée statique lors de la création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bb503-112">How to specify a static private IP address when creating a VM</span></span>
<span data-ttu-id="bb503-113">Pour créer une machine virtuelle nommée *DNS01* dans le sous-réseau *FrontEnd* d’un réseau virtuel nommé *TestVNet* avec l’adresse IP privée statique *192.168.1.101*, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bb503-113">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="bb503-114">Si vous n’avez jamais utilisé l’interface de ligne de commande Azure, consultez [Installer et configurer l’interface de ligne de commande Azure](../cli-install-nodejs.md) et suivez les instructions jusqu’à l’étape où vous sélectionnez votre compte et votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="bb503-114">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="bb503-115">Exécutez la commande **azure config mode** pour passer en mode Resource Manager, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bb503-115">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="bb503-116">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="bb503-116">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="bb503-117">Exécutez la commande **azure network public-ip create** pour créer une adresse IP publique de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bb503-117">Run the **azure network public-ip create** to create a public IP for the VM.</span></span> <span data-ttu-id="bb503-118">La liste affichée après le résultat présente les différents paramètres utilisés.</span><span class="sxs-lookup"><span data-stu-id="bb503-118">The list shown after the output explains the parameters used.</span></span>
   
        azure network public-ip create -g TestRG -n TestPIP -l centralus
   
    <span data-ttu-id="bb503-119">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="bb503-119">Expected output:</span></span>
   
        info:    Executing command network public-ip create
        + Looking up the public ip "TestPIP"
        + Creating public ip address "TestPIP"
        + Looking up the public ip "TestPIP"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP
        data:    Name                            : TestPIP
        data:    Type                            : Microsoft.Network/publicIPAddresses
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Allocation method               : Dynamic
        data:    Idle timeout                    : 4
        info:    network public-ip create command OK
   
   * <span data-ttu-id="bb503-120">**-g (ou --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="bb503-120">**-g (or --resource-group)**.</span></span> <span data-ttu-id="bb503-121">Nom du groupe de ressources dans l’IP public, lequel sera créé le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="bb503-121">Name of the resource group the public IP will be created in.</span></span>
   * <span data-ttu-id="bb503-122">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="bb503-122">**-n (or --name)**.</span></span> <span data-ttu-id="bb503-123">Nom de l’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="bb503-123">Name of the public IP.</span></span>
   * <span data-ttu-id="bb503-124">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="bb503-124">**-l (or --location)**.</span></span> <span data-ttu-id="bb503-125">Région Azure où le réseau virtuel doit être créé.</span><span class="sxs-lookup"><span data-stu-id="bb503-125">Azure region where the public IP will be created.</span></span> <span data-ttu-id="bb503-126">Pour notre scénario, *centralus*.</span><span class="sxs-lookup"><span data-stu-id="bb503-126">For our scenario, *centralus*.</span></span>
4. <span data-ttu-id="bb503-127">Exécutez la commande **azure network nic create** pour créer une carte réseau avec une adresse IP privée statique.</span><span class="sxs-lookup"><span data-stu-id="bb503-127">Run the **azure network nic create** command to create a NIC with a static private IP.</span></span> <span data-ttu-id="bb503-128">La liste affichée après le résultat présente les différents paramètres utilisés.</span><span class="sxs-lookup"><span data-stu-id="bb503-128">The list shown after the output explains the parameters used.</span></span>
   
        azure network nic create -g TestRG -n TestNIC -l centralus -a 192.168.1.101 -m TestVNet -k FrontEnd
   
    <span data-ttu-id="bb503-129">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="bb503-129">Expected output:</span></span>
   
        + Looking up the network interface "TestNIC"
        + Looking up the subnet "FrontEnd"
        + Creating network interface "TestNIC"
        + Looking up the network interface "TestNIC"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
        data:    Name                            : TestNIC
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.101
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
   
   * <span data-ttu-id="bb503-130">**-a (or --private-ip-address)**.</span><span class="sxs-lookup"><span data-stu-id="bb503-130">**-a (or --private-ip-address)**.</span></span> <span data-ttu-id="bb503-131">Adresse IP privée statique pour la carte réseau.</span><span class="sxs-lookup"><span data-stu-id="bb503-131">Static private IP address for the NIC.</span></span>
   * <span data-ttu-id="bb503-132">**-m (or --subnet-vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="bb503-132">**-m (or --subnet-vnet-name)**.</span></span> <span data-ttu-id="bb503-133">Nom du réseauVNet où sera créé le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="bb503-133">Name of the VNet where the NIC will be created.</span></span>
   * <span data-ttu-id="bb503-134">**-k (or --subnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="bb503-134">**-k (or --subnet-name)**.</span></span> <span data-ttu-id="bb503-135">Nom du réseau virtuel où sera créé le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="bb503-135">Name of the subnet where the NIC will be created.</span></span>
5. <span data-ttu-id="bb503-136">Exécutez la commande **azure vm create** pour créer la machine virtuelle à l’aide de l’adresse IP publique et la carte réseau créées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="bb503-136">Run the **azure vm create** command to create the VM using the public IP and NIC created above.</span></span> <span data-ttu-id="bb503-137">La liste affichée après le résultat présente les différents paramètres utilisés.</span><span class="sxs-lookup"><span data-stu-id="bb503-137">The list shown after the output explains the parameters used.</span></span>
   
        azure vm create -g TestRG -n DNS01 -l centralus -y Windows -f TestNIC -i TestPIP -F TestVNet -j FrontEnd -o vnetstorage -q bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 -u adminuser -p AdminP@ssw0rd
   
    <span data-ttu-id="bb503-138">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="bb503-138">Expected output:</span></span>
   
        info:    Executing command vm create
        + Looking up the VM "DNS01"
        info:    Using the VM Size "Standard_A1"
        warn:    The image "bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2" will be used for VM
        info:    The [OS, Data] Disk or image configuration requires storage account
        + Looking up the storage account vnetstorage
        + Looking up the NIC "TestNIC"
        info:    Found an existing NIC "TestNIC"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd" in the NIC "TestNIC"
        info:    Found public ip parameters, trying to setup PublicIP profile
        + Looking up the public ip "TestPIP"
        info:    Found an existing PublicIP "TestPIP"
        info:    Configuring identified NIC IP configuration with PublicIP "TestPIP"
        + Updating NIC "TestNIC"
        + Looking up the NIC "TestNIC"
        + Creating VM "DNS01"
        info:    vm create command OK
   
   * <span data-ttu-id="bb503-139">**-y (ou type de système d’exploitation--)**.</span><span class="sxs-lookup"><span data-stu-id="bb503-139">**-y (or --os-type)**.</span></span> <span data-ttu-id="bb503-140">Type de système d’exploitation pour la machine virtuelle, soit *Windows*, soit *Linux*.</span><span class="sxs-lookup"><span data-stu-id="bb503-140">Type of operating system for the VM, either *Windows* or *Linux*.</span></span>
   * <span data-ttu-id="bb503-141">**-f (ou nom de la carte réseau--)**.</span><span class="sxs-lookup"><span data-stu-id="bb503-141">**-f (or --nic-name)**.</span></span> <span data-ttu-id="bb503-142">Nom de la carte réseau que la machine virtuelle utilisera.</span><span class="sxs-lookup"><span data-stu-id="bb503-142">Name of the NIC the VM will use.</span></span>
   * <span data-ttu-id="bb503-143">**-i (ou --nom ip public)**.</span><span class="sxs-lookup"><span data-stu-id="bb503-143">**-i (or --public-ip-name)**.</span></span> <span data-ttu-id="bb503-144">Nom de l’adresse IP publique que la machine virtuelle utilisera.</span><span class="sxs-lookup"><span data-stu-id="bb503-144">Name of the public IP the VM will use.</span></span>
   * <span data-ttu-id="bb503-145">**-F (ou --nom vnet)**.</span><span class="sxs-lookup"><span data-stu-id="bb503-145">**-F (or --vnet-name)**.</span></span> <span data-ttu-id="bb503-146">Nom du réseauVNet où sera créée la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bb503-146">Name of the VNet where the VM will be created.</span></span>
   * <span data-ttu-id="bb503-147">**-j (or --vnet-subnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="bb503-147">**-j (or --vnet-subnet-name)**.</span></span> <span data-ttu-id="bb503-148">Nom du sous-réseau où sera créée la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bb503-148">Name of the subnet where the VM will be created.</span></span>

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="bb503-149">Comment récupérer des informations d’adresse IP privée statique pour une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bb503-149">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="bb503-150">Pour visualiser les informations d’adresse IP privée statique concernant la machine virtuelle créée avec le script ci-dessus, exécutez la commande Azure CLI suivante, puis examinez les valeurs *Private IP alloc-method* et *Private IP address* :</span><span class="sxs-lookup"><span data-stu-id="bb503-150">To view the static private IP address information for the VM created with the script above, run the following Azure CLI command and observe the values for *Private IP alloc-method* and *Private IP address*:</span></span>

    azure vm show -g TestRG -n DNS01

<span data-ttu-id="bb503-151">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="bb503-151">Expected output:</span></span>

    info:    Executing command vm show
    + Looking up the VM "DNS01"
    + Looking up the NIC "TestNIC"
    + Looking up the public ip "TestPIP
    data:    Id                              :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    ProvisioningState               :Succeeded
    data:    Name                            :DNS01
    data:    Location                        :centralus
    data:    Type                            :Microsoft.Compute/virtualMachines
    data:
    data:    Hardware Profile:
    data:      Size                          :Standard_A1
    data:
    data:    Storage Profile:
    data:      Source image:
    data:        Id                          :/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/services/images/bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
    data:
    data:      OS Disk:
    data:        OSType                      :Windows
    data:        Name                        :cli08d7bd987a0112a8-os-1441774961355
    data:        Caching                     :ReadWrite
    data:        CreateOption                :FromImage
    data:        Vhd:
    data:          Uri                       :https://vnetstorage2.blob.core.windows.net/vhds/cli08d7bd987a0112a8-os-1441774961355vhd
    data:
    data:    OS Profile:
    data:      Computer Name                 :DNS01
    data:      User Name                     :adminuser
    data:      Windows Configuration:
    data:        Provision VM Agent          :true
    data:        Enable automatic updates    :true
    data:
    data:    Network Profile:
    data:      Network Interfaces:
    data:        Network Interface #1:
    data:          Id                        :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    data:          Primary                   :true
    data:          MAC Address               :00-0D-3A-90-1A-A8
    data:          Provisioning State        :Succeeded
    data:          Name                      :TestNIC
    data:          Location                  :centralus
    data:            Private IP alloc-method :Static
    data:            Private IP address      :192.168.1.101
    data:            Public IP address       :40.122.213.159
    info:    vm show command OK

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="bb503-152">Comment supprimer une adresse IP privée statique d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bb503-152">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="bb503-153">Vous ne pouvez pas supprimer une adresse IP privée statique à partir d’une carte réseau dans l’interface de ligne de commande de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bb503-153">You cannot remove a static private IP address from a NIC in Azure CLI for Resource Manager.</span></span> <span data-ttu-id="bb503-154">Vous devez créer une nouvelle carte réseau qui utilise une adresse IP dynamique, supprimer la carte réseau précédente de la machine virtuelle et ajouter la nouvelle carte réseau à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bb503-154">You must create a new NIC that uses a dynamic IP, remove the previous NIC from the VM, and then add the new NIC to the VM.</span></span> <span data-ttu-id="bb503-155">Pour modifier la carte réseau de la machine virtuelle utilisée dans les commandes ci-dessus, suivez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="bb503-155">To change the NIC for the VM used int eh commands above, follow the steps below.</span></span>

1. <span data-ttu-id="bb503-156">Exécutez la commande **azure network nic create** pour créer une nouvelle carte réseau à l’aide de l’allocation d’adresses IP dynamiques.</span><span class="sxs-lookup"><span data-stu-id="bb503-156">Run the **azure network nic create** command to create a new NIC using dynamic IP allocation.</span></span> <span data-ttu-id="bb503-157">Notez que cette fois, vous n’avez pas besoin de spécifier l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="bb503-157">Notice how you do not need to specify the IP address this time.</span></span>
   
        azure network nic create -g TestRG -n TestNIC2 -l centralus -m TestVNet -k FrontEnd
   
    <span data-ttu-id="bb503-158">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="bb503-158">Expected output:</span></span>
   
        info:    Executing command network nic create
        + Looking up the network interface "TestNIC2"
        + Looking up the subnet "FrontEnd"
        + Creating network interface "TestNIC2"
        + Looking up the network interface "TestNIC2"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
        data:    Name                            : TestNIC2
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.6
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
2. <span data-ttu-id="bb503-159">exécutez la commande **azure vm set** pour modifier la carte réseau utilisée par la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bb503-159">Run the **azure vm set** command to change the NIC used by the VM.</span></span>
   
        azure vm set -g TestRG -n DNS01 -N TestNIC2
   
    <span data-ttu-id="bb503-160">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="bb503-160">Expected output:</span></span>
   
        info:    Executing command vm set
        + Looking up the VM "DNS01"
        + Looking up the NIC "TestNIC2"
        + Updating VM "DNS01"
        info:    vm set command OK
3. <span data-ttu-id="bb503-161">le cas échéant, exécutez la commande **azure network nic delete** pour supprimer l’ancienne carte réseau.</span><span class="sxs-lookup"><span data-stu-id="bb503-161">If wanted, run the **azure network nic delete** command to delete the old NIC.</span></span>
   
        azure network nic delete -g TestRG -n TestNIC --quiet
   
    <span data-ttu-id="bb503-162">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="bb503-162">Expected output:</span></span>
   
        info:    Executing command network nic delete
        + Looking up the network interface "TestNIC"
        + Deleting network interface "TestNIC"
        info:    network nic delete command OK

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="bb503-163">Comment ajouter une adresse IP privée statique à une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="bb503-163">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="bb503-164">Pour ajouter une adresse IP privée statique à la carte d’interface réseau utilisée par la machine virtuelle créée à l’aide du script ci-dessus, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bb503-164">To add a static private IP address to the NIC used by teh VM created using the script above, run the following command:</span></span>

    azure network nic set -g TestRG -n TestNIC2 -a 192.168.1.101

<span data-ttu-id="bb503-165">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="bb503-165">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up the network interface "TestNIC2"
    + Updating network interface "TestNIC2"
    + Looking up the network interface "TestNIC2"
    data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
    data:    Name                            : TestNIC2
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : centralus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-90-29-25
    data:    Enable IP forwarding            : false
    data:    Virtual machine                 : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    IP configurations:
    data:      Name                          : NIC-config
    data:      Provisioning state            : Succeeded
    data:      Private IP address            : 192.168.1.101
    data:      Private IP Allocation Method  : Static
    data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

## <a name="next-steps"></a><span data-ttu-id="bb503-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bb503-166">Next steps</span></span>
* <span data-ttu-id="bb503-167">En savoir plus sur les [adresses IP publiques réservées](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="bb503-167">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="bb503-168">En savoir plus sur les [adresses IP publiques de niveau d’instance](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="bb503-168">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="bb503-169">Consulter les [API REST d’adresse IP réservée](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="bb503-169">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

