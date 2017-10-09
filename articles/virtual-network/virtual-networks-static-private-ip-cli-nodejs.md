---
title: "les adresses IP privées aaaConfigure pour les machines virtuelles - Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment les adresses IP privées tooconfigure pour les ordinateurs virtuels à l’aide de hello Azure interface de ligne de commande (CLI) 1.0."
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
ms.openlocfilehash: 6caae79c98c7bc5f246b7bb3bb8bd8f032eb2d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-10"></a><span data-ttu-id="8cd66-103">Configurer des adresses IP privées pour un ordinateur virtuel à l’aide de hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8cd66-103">Configure private IP addresses for a virtual machine using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="8cd66-104">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="8cd66-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="8cd66-105">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="8cd66-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="8cd66-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="8cd66-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="8cd66-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) -CLI de notre nouvelle génération pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="8cd66-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="8cd66-108">Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="8cd66-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="8cd66-109">Vous pouvez également [gérer une adresse IP privée statique dans le modèle de déploiement classique hello](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8cd66-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="8cd66-110">commandes CLI d’Azure d’exemple Hello ci-dessous s’attendre à un environnement simple déjà créé.</span><span class="sxs-lookup"><span data-stu-id="8cd66-110">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="8cd66-111">Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, tout d’abord créer d’environnement de test hello décrit dans [créer un réseau virtuel](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8cd66-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="8cd66-112">Comment toospecify une adresse IP privée statique d’adresses lorsque vous créez une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8cd66-112">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="8cd66-113">toocreate un ordinateur virtuel nommé *DNS01* Bonjour *frontal* sous-réseau d’un réseau virtuel nommé *TestVNet* avec une adresse IP privée statique de *192.168.1.101*, Suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8cd66-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="8cd66-114">Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="8cd66-114">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="8cd66-115">Exécutez hello **configuration azure mode** mode Manager tooResource commande tooswitch, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8cd66-115">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="8cd66-116">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8cd66-116">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="8cd66-117">Exécutez hello **public-ip de réseau azure créer** toocreate une adresse IP publique pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8cd66-117">Run hello **azure network public-ip create** toocreate a public IP for hello VM.</span></span> <span data-ttu-id="8cd66-118">liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.</span><span class="sxs-lookup"><span data-stu-id="8cd66-118">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network public-ip create -g TestRG -n TestPIP -l centralus
   
    <span data-ttu-id="8cd66-119">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8cd66-119">Expected output:</span></span>
   
        info:    Executing command network public-ip create
        + Looking up hello public ip "TestPIP"
        + Creating public ip address "TestPIP"
        + Looking up hello public ip "TestPIP"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP
        data:    Name                            : TestPIP
        data:    Type                            : Microsoft.Network/publicIPAddresses
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Allocation method               : Dynamic
        data:    Idle timeout                    : 4
        info:    network public-ip create command OK
   
   * <span data-ttu-id="8cd66-120">**-g (ou --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="8cd66-120">**-g (or --resource-group)**.</span></span> <span data-ttu-id="8cd66-121">Nom de l’adresse IP publique hello ressource groupe hello sera créé dans.</span><span class="sxs-lookup"><span data-stu-id="8cd66-121">Name of hello resource group hello public IP will be created in.</span></span>
   * <span data-ttu-id="8cd66-122">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="8cd66-122">**-n (or --name)**.</span></span> <span data-ttu-id="8cd66-123">Nom de l’adresse IP publique hello.</span><span class="sxs-lookup"><span data-stu-id="8cd66-123">Name of hello public IP.</span></span>
   * <span data-ttu-id="8cd66-124">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="8cd66-124">**-l (or --location)**.</span></span> <span data-ttu-id="8cd66-125">Région Azure où adresse IP publique hello sera créé.</span><span class="sxs-lookup"><span data-stu-id="8cd66-125">Azure region where hello public IP will be created.</span></span> <span data-ttu-id="8cd66-126">Pour notre scénario, *centralus*.</span><span class="sxs-lookup"><span data-stu-id="8cd66-126">For our scenario, *centralus*.</span></span>
4. <span data-ttu-id="8cd66-127">Exécutez hello **créer des cartes réseau du réseau azure** commande toocreate une carte réseau avec une adresse IP statique privée.</span><span class="sxs-lookup"><span data-stu-id="8cd66-127">Run hello **azure network nic create** command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="8cd66-128">liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.</span><span class="sxs-lookup"><span data-stu-id="8cd66-128">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network nic create -g TestRG -n TestNIC -l centralus -a 192.168.1.101 -m TestVNet -k FrontEnd
   
    <span data-ttu-id="8cd66-129">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8cd66-129">Expected output:</span></span>
   
        + Looking up hello network interface "TestNIC"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC"
        + Looking up hello network interface "TestNIC"
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
   
   * <span data-ttu-id="8cd66-130">**-a (or --private-ip-address)**.</span><span class="sxs-lookup"><span data-stu-id="8cd66-130">**-a (or --private-ip-address)**.</span></span> <span data-ttu-id="8cd66-131">Adresse IP privée statique pour hello carte réseau.</span><span class="sxs-lookup"><span data-stu-id="8cd66-131">Static private IP address for hello NIC.</span></span>
   * <span data-ttu-id="8cd66-132">**-m (or --subnet-vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="8cd66-132">**-m (or --subnet-vnet-name)**.</span></span> <span data-ttu-id="8cd66-133">Nom de hello réseau virtuel où hello carte réseau doit être créé.</span><span class="sxs-lookup"><span data-stu-id="8cd66-133">Name of hello VNet where hello NIC will be created.</span></span>
   * <span data-ttu-id="8cd66-134">**-k (or --subnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="8cd66-134">**-k (or --subnet-name)**.</span></span> <span data-ttu-id="8cd66-135">Nom du sous-réseau hello où hello carte réseau doit être créé.</span><span class="sxs-lookup"><span data-stu-id="8cd66-135">Name of hello subnet where hello NIC will be created.</span></span>
5. <span data-ttu-id="8cd66-136">Exécutez hello **créer de machine virtuelle azure** commande toocreate hello machine virtuelle en utilisant l’adresse IP publique hello et la carte réseau créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="8cd66-136">Run hello **azure vm create** command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="8cd66-137">liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.</span><span class="sxs-lookup"><span data-stu-id="8cd66-137">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -g TestRG -n DNS01 -l centralus -y Windows -f TestNIC -i TestPIP -F TestVNet -j FrontEnd -o vnetstorage -q bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 -u adminuser -p AdminP@ssw0rd
   
    <span data-ttu-id="8cd66-138">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8cd66-138">Expected output:</span></span>
   
        info:    Executing command vm create
        + Looking up hello VM "DNS01"
        info:    Using hello VM Size "Standard_A1"
        warn:    hello image "bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2" will be used for VM
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account vnetstorage
        + Looking up hello NIC "TestNIC"
        info:    Found an existing NIC "TestNIC"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd" in hello NIC "TestNIC"
        info:    Found public ip parameters, trying toosetup PublicIP profile
        + Looking up hello public ip "TestPIP"
        info:    Found an existing PublicIP "TestPIP"
        info:    Configuring identified NIC IP configuration with PublicIP "TestPIP"
        + Updating NIC "TestNIC"
        + Looking up hello NIC "TestNIC"
        + Creating VM "DNS01"
        info:    vm create command OK
   
   * <span data-ttu-id="8cd66-139">**-y (ou type de système d’exploitation--)**.</span><span class="sxs-lookup"><span data-stu-id="8cd66-139">**-y (or --os-type)**.</span></span> <span data-ttu-id="8cd66-140">Type de hello machine virtuelle, système d’exploitation, soit *Windows* ou *Linux*.</span><span class="sxs-lookup"><span data-stu-id="8cd66-140">Type of operating system for hello VM, either *Windows* or *Linux*.</span></span>
   * <span data-ttu-id="8cd66-141">**-f (ou nom de la carte réseau--)**.</span><span class="sxs-lookup"><span data-stu-id="8cd66-141">**-f (or --nic-name)**.</span></span> <span data-ttu-id="8cd66-142">Nom de Bonjour Bonjour de carte réseau virtuelle utilisera.</span><span class="sxs-lookup"><span data-stu-id="8cd66-142">Name of hello NIC hello VM will use.</span></span>
   * <span data-ttu-id="8cd66-143">**-i (ou --nom ip public)**.</span><span class="sxs-lookup"><span data-stu-id="8cd66-143">**-i (or --public-ip-name)**.</span></span> <span data-ttu-id="8cd66-144">Nom de Bonjour Bonjour IP public VM utilisera.</span><span class="sxs-lookup"><span data-stu-id="8cd66-144">Name of hello public IP hello VM will use.</span></span>
   * <span data-ttu-id="8cd66-145">**-F (ou --nom vnet)**.</span><span class="sxs-lookup"><span data-stu-id="8cd66-145">**-F (or --vnet-name)**.</span></span> <span data-ttu-id="8cd66-146">Nom de hello réseau virtuel où hello machine virtuelle doit être créé.</span><span class="sxs-lookup"><span data-stu-id="8cd66-146">Name of hello VNet where hello VM will be created.</span></span>
   * <span data-ttu-id="8cd66-147">**-j (or --vnet-subnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="8cd66-147">**-j (or --vnet-subnet-name)**.</span></span> <span data-ttu-id="8cd66-148">Nom du sous-réseau hello où hello machine virtuelle doit être créé.</span><span class="sxs-lookup"><span data-stu-id="8cd66-148">Name of hello subnet where hello VM will be created.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="8cd66-149">Comment informations pour une machine virtuelle d’adresse IP privée statique de tooretrieve</span><span class="sxs-lookup"><span data-stu-id="8cd66-149">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="8cd66-150">adresse IP privée statique de tooview hello adresse hello pour les ordinateurs virtuels créés avec script hello ci-dessus, exécutez hello suivant commande CLI d’Azure et observer les valeurs hello pour *IP privée de la méthode d’allocation* et *l’adresse IP privée*:</span><span class="sxs-lookup"><span data-stu-id="8cd66-150">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

    azure vm show -g TestRG -n DNS01

<span data-ttu-id="8cd66-151">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8cd66-151">Expected output:</span></span>

    info:    Executing command vm show
    + Looking up hello VM "DNS01"
    + Looking up hello NIC "TestNIC"
    + Looking up hello public ip "TestPIP
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

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="8cd66-152">Comment tooremove une privée d’adresses IP statiques à partir d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8cd66-152">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="8cd66-153">Vous ne pouvez pas supprimer une adresse IP privée statique à partir d’une carte réseau dans l’interface de ligne de commande de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8cd66-153">You cannot remove a static private IP address from a NIC in Azure CLI for Resource Manager.</span></span> <span data-ttu-id="8cd66-154">Vous devez créer une nouvelle carte réseau qui utilise une adresse IP dynamique, supprimez hello NIC précédente à partir de la machine virtuelle de hello et ajoutez hello nouvelle carte réseau toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8cd66-154">You must create a new NIC that uses a dynamic IP, remove hello previous NIC from hello VM, and then add hello new NIC toohello VM.</span></span> <span data-ttu-id="8cd66-155">toochange hello NIC pour hello VM utilisé int eh commandes ci-dessus, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8cd66-155">toochange hello NIC for hello VM used int eh commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="8cd66-156">Exécutez hello **créer des cartes réseau du réseau azure** commande toocreate une nouvelle carte réseau à l’aide de l’allocation dynamique d’IP.</span><span class="sxs-lookup"><span data-stu-id="8cd66-156">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation.</span></span> <span data-ttu-id="8cd66-157">Notez comment il est inutile adresse IP de hello toospecify cette heure.</span><span class="sxs-lookup"><span data-stu-id="8cd66-157">Notice how you do not need toospecify hello IP address this time.</span></span>
   
        azure network nic create -g TestRG -n TestNIC2 -l centralus -m TestVNet -k FrontEnd
   
    <span data-ttu-id="8cd66-158">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8cd66-158">Expected output:</span></span>
   
        info:    Executing command network nic create
        + Looking up hello network interface "TestNIC2"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC2"
        + Looking up hello network interface "TestNIC2"
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
2. <span data-ttu-id="8cd66-159">Exécutez hello **ensemble de la machine virtuelle azure** commande toochange hello carte réseau utilisée par hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8cd66-159">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
        azure vm set -g TestRG -n DNS01 -N TestNIC2
   
    <span data-ttu-id="8cd66-160">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8cd66-160">Expected output:</span></span>
   
        info:    Executing command vm set
        + Looking up hello VM "DNS01"
        + Looking up hello NIC "TestNIC2"
        + Updating VM "DNS01"
        info:    vm set command OK
3. <span data-ttu-id="8cd66-161">Si vous souhaitiez, exécutez hello **supprimer les cartes réseau du réseau azure** commande hello de toodelete ancien NIC.</span><span class="sxs-lookup"><span data-stu-id="8cd66-161">If wanted, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
        azure network nic delete -g TestRG -n TestNIC --quiet
   
    <span data-ttu-id="8cd66-162">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8cd66-162">Expected output:</span></span>
   
        info:    Executing command network nic delete
        + Looking up hello network interface "TestNIC"
        + Deleting network interface "TestNIC"
        info:    network nic delete command OK

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="8cd66-163">Comment tooadd une adresse IP privée statique d’adresses tooan existant de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8cd66-163">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="8cd66-164">tooadd un toohello d’adresse IP privée statique carte réseau utilisée par l’ordinateur virtuel créé à l’aide du script hello ci-dessus, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8cd66-164">tooadd a static private IP address toohello NIC used by teh VM created using hello script above, run hello following command:</span></span>

    azure network nic set -g TestRG -n TestNIC2 -a 192.168.1.101

<span data-ttu-id="8cd66-165">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8cd66-165">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNIC2"
    + Updating network interface "TestNIC2"
    + Looking up hello network interface "TestNIC2"
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

## <a name="next-steps"></a><span data-ttu-id="8cd66-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8cd66-166">Next steps</span></span>
* <span data-ttu-id="8cd66-167">En savoir plus sur les [adresses IP publiques réservées](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="8cd66-167">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="8cd66-168">En savoir plus sur les [adresses IP publiques de niveau d’instance](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="8cd66-168">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="8cd66-169">Consultez hello [API REST de IP réservée](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="8cd66-169">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

