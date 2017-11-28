---
title: "les adresses IP privées aaaConfigure pour les machines virtuelles - Azure PowerShell | Documents Microsoft"
description: "Découvrez comment les adresses IP privées de tooconfigure pour les ordinateurs virtuels à l’aide de PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: d5f18929-15e3-40a2-9ee3-8188bc248ed8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4a3eb67de583e08208fcab40de1c2a8a9b65618c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a><span data-ttu-id="1198e-103">Configurer des adresses IP privées pour une machine virtuelle à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="1198e-103">Configure private IP addresses for a virtual machine using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

<span data-ttu-id="1198e-104">Azure propose deux modèles de déploiement : Azure Resource Manager et classique.</span><span class="sxs-lookup"><span data-stu-id="1198e-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="1198e-105">Microsoft recommande de créer des ressources via le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="1198e-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="1198e-106">toolearn en savoir plus sur hello différences entre hello deux modèles, lire hello [modèles de déploiement Azure de comprendre](../azure-resource-manager/resource-manager-deployment-model.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="1198e-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="1198e-107">Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="1198e-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="1198e-108">Vous pouvez également [gérer une adresse IP privée statique dans le modèle de déploiement classique hello](virtual-networks-static-private-ip-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1198e-108">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="1198e-109">l’exemple Hello PowerShell commandes ci-dessous attendent un simple environnement déjà créé en fonction de scénario hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="1198e-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="1198e-110">Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, tout d’abord créer d’environnement de test hello décrit dans [créer un réseau virtuel](virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="1198e-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span></span>

## <a name="create-a-vm-with-a-static-private-ip-address"></a><span data-ttu-id="1198e-111">Créer une machine virtuelle avec une adresse IP privée statique</span><span class="sxs-lookup"><span data-stu-id="1198e-111">Create a VM with a static private IP address</span></span>
<span data-ttu-id="1198e-112">toocreate un ordinateur virtuel nommé *DNS01* Bonjour *frontal* sous-réseau d’un réseau virtuel nommé *TestVNet* avec une adresse IP privée statique de *192.168.1.101*, Suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1198e-112">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="1198e-113">Définir les variables pour le compte de stockage hello, l’emplacement, groupe de ressources et toobe des informations d’identification utilisées.</span><span class="sxs-lookup"><span data-stu-id="1198e-113">Set variables for hello storage account, location, resource group, and credentials toobe used.</span></span> <span data-ttu-id="1198e-114">Vous devez tooenter un nom d’utilisateur et mot de passe pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1198e-114">You will need tooenter a user name and password for hello VM.</span></span> <span data-ttu-id="1198e-115">groupe de comptes et de ressources de stockage Hello doit déjà exister.</span><span class="sxs-lookup"><span data-stu-id="1198e-115">hello storage account and resource group must already exist.</span></span>

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type hello name and password of hello local administrator account."
    ```

2. <span data-ttu-id="1198e-116">Réseau virtuel de récupération hello et sous-réseau toocreate hello machine virtuelle dans.</span><span class="sxs-lookup"><span data-stu-id="1198e-116">Retrieve hello virtual network and subnet you want toocreate hello VM in.</span></span>

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. <span data-ttu-id="1198e-117">Si nécessaire, créez un Bonjour de tooaccess adresse IP publique machine virtuelle à partir de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="1198e-117">If necessary, create a public IP address tooaccess hello VM from hello Internet.</span></span>

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. <span data-ttu-id="1198e-118">Créer une carte réseau à l’aide de hello adresse IP privée statique souhaité tooassign toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1198e-118">Create a NIC using hello static private IP address you want tooassign toohello VM.</span></span> <span data-ttu-id="1198e-119">Vérifiez que hello IP est de plage de sous-réseau hello vous ajoutez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1198e-119">Make sure hello IP is from hello subnet range you are adding hello VM to.</span></span> <span data-ttu-id="1198e-120">Ceci est hello principal pour cet article, où vous avez défini les toobe IP privé hello statique.</span><span class="sxs-lookup"><span data-stu-id="1198e-120">This is hello main step for this article, where you set hello private IP toobe static.</span></span>

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. <span data-ttu-id="1198e-121">Créer hello à l’aide de hello NIC de machine virtuelle créée ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="1198e-121">Create hello VM using hello NIC created above.</span></span>

    ```powershell
    $vm = New-AzureRmVMConfig -VMName DNS01 -VMSize "Standard_A1"
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName DNS01 `
    -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri = $storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/WindowsVMosDisk.vhd"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name "windowsvmosdisk" -VhdUri $osDiskUri `
    -CreateOption fromImage
    New-AzureRmVM -ResourceGroupName $rgName -Location $locName -VM $vm 
    ```

    <span data-ttu-id="1198e-122">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="1198e-122">Expected output:</span></span>
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a><span data-ttu-id="1198e-123">Récupérer les informations d’adresse IP privée statique d’une interface réseau</span><span class="sxs-lookup"><span data-stu-id="1198e-123">Retrieve static private IP address information for a network interface</span></span>
<span data-ttu-id="1198e-124">adresse IP privée statique de tooview hello adresse hello pour les ordinateurs virtuels créés avec script hello ci-dessus, exécutez hello suivant de commande PowerShell et observer les valeurs hello pour *une adresse IP privée* et  *PrivateIpAllocationMethod*:</span><span class="sxs-lookup"><span data-stu-id="1198e-124">tooview hello static private IP address information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span></span>

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

<span data-ttu-id="1198e-125">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="1198e-125">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Static",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a><span data-ttu-id="1198e-126">Supprimer une adresse IP privée statique d’une interface réseau</span><span class="sxs-lookup"><span data-stu-id="1198e-126">Remove a static private IP address from a network interface</span></span>
<span data-ttu-id="1198e-127">tooremove hello adresse IP privée statique ajouté toohello machine virtuelle dans le script hello ci-dessus, hello exécution suivant des commandes PowerShell :</span><span class="sxs-lookup"><span data-stu-id="1198e-127">tooremove hello static private IP address added toohello VM in hello script above, run hello following PowerShell commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="1198e-128">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="1198e-128">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WindowsVM"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Dynamic",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="add-a-static-private-ip-address-tooa-network-interface"></a><span data-ttu-id="1198e-129">Ajoutez un statique privé IP adresse tooa d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="1198e-129">Add a static private IP address tooa network interface</span></span>
<span data-ttu-id="1198e-130">tooadd un toohello d’adresse IP privée statique machine virtuelle créée à l’aide du script hello ci-dessus, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="1198e-130">tooadd a static private IP address toohello VM created using hello script above, run hello following commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-hello-allocation-method-for-a-private-ip-address-assigned-tooa-network-interface"></a><span data-ttu-id="1198e-131">Modifier la méthode d’allocation hello pour une adresse IP privée affecté l’interface de réseau tooa</span><span class="sxs-lookup"><span data-stu-id="1198e-131">Change hello allocation method for a private IP address assigned tooa network interface</span></span>

<span data-ttu-id="1198e-132">Une adresse IP privée est affectée tooa carte réseau avec la méthode d’allocation statique ou dynamique hello.</span><span class="sxs-lookup"><span data-stu-id="1198e-132">A private IP address is assigned tooa NIC with hello static or dynamic allocation method.</span></span> <span data-ttu-id="1198e-133">Des adresses IP dynamiques peuvent changer après que le démarrage d’un ordinateur virtuel qui a été précédemment Bonjour arrêtée (désallouée) d’état.</span><span class="sxs-lookup"><span data-stu-id="1198e-133">Dynamic IP addresses can change after starting a VM that was previously in hello stopped (deallocated) state.</span></span> <span data-ttu-id="1198e-134">Cela peut entraîner des problèmes potentiellement si hello machine virtuelle héberge un service qui requiert hello même adresse IP, même après le redémarrage de l’état arrêté (désalloué).</span><span class="sxs-lookup"><span data-stu-id="1198e-134">This can potentially cause issues if hello VM is hosting a service that requires hello same IP address, even after restarts from a stopped (deallocated) state.</span></span> <span data-ttu-id="1198e-135">Les adresses IP statiques sont conservées jusqu'à la suppression de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1198e-135">Static IP addresses are retained until hello VM is deleted.</span></span> <span data-ttu-id="1198e-136">méthode d’allocation du hello toochange d’une adresse IP, exécutez hello script, ce qui modifie la méthode d’allocation de hello de toostatic dynamique suivant.</span><span class="sxs-lookup"><span data-stu-id="1198e-136">toochange hello allocation method of an IP address, run hello following script, which changes hello allocation method from dynamic toostatic.</span></span> <span data-ttu-id="1198e-137">Si la méthode d’allocation hello pour l’adresse IP privée actuelle hello est statique, modifiez *statique* trop*dynamique* avant d’exécuter le script de hello.</span><span class="sxs-lookup"><span data-stu-id="1198e-137">If hello allocation method for hello current private IP address is static, change *Static* too*Dynamic* before executing hello script.</span></span>

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "hello allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for hello IP address" $IP"." -NoNewline
```

<span data-ttu-id="1198e-138">Si vous ne connaissez pas nom hello Hello carte réseau, vous pouvez afficher une liste de cartes réseau dans un groupe de ressources en entrant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1198e-138">If you don't know hello name of hello NIC, you can view a list of NICs within a resource group by entering hello following command:</span></span>

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a><span data-ttu-id="1198e-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1198e-139">Next steps</span></span>
* <span data-ttu-id="1198e-140">En savoir plus sur les [adresses IP publiques réservées](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="1198e-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="1198e-141">En savoir plus sur les [adresses IP publiques de niveau d’instance](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="1198e-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="1198e-142">Consultez hello [API REST de IP réservée](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="1198e-142">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

