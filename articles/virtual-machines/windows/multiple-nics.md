---
title: "aaaCreate et gérer des machines virtuelles Windows dans Azure qui utilisent plusieurs cartes réseau | Documents Microsoft"
description: "Découvrez comment toocreate et gérer une machine virtuelle Windows qui a plusieurs tooit de cartes réseau attachée à l’aide de modèles Azure PowerShell ou le Gestionnaire de ressources."
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
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="af548-103">Créer et gérer une machine virtuelle Windows équipée de plusieurs cartes d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="af548-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="af548-104">Machines virtuelles (VM) dans Azure peut avoir plusieurs toothem de cartes (NIC) connectées interface réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="af548-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached toothem.</span></span> <span data-ttu-id="af548-105">Un scénario courant consiste à toohave des sous-réseaux différents pour la connectivité des serveurs frontale et principaux, ou un réseau dédié tooa analyse ou la solution de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="af548-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="af548-106">Cet article décrit en détail comment toocreate une machine virtuelle qui possède plusieurs cartes réseau connectée tooit.</span><span class="sxs-lookup"><span data-stu-id="af548-106">This article details how toocreate a VM that has multiple NICs attached tooit.</span></span> <span data-ttu-id="af548-107">Vous apprendrez également comment tooadd ou supprimer des cartes réseau à partir d’une machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="af548-107">You also learn how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="af548-108">Comme le nombre de cartes réseau prises en charge varie suivant la [taille des machines virtuelles](sizes.md) , pensez à dimensionner la vôtre en conséquence.</span><span class="sxs-lookup"><span data-stu-id="af548-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="af548-109">Pour plus d’informations, y compris toocreate plusieurs cartes réseau dans vos propres scripts PowerShell, voir [déploiement de machines virtuelles de plusieurs cartes](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="af548-109">For detailed information, including how toocreate multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af548-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="af548-110">Prerequisites</span></span>
<span data-ttu-id="af548-111">Assurez-vous que vous avez hello [dernière version de Azure PowerShell installé et configuré](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="af548-111">Make sure that you have hello [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="af548-112">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="af548-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="af548-113">Les noms de paramètre sont par exemple *myResourceGroup*, *myVnet* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="af548-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="af548-114">Créer une machine virtuelle avec plusieurs cartes d’interface réseau</span><span class="sxs-lookup"><span data-stu-id="af548-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="af548-115">Créez d’abord un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="af548-115">First, create a resource group.</span></span> <span data-ttu-id="af548-116">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *EastUs* emplacement :</span><span class="sxs-lookup"><span data-stu-id="af548-116">hello following example creates a resource group named *myResourceGroup* in hello *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="af548-117">Créer un réseau virtuel et des sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="af548-117">Create virtual network and subnets</span></span>
<span data-ttu-id="af548-118">Un scénario courant consiste pour un réseau virtuel de toohave deux ou plusieurs sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="af548-118">A common scenario is for a virtual network toohave two or more subnets.</span></span> <span data-ttu-id="af548-119">Un sous-réseau est peut-être pour le trafic frontal, hello autre pour le trafic du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="af548-119">One subnet may be for front-end traffic, hello other for back-end traffic.</span></span> <span data-ttu-id="af548-120">tooconnect tooboth sous-réseaux, vous utilisez ensuite plusieurs cartes réseau sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af548-120">tooconnect tooboth subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="af548-121">Définissez deux sous-réseaux de réseau virtuel avec la commande [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="af548-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="af548-122">Hello exemple suivant définit les sous-réseaux hello pour *mySubnetFrontEnd* et *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="af548-122">hello following example defines hello subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="af548-123">Créez votre réseau virtuel et vos sous-réseaux avec la commande [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="af548-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="af548-124">Hello exemple suivant crée un réseau virtuel nommé *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="af548-124">hello following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="af548-125">Créer plusieurs cartes réseau</span><span class="sxs-lookup"><span data-stu-id="af548-125">Create multiple NICs</span></span>
<span data-ttu-id="af548-126">Créez deux cartes d’interface réseau avec la commande [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="af548-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="af548-127">Attacher un sous-réseau frontal toohello de la carte réseau et un sous-réseau de principaux de toohello de carte réseau.</span><span class="sxs-lookup"><span data-stu-id="af548-127">Attach one NIC toohello front-end subnet and one NIC toohello back-end subnet.</span></span> <span data-ttu-id="af548-128">exemple Hello crée NIC nommé *myNic1* et *myNic2*:</span><span class="sxs-lookup"><span data-stu-id="af548-128">hello following example creates NICs named *myNic1* and *myNic2*:</span></span>

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

<span data-ttu-id="af548-129">En général, vous créez également un [groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md) ou [l’équilibrage de charge](../../load-balancer/load-balancer-overview.md) toohelp gérer et répartir le trafic entre vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="af548-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="af548-130">Hello [plus d’ordinateurs virtuels de plusieurs cartes](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article explique comment créer un groupe de sécurité réseau et l’affectation des cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="af548-130">hello [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="af548-131">Créer la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="af548-131">Create hello virtual machine</span></span>
<span data-ttu-id="af548-132">Maintenant démarrer toobuild votre configuration d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="af548-132">Now start toobuild your VM configuration.</span></span> <span data-ttu-id="af548-133">Chaque taille de machine virtuelle a une limite pour le nombre total de hello de cartes réseau que vous pouvez ajouter tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af548-133">Each VM size has a limit for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="af548-134">Pour plus d’informations, voir [Tailles des machines virtuelles Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="af548-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="af548-135">Définir votre toohello d’informations d’identification de machine virtuelle `$cred` variable comme suit :</span><span class="sxs-lookup"><span data-stu-id="af548-135">Set your VM credentials toohello `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="af548-136">Définissez votre machine virtuelle avec la commande [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span><span class="sxs-lookup"><span data-stu-id="af548-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="af548-137">Hello exemple suivant définit un ordinateur virtuel nommé *myVM* et utilise une taille de machine virtuelle qui prend en charge plus de deux cartes réseau (*Standard_DS3_v2*) :</span><span class="sxs-lookup"><span data-stu-id="af548-137">hello following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="af548-138">Créez reste hello de configuration de votre machine virtuelle avec [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) et [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span><span class="sxs-lookup"><span data-stu-id="af548-138">Create hello rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="af548-139">Bonjour à l’exemple suivant crée un ordinateur Windows Server 2016 :</span><span class="sxs-lookup"><span data-stu-id="af548-139">hello following example creates a Windows Server 2016 VM:</span></span>

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

4. <span data-ttu-id="af548-140">Attacher des cartes réseau hello deux que vous avez créé précédemment avec [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="af548-140">Attach hello two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="af548-141">Enfin, créez votre machine virtuelle avec la commande [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) :</span><span class="sxs-lookup"><span data-stu-id="af548-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a><span data-ttu-id="af548-142">Ajouter un tooan de carte réseau existante de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="af548-142">Add a NIC tooan existing VM</span></span>
<span data-ttu-id="af548-143">tooadd une carte réseau virtuelle tooan existant de machine virtuelle, vous libérer hello machine virtuelle, ajoutez hello carte réseau virtuelle, puis démarrer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af548-143">tooadd a virtual NIC tooan existing VM, you deallocate hello VM, add hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="af548-144">Désallouer hello machine virtuelle avec [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="af548-144">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="af548-145">exemple Hello désalloue hello ordinateur virtuel nommé *myVM* dans *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="af548-145">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="af548-146">Obtenir la configuration existante de hello Hello machine virtuelle avec [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="af548-146">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="af548-147">Hello exemple suivant obtient les informations pour hello ordinateur virtuel nommé *myVM* dans *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="af548-147">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="af548-148">Hello exemple suivant crée une carte réseau virtuelle avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) nommé *myNic3* qui est attaché trop*mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="af548-148">hello following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached too*mySubnetBackEnd*.</span></span> <span data-ttu-id="af548-149">Hello carte réseau virtuelle est ensuite jointe toohello ordinateur virtuel nommé *myVM* dans *myResourceGroup* avec [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="af548-149">hello virtual NIC is then attached toohello VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="af548-150">Cartes d’interface réseau virtuelles principales</span><span class="sxs-lookup"><span data-stu-id="af548-150">Primary virtual NICs</span></span>
    <span data-ttu-id="af548-151">Une des cartes réseau sur une machine virtuelle multi-NIC de hello doit toobe principal.</span><span class="sxs-lookup"><span data-stu-id="af548-151">One of hello NICs on a multi-NIC VM needs toobe primary.</span></span> <span data-ttu-id="af548-152">Si un des hello existant de cartes réseau virtuelles sur hello machine virtuelle est déjà défini comme principal, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="af548-152">If one of hello existing virtual NICs on hello VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="af548-153">Hello exemple suivant suppose que deux cartes réseau virtuelles est désormais présentes sur une machine virtuelle et que vous souhaitez tooadd hello la première carte réseau (`[0]`) en tant que hello principal :</span><span class="sxs-lookup"><span data-stu-id="af548-153">hello following example assumes that two virtual NICs are now present on a VM and you wish tooadd hello first NIC (`[0]`) as hello primary:</span></span>
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="af548-154">Démarrer hello machine virtuelle avec [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="af548-154">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="af548-155">Supprimer une carte réseau d’une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="af548-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="af548-156">tooremove une carte réseau virtuelle à partir d’un ordinateur virtuel existant, vous libérer hello machine virtuelle, supprimez hello carte réseau virtuelle, puis démarrer hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af548-156">tooremove a virtual NIC from an existing VM, you deallocate hello VM, remove hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="af548-157">Désallouer hello machine virtuelle avec [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="af548-157">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="af548-158">exemple Hello désalloue hello ordinateur virtuel nommé *myVM* dans *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="af548-158">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="af548-159">Obtenir la configuration existante de hello Hello machine virtuelle avec [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="af548-159">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="af548-160">Hello exemple suivant obtient les informations pour hello ordinateur virtuel nommé *myVM* dans *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="af548-160">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="af548-161">Obtenir des informations sur hello NIC supprimer avec [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="af548-161">Get information about hello NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="af548-162">Hello exemple suivant obtient des informations sur *myNic3*:</span><span class="sxs-lookup"><span data-stu-id="af548-162">hello following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="af548-163">Supprimer hello carte réseau avec [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) puis mettez à jour hello machine virtuelle avec [AzureRmVm de mise à jour](/powershell/module/azurerm.compute/update-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="af548-163">Remove hello NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update hello VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="af548-164">Hello exemple suivant supprime *myNic3* tels qu’obtenus par `$nicId` Bonjour précédant l’étape :</span><span class="sxs-lookup"><span data-stu-id="af548-164">hello following example removes *myNic3* as obtained by `$nicId` in hello preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="af548-165">Démarrer hello machine virtuelle avec [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="af548-165">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="af548-166">Créer plusieurs cartes d’interface réseau avec des modèles</span><span class="sxs-lookup"><span data-stu-id="af548-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="af548-167">Les modèles de gestionnaire de ressources Azure fournissent un toocreate de façon plusieurs instances d’une ressource pendant le déploiement, telles que la création de plusieurs cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="af548-167">Azure Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="af548-168">Modèles du Gestionnaire de ressources utilisent toodefine de fichiers JSON déclarative de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="af548-168">Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="af548-169">Pour plus d’informations, voir [Présentation d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="af548-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="af548-170">Vous pouvez utiliser *copie* nombre de hello toospecify de toocreate d’instances :</span><span class="sxs-lookup"><span data-stu-id="af548-170">You can use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="af548-171">Pour plus d’informations, voir [Création de plusieurs instances à l’aide de la commande *copie*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="af548-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="af548-172">Vous pouvez également utiliser `copyIndex()` tooappend un nom de ressource tooa nombre.</span><span class="sxs-lookup"><span data-stu-id="af548-172">You can also use `copyIndex()` tooappend a number tooa resource name.</span></span> <span data-ttu-id="af548-173">Vous pouvez ensuite créer les cartes *myNic1*, *MyNic2* et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="af548-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="af548-174">Hello de code suivant montre un exemple d’ajout de valeur d’index hello :</span><span class="sxs-lookup"><span data-stu-id="af548-174">hello following code shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="af548-175">Vous pouvez consulter un exemple complet de la [création de plusieurs cartes d’interface réseau à l’aide de modèles Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="af548-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="af548-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="af548-176">Next steps</span></span>
<span data-ttu-id="af548-177">Révision [tailles de machine virtuelle Windows](sizes.md) lorsque vous essayez de toocreate une machine virtuelle qui possède plusieurs cartes réseau.</span><span class="sxs-lookup"><span data-stu-id="af548-177">Review [Windows VM sizes](sizes.md) when you're trying toocreate a VM that has multiple NICs.</span></span> <span data-ttu-id="af548-178">Payer une attention toohello nombre de cartes réseau prenant en charge la taille de chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af548-178">Pay attention toohello maximum number of NICs that each VM size supports.</span></span> 


