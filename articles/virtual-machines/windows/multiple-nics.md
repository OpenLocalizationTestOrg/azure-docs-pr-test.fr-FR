---
title: "Créer et gérer dans Azure des machines virtuelles Windows utilisant plusieurs cartes d’interface réseau | Microsoft Docs"
description: "Découvrez comment créer et gérer une machine virtuelle Windows équipée de plusieurs cartes d’interface réseau à l’aide d’Azure PowerShell ou de modèles Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 3bd99a67dae41de3533d7f6e244eb7ee3ecc4049
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="808c5-103">Créer et gérer une machine virtuelle Windows équipée de plusieurs cartes d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="808c5-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="808c5-104">Les machines virtuelles (VM) dans Azure peuvent être équipées de plusieurs cartes d’interface réseau (NIC) virtuelles.</span><span class="sxs-lookup"><span data-stu-id="808c5-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached to them.</span></span> <span data-ttu-id="808c5-105">Un scénario courant consiste à avoir des sous-réseaux différents pour les connectivités frontale et principale, ou un réseau dédié à une solution de surveillance ou de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="808c5-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="808c5-106">Cet article explique comment créer une machine virtuelle équipée de plusieurs cartes d’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="808c5-106">This article details how to create a VM that has multiple NICs attached to it.</span></span> <span data-ttu-id="808c5-107">Il explique également comment ajouter ou supprimer des cartes d’interface réseau d’une machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="808c5-107">You also learn how to add or remove NICs from an existing VM.</span></span> <span data-ttu-id="808c5-108">Comme le nombre de cartes réseau prises en charge varie suivant la [taille des machines virtuelles](sizes.md) , pensez à dimensionner la vôtre en conséquence.</span><span class="sxs-lookup"><span data-stu-id="808c5-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="808c5-109">Pour plus d’informations, notamment sur la création de plusieurs cartes d’interface réseau dans vos propres scripts PowerShell, voir [Déploiement de machines virtuelles avec plusieurs cartes d’interface réseau](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="808c5-109">For detailed information, including how to create multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="808c5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="808c5-110">Prerequisites</span></span>
<span data-ttu-id="808c5-111">Vérifiez que vous disposez de la [dernière version d’Azure PowerShell installée et configurée](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="808c5-111">Make sure that you have the [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="808c5-112">Dans les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="808c5-112">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="808c5-113">Les noms de paramètre sont par exemple *myResourceGroup*, *myVnet* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="808c5-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="808c5-114">Créer une machine virtuelle avec plusieurs cartes d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="808c5-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="808c5-115">Créez d’abord un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="808c5-115">First, create a resource group.</span></span> <span data-ttu-id="808c5-116">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *EastUs*:</span><span class="sxs-lookup"><span data-stu-id="808c5-116">The following example creates a resource group named *myResourceGroup* in the *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="808c5-117">Créer un réseau virtuel et des sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="808c5-117">Create virtual network and subnets</span></span>
<span data-ttu-id="808c5-118">Un scénario courant pour un réseau virtuel consiste à avoir deux sous-réseaux ou plus.</span><span class="sxs-lookup"><span data-stu-id="808c5-118">A common scenario is for a virtual network to have two or more subnets.</span></span> <span data-ttu-id="808c5-119">Un sous-réseau peut être dédié au trafic frontal, et l’autre au trafic principal.</span><span class="sxs-lookup"><span data-stu-id="808c5-119">One subnet may be for front-end traffic, the other for back-end traffic.</span></span> <span data-ttu-id="808c5-120">Pour connecter les deux sous-réseaux, vous utilisez ensuite plusieurs cartes d’interface réseau sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="808c5-120">To connect to both subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="808c5-121">Définissez deux sous-réseaux de réseau virtuel avec la commande [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="808c5-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="808c5-122">L’exemple suivant définit les sous-réseaux pour *mySubnetFrontEnd* et *mySubnetBackEnd* :</span><span class="sxs-lookup"><span data-stu-id="808c5-122">The following example defines the subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="808c5-123">Créez votre réseau virtuel et vos sous-réseaux avec la commande [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="808c5-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="808c5-124">L’exemple suivant crée un réseau virtuel nommé *myVnet* :</span><span class="sxs-lookup"><span data-stu-id="808c5-124">The following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="808c5-125">Créer plusieurs cartes réseau</span><span class="sxs-lookup"><span data-stu-id="808c5-125">Create multiple NICs</span></span>
<span data-ttu-id="808c5-126">Créez deux cartes d’interface réseau avec la commande [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="808c5-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="808c5-127">Associez une carte d’interface réseau au sous-réseau frontal et l’autre au sous-réseau principal.</span><span class="sxs-lookup"><span data-stu-id="808c5-127">Attach one NIC to the front-end subnet and one NIC to the back-end subnet.</span></span> <span data-ttu-id="808c5-128">L’exemple suivant crée des cartes d’interface réseau nommées *myNic1* et *myNic2* :</span><span class="sxs-lookup"><span data-stu-id="808c5-128">The following example creates NICs named *myNic1* and *myNic2*:</span></span>

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

<span data-ttu-id="808c5-129">En général, vous créez également un [groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md) ou un [équilibreur de charge](../../load-balancer/load-balancer-overview.md) pour faciliter la gestion et la répartition du trafic entre vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="808c5-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="808c5-130">L’article [Machines virtuelles équipées de plusieurs cartes d’interface réseau](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) explique comment créer un groupe de sécurité réseau et affecter des cartes d’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="808c5-130">The [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-the-virtual-machine"></a><span data-ttu-id="808c5-131">Créer la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="808c5-131">Create the virtual machine</span></span>
<span data-ttu-id="808c5-132">Maintenant, commencez à élaborer la configuration de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="808c5-132">Now start to build your VM configuration.</span></span> <span data-ttu-id="808c5-133">La taille d’une machine virtuelle détermine le nombre maximal de cartes réseau qu’elle peut accueillir.</span><span class="sxs-lookup"><span data-stu-id="808c5-133">Each VM size has a limit for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="808c5-134">Pour plus d’informations, voir [Tailles des machines virtuelles Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="808c5-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="808c5-135">Tout d’abord, définissez les informations d’identification de votre machine virtuelle sur la variable `$cred` comme suit :</span><span class="sxs-lookup"><span data-stu-id="808c5-135">Set your VM credentials to the `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="808c5-136">Définissez votre machine virtuelle avec la commande [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span><span class="sxs-lookup"><span data-stu-id="808c5-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="808c5-137">L’exemple suivant définit une machine virtuelle nommée *myVM* et utilise une taille de machine virtuelle qui prend en charge plus de deux cartes d’interface réseau (*Standard_DS3_v2*) :</span><span class="sxs-lookup"><span data-stu-id="808c5-137">The following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="808c5-138">Créez le reste de la configuration de votre machine virtuelle avec les commandes [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) et [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span><span class="sxs-lookup"><span data-stu-id="808c5-138">Create the rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="808c5-139">L’exemple suivant crée une machine virtuelle Windows Server 2016 R2 :</span><span class="sxs-lookup"><span data-stu-id="808c5-139">The following example creates a Windows Server 2016 VM:</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. <span data-ttu-id="808c5-140">Associez les deux cartes d’interface réseau que vous avez créées précédemment à l’aide de la commande [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) :</span><span class="sxs-lookup"><span data-stu-id="808c5-140">Attach the two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="808c5-141">Enfin, créez votre machine virtuelle avec la commande [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) :</span><span class="sxs-lookup"><span data-stu-id="808c5-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-to-an-existing-vm"></a><span data-ttu-id="808c5-142">Ajouter une carte réseau à une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="808c5-142">Add a NIC to an existing VM</span></span>
<span data-ttu-id="808c5-143">Pour ajouter une carte d’interface réseau virtuelle à une machine virtuelle existante, désallouez la machine virtuelle, ajoutez la carte d’interface réseau virtuelle, puis démarrez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="808c5-143">To add a virtual NIC to an existing VM, you deallocate the VM, add the virtual NIC, then start the VM.</span></span>

1. <span data-ttu-id="808c5-144">Désallouez la machine virtuelle avec la commande [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="808c5-144">Deallocate the VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="808c5-145">L’exemple suivant désalloue la machine virtuelle nommée *myVM* dans *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="808c5-145">The following example deallocates the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="808c5-146">Obtenez la configuration existante de la machine virtuelle avec commande [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="808c5-146">Get the existing configuration of the VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="808c5-147">L’exemple suivant récupère des informations sur la machine virtuelle nommée *myVM* dans *myResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="808c5-147">The following example gets information for the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="808c5-148">L’exemple suivant crée une carte d’interface réseau virtuelle avec la commande [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface), nommée *myNic3*, et associée à *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="808c5-148">The following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached to *mySubnetBackEnd*.</span></span> <span data-ttu-id="808c5-149">La carte d’interface réseau virtuelle est ensuite associée à la machine virtuelle nommée *myVM* dans *myResourceGroup* avec la commande [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) :</span><span class="sxs-lookup"><span data-stu-id="808c5-149">The virtual NIC is then attached to the VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for the back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get the ID of the new virtual NIC and add to VM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="808c5-150">Cartes d’interface réseau virtuelles principales</span><span class="sxs-lookup"><span data-stu-id="808c5-150">Primary virtual NICs</span></span>
    <span data-ttu-id="808c5-151">L’une des cartes d’interface réseau sur une machine virtuelle dotées de plusieurs cartes doit être la carte principale.</span><span class="sxs-lookup"><span data-stu-id="808c5-151">One of the NICs on a multi-NIC VM needs to be primary.</span></span> <span data-ttu-id="808c5-152">Si l’une des cartes d’interface réseau virtuelles existantes sur la machine virtuelle est déjà définie comme principale, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="808c5-152">If one of the existing virtual NICs on the VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="808c5-153">L’exemple suivant suppose que deux cartes d’interface réseau virtuelles sont désormais présentes sur une machine virtuelle, et que vous souhaitez ajouter la première carte d’interface réseau (`[0]`) en tant que carte principale :</span><span class="sxs-lookup"><span data-stu-id="808c5-153">The following example assumes that two virtual NICs are now present on a VM and you wish to add the first NIC (`[0]`) as the primary:</span></span>
        
    ```powershell
    # List existing NICs on the VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 to be primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update the VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="808c5-154">Démarrez la machine virtuelle avec la commande [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm) :</span><span class="sxs-lookup"><span data-stu-id="808c5-154">Start the VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="808c5-155">Supprimer une carte réseau d’une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="808c5-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="808c5-156">Pour supprimer une carte d’interface réseau virtuelle à partir d’une machine virtuelle existante, désallouez la machine virtuelle, supprimez la carte d’interface réseau virtuelle, puis démarrez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="808c5-156">To remove a virtual NIC from an existing VM, you deallocate the VM, remove the virtual NIC, then start the VM.</span></span>

1. <span data-ttu-id="808c5-157">Désallouez la machine virtuelle avec la commande [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="808c5-157">Deallocate the VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="808c5-158">L’exemple suivant désalloue la machine virtuelle nommée *myVM* dans *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="808c5-158">The following example deallocates the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="808c5-159">Obtenez la configuration existante de la machine virtuelle avec commande [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="808c5-159">Get the existing configuration of the VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="808c5-160">L’exemple suivant récupère des informations sur la machine virtuelle nommée *myVM* dans *myResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="808c5-160">The following example gets information for the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="808c5-161">Obtenez des informations sur la suppression de la carte d’interface réseau avec la commande [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="808c5-161">Get information about the NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="808c5-162">L’exemple suivant obtient des informations sur la carte *myNic3* :</span><span class="sxs-lookup"><span data-stu-id="808c5-162">The following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on the VM if you need to determine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="808c5-163">Supprimez la carte d’interface réseau avec la commande [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface), puis mettez à jour la machine virtuelle avec la commande [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="808c5-163">Remove the NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update the VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="808c5-164">L’exemple suivant supprime la carte *myNic3* obtenue par `$nicId` à l’étape précédente :</span><span class="sxs-lookup"><span data-stu-id="808c5-164">The following example removes *myNic3* as obtained by `$nicId` in the preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="808c5-165">Démarrez la machine virtuelle avec la commande [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm) :</span><span class="sxs-lookup"><span data-stu-id="808c5-165">Start the VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="808c5-166">Créer plusieurs cartes d’interface réseau avec des modèles</span><span class="sxs-lookup"><span data-stu-id="808c5-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="808c5-167">Grâce aux modèles Azure Resource Manager, vous pouvez créer plusieurs instances d’une ressource pendant le déploiement, à l’image de la création de plusieurs cartes d’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="808c5-167">Azure Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="808c5-168">Les modèles Resource Manager utilisent des fichiers JSON déclaratifs pour définir votre environnement.</span><span class="sxs-lookup"><span data-stu-id="808c5-168">Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="808c5-169">Pour plus d’informations, voir [Présentation d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="808c5-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="808c5-170">Vous pouvez utiliser la commande *copy* pour spécifier le nombre d’instances à  :</span><span class="sxs-lookup"><span data-stu-id="808c5-170">You can use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="808c5-171">Pour plus d’informations, voir [Création de plusieurs instances à l’aide de la commande *copie*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="808c5-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="808c5-172">Vous pouvez également utiliser la commande `copyIndex()` pour ajouter un numéro à un nom de ressource.</span><span class="sxs-lookup"><span data-stu-id="808c5-172">You can also use `copyIndex()` to append a number to a resource name.</span></span> <span data-ttu-id="808c5-173">Vous pouvez ensuite créer les cartes *myNic1*, *MyNic2* et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="808c5-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="808c5-174">Voici un exemple de code pour l’ajout de la valeur d’index :</span><span class="sxs-lookup"><span data-stu-id="808c5-174">The following code shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="808c5-175">Vous pouvez consulter un exemple complet de la [création de plusieurs cartes d’interface réseau à l’aide de modèles Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="808c5-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="808c5-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="808c5-176">Next steps</span></span>
<span data-ttu-id="808c5-177">Réviser les [Tailles des machines virtuelles Windows](sizes.md) lorsque vous tentez de créer une machine virtuelle équipée de plusieurs cartes d’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="808c5-177">Review [Windows VM sizes](sizes.md) when you're trying to create a VM that has multiple NICs.</span></span> <span data-ttu-id="808c5-178">Faites attention au nombre maximal de cartes d’interface réseau pris en charge par chaque taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="808c5-178">Pay attention to the maximum number of NICs that each VM size supports.</span></span> 


