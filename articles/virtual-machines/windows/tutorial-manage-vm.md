---
title: "aaaCreate et gérer des machines virtuelles Windows avec hello module Azure PowerShell | Documents Microsoft"
description: "Didacticiel : créer et gérer des machines virtuelles Windows avec hello module Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a><span data-ttu-id="920d8-103">Créer et gérer des machines virtuelles Windows avec hello module Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="920d8-103">Create and Manage Windows VMs with hello Azure PowerShell module</span></span>

<span data-ttu-id="920d8-104">Les machines virtuelles fournissent un environnement informatique entièrement configurable et flexible.</span><span class="sxs-lookup"><span data-stu-id="920d8-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="920d8-105">Ce didacticiel traite d’aspects de base du déploiement de machines virtuelles Azure, tels que la sélection d’une taille de machine virtuelle, la sélection d’une image de machine virtuelle et le déploiement d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="920d8-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="920d8-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="920d8-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="920d8-107">Créer et connecter tooa machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="920d8-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="920d8-108">Sélectionner et utiliser des images de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="920d8-108">Select and use VM images</span></span>
> * <span data-ttu-id="920d8-109">Afficher et utiliser des tailles de machine virtuelle spécifiques</span><span class="sxs-lookup"><span data-stu-id="920d8-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="920d8-110">Redimensionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="920d8-110">Resize a VM</span></span>
> * <span data-ttu-id="920d8-111">Consulter et comprendre l’état d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="920d8-111">View and understand VM state</span></span>

<span data-ttu-id="920d8-112">Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module.</span><span class="sxs-lookup"><span data-stu-id="920d8-112">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="920d8-113">Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="920d8-113">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="920d8-114">Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="920d8-114">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="920d8-115">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="920d8-115">Create resource group</span></span>

<span data-ttu-id="920d8-116">Créer un groupe de ressources avec hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) commande.</span><span class="sxs-lookup"><span data-stu-id="920d8-116">Create a resource group with hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> 

<span data-ttu-id="920d8-117">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="920d8-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="920d8-118">Un groupe de ressources doit être créé avant les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="920d8-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="920d8-119">Dans cet exemple, un groupe de ressources nommé *myResourceGroupVM* est créé dans hello *EastUS* région.</span><span class="sxs-lookup"><span data-stu-id="920d8-119">In this example, a resource group named *myResourceGroupVM* is created in hello *EastUS* region.</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

<span data-ttu-id="920d8-120">groupe de ressources Hello est spécifié lors de la création ou la modification d’une machine virtuelle, ce qui peut être vu dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="920d8-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="920d8-121">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="920d8-121">Create virtual machine</span></span>

<span data-ttu-id="920d8-122">Un ordinateur virtuel doit être connecté tooa des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="920d8-122">A virtual machine must be connected tooa virtual network.</span></span> <span data-ttu-id="920d8-123">Vous communiquez avec l’ordinateur virtuel de hello à l’aide d’une adresse IP publique via une carte d’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="920d8-123">You communicate with hello virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="920d8-124">Création d’un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="920d8-124">Create virtual network</span></span>

<span data-ttu-id="920d8-125">Créez un sous-réseau avec [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) :</span><span class="sxs-lookup"><span data-stu-id="920d8-125">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="920d8-126">Créez un réseau virtuel avec [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) :</span><span class="sxs-lookup"><span data-stu-id="920d8-126">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="920d8-127">Création d’une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="920d8-127">Create public IP address</span></span>

<span data-ttu-id="920d8-128">Créez une adresse IP publique avec [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) :</span><span class="sxs-lookup"><span data-stu-id="920d8-128">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="920d8-129">Création de la carte réseau</span><span class="sxs-lookup"><span data-stu-id="920d8-129">Create network interface card</span></span>

<span data-ttu-id="920d8-130">Créez une carte réseau avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) :</span><span class="sxs-lookup"><span data-stu-id="920d8-130">Create a network interface card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="920d8-131">Création d’un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="920d8-131">Create network security group</span></span>

<span data-ttu-id="920d8-132">Un [groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md) (NSG) Azure contrôle le trafic entrant et sortant pour une ou plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="920d8-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="920d8-133">Les règles de groupe de sécurité réseau autorisent ou refusent le trafic réseau sur un port ou une plage de ports spécifique.</span><span class="sxs-lookup"><span data-stu-id="920d8-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="920d8-134">Ces règles peuvent également inclure un préfixe d’adresse source afin que seul le trafic provenant d’une source prédéfinie puisse communiquer avec une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="920d8-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="920d8-135">tooaccess hello IIS serveur Web que vous installez, vous devez ajouter une règle entrante de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="920d8-135">tooaccess hello IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="920d8-136">toocreate une règle entrante de groupe de sécurité réseau, utilisez [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="920d8-136">toocreate an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="920d8-137">Hello exemple suivant crée une règle de groupe de sécurité réseau nommée *myNSGRule* qui ouvre le port *3389* pour la machine virtuelle de hello :</span><span class="sxs-lookup"><span data-stu-id="920d8-137">hello following example creates an NSG rule named *myNSGRule* that opens port *3389* for hello virtual machine:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

<span data-ttu-id="920d8-138">Créer à l’aide du groupe de sécurité réseau hello *myNSGRule* avec [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="920d8-138">Create hello NSG using *myNSGRule* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

<span data-ttu-id="920d8-139">Ajouter un sous-réseau de toohello de groupe de sécurité réseau hello dans le réseau virtuel hello [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="920d8-139">Add hello NSG toohello subnet in hello virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="920d8-140">Réseau virtuel de mise à jour hello avec [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="920d8-140">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="920d8-141">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="920d8-141">Create virtual machine</span></span>

<span data-ttu-id="920d8-142">Lorsque vous créez une machine virtuelle, plusieurs options sont disponibles, comme l’image de système d’exploitation, les informations d’identification d’administration ou le dimensionnement des disques.</span><span class="sxs-lookup"><span data-stu-id="920d8-142">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="920d8-143">Dans cet exemple, un ordinateur virtuel est créé avec un nom de *myVM* en cours d’exécution hello dernière version de Windows Server 2016 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="920d8-143">In this example, a virtual machine is created with a name of *myVM* running hello latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="920d8-144">Définir le nom d’utilisateur hello et le mot de passe pour le compte d’administrateur hello sur l’ordinateur virtuel de hello avec [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="920d8-144">Set hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="920d8-145">Créer la configuration initiale de l’ordinateur virtuel hello hello [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span><span class="sxs-lookup"><span data-stu-id="920d8-145">Create hello initial configuration for hello virtual machine with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="920d8-146">Ajouter une configuration de machine virtuelle hello système d’exploitation informations toohello avec [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span><span class="sxs-lookup"><span data-stu-id="920d8-146">Add hello operating system information toohello virtual machine configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="920d8-147">Ajouter la configuration d’ordinateur virtuel hello image informations toohello avec [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span><span class="sxs-lookup"><span data-stu-id="920d8-147">Add hello image information toohello virtual machine configuration with [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

<span data-ttu-id="920d8-148">Ajouter hello système d’exploitation disque paramètres toohello configuration d’ordinateur virtuel avec [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span><span class="sxs-lookup"><span data-stu-id="920d8-148">Add hello operating system disk settings toohello virtual machine configuration with [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

<span data-ttu-id="920d8-149">Ajouter hello carte réseau que vous avez créé précédemment toohello configuration d’ordinateur virtuel avec [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="920d8-149">Add hello network interface card that you previously created toohello virtual machine configuration with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="920d8-150">Créer la machine virtuelle hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="920d8-150">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a><span data-ttu-id="920d8-151">Se connecter tooVM</span><span class="sxs-lookup"><span data-stu-id="920d8-151">Connect tooVM</span></span>

<span data-ttu-id="920d8-152">Après que le déploiement de hello terminée, créez une connexion Bureau à distance avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="920d8-152">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="920d8-153">Exécutez hello suivant de commandes tooreturn hello adresse IP publique de l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="920d8-153">Run hello following commands tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="920d8-154">Prenez note de cette adresse IP pour pouvoir vous connecter tooit reliées votre navigateur tootest web dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="920d8-154">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

<span data-ttu-id="920d8-155">La commande suivante de hello utilisation toocreate une session Bureau à distance avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="920d8-155">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="920d8-156">Remplacer l’adresse IP de hello avec hello *publicIPAddress* de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="920d8-156">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="920d8-157">Lorsque vous y êtes invité, entrez les informations d’identification de l’hello utilisées lors de la création d’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="920d8-157">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a><span data-ttu-id="920d8-158">Comprendre les images de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="920d8-158">Understand VM images</span></span>

<span data-ttu-id="920d8-159">Bonjour Azure marketplace inclut plusieurs images de machine virtuelle qui peuvent être utilisé toocreate un nouvel ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="920d8-159">hello Azure marketplace includes many virtual machine images that can be used toocreate a new virtual machine.</span></span> <span data-ttu-id="920d8-160">Dans les étapes précédentes hello, un ordinateur virtuel a été créé à l’aide d’image de Windows Server 2016-Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="920d8-160">In hello previous steps, a virtual machine was created using hello Windows Server 2016-Datacenter image.</span></span> <span data-ttu-id="920d8-161">Dans cette étape, le module PowerShell de hello est marketplace de hello toosearch utilisé pour les autres images de Windows, qui peut également comme base pour les nouvelles machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="920d8-161">In this step, hello PowerShell module is used toosearch hello marketplace for other Windows images, which can also as a base for new VMs.</span></span> <span data-ttu-id="920d8-162">Ce processus se compose de recherche de serveur de publication hello, offre et le nom d’image hello (référence Sku).</span><span class="sxs-lookup"><span data-stu-id="920d8-162">This process consists of finding hello publisher, offer, and hello image name (Sku).</span></span> 

<span data-ttu-id="920d8-163">Hello d’utilisation [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) commande tooreturn une liste des serveurs de publication de l’image.</span><span class="sxs-lookup"><span data-stu-id="920d8-163">Use hello [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command tooreturn a list of image publishers.</span></span>  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

<span data-ttu-id="920d8-164">Hello d’utilisation [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn une liste des offres de l’image.</span><span class="sxs-lookup"><span data-stu-id="920d8-164">Use hello [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn a list of image offers.</span></span> <span data-ttu-id="920d8-165">Avec cette commande, hello retourné la liste est filtrée sur le serveur de publication spécifié hello.</span><span class="sxs-lookup"><span data-stu-id="920d8-165">With this command, hello returned list is filtered on hello specified publisher.</span></span> 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

<span data-ttu-id="920d8-166">Hello [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) commande puis filtre sur tooreturn de nom de serveur de publication et offre hello une liste de noms d’images.</span><span class="sxs-lookup"><span data-stu-id="920d8-166">hello [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) command will then filter on hello publisher and offer name tooreturn a list of image names.</span></span>

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

<span data-ttu-id="920d8-167">Ces informations peuvent être utilisée toodeploy une machine virtuelle avec une image spécifique.</span><span class="sxs-lookup"><span data-stu-id="920d8-167">This information can be used toodeploy a VM with a specific image.</span></span> <span data-ttu-id="920d8-168">Cet exemple définit le nom de l’image hello sur l’objet de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="920d8-168">This example sets hello image name on hello VM object.</span></span> <span data-ttu-id="920d8-169">Consultez les exemples précédents toohello dans ce didacticiel pour les étapes de déploiement complet.</span><span class="sxs-lookup"><span data-stu-id="920d8-169">Refer toohello previous examples in this tutorial for complete deployment steps.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="920d8-170">Comprendre les tailles de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="920d8-170">Understand VM sizes</span></span>

<span data-ttu-id="920d8-171">Une taille de machine virtuelle détermine hello des ressources de calcul tels que le processeur et mémoire GPU apportées virtuels toohello disponibles.</span><span class="sxs-lookup"><span data-stu-id="920d8-171">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="920d8-172">Machines virtuelles doivent toobe créé avec une taille appropriée pour hello attendent la charge de travail.</span><span class="sxs-lookup"><span data-stu-id="920d8-172">Virtual machines need toobe created with a size appropriate for hello expect work load.</span></span> <span data-ttu-id="920d8-173">Si la charge de travail augmente, une machine virtuelle existante peut être redimensionnée.</span><span class="sxs-lookup"><span data-stu-id="920d8-173">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="920d8-174">Tailles de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="920d8-174">VM Sizes</span></span>

<span data-ttu-id="920d8-175">Hello tableau suivant catégorise les tailles en cas d’usage.</span><span class="sxs-lookup"><span data-stu-id="920d8-175">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="920d8-176">Type</span><span class="sxs-lookup"><span data-stu-id="920d8-176">Type</span></span>                     | <span data-ttu-id="920d8-177">Tailles</span><span class="sxs-lookup"><span data-stu-id="920d8-177">Sizes</span></span>           |    <span data-ttu-id="920d8-178">Description</span><span class="sxs-lookup"><span data-stu-id="920d8-178">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="920d8-179">Usage général</span><span class="sxs-lookup"><span data-stu-id="920d8-179">General purpose</span></span>         |<span data-ttu-id="920d8-180">DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="920d8-180">DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="920d8-181">Ratio processeur/mémoire équilibré.</span><span class="sxs-lookup"><span data-stu-id="920d8-181">Balanced CPU-to-memory.</span></span> <span data-ttu-id="920d8-182">La solution idéale pour le développement / test et des solutions d’applications et des données toomedium petit.</span><span class="sxs-lookup"><span data-stu-id="920d8-182">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| <span data-ttu-id="920d8-183">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="920d8-183">Compute optimized</span></span>      | <span data-ttu-id="920d8-184">Fs, F</span><span class="sxs-lookup"><span data-stu-id="920d8-184">Fs, F</span></span>             | <span data-ttu-id="920d8-185">Ratio processeur/mémoire élevé.</span><span class="sxs-lookup"><span data-stu-id="920d8-185">High CPU-to-memory.</span></span> <span data-ttu-id="920d8-186">Convient pour les applications au trafic moyen, les appliances réseau et les processus de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="920d8-186">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| <span data-ttu-id="920d8-187">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="920d8-187">Memory optimized</span></span>       | <span data-ttu-id="920d8-188">GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="920d8-188">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="920d8-189">Ratio mémoire/cœur élevé.</span><span class="sxs-lookup"><span data-stu-id="920d8-189">High memory-to-core.</span></span> <span data-ttu-id="920d8-190">Idéal pour les bases de données relationnelles, les caches toolarge moyenne et en mémoire analytique.</span><span class="sxs-lookup"><span data-stu-id="920d8-190">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| <span data-ttu-id="920d8-191">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="920d8-191">Storage optimized</span></span>       | <span data-ttu-id="920d8-192">Ls</span><span class="sxs-lookup"><span data-stu-id="920d8-192">Ls</span></span>                | <span data-ttu-id="920d8-193">Débit de disque et E/S élevés.</span><span class="sxs-lookup"><span data-stu-id="920d8-193">High disk throughput and IO.</span></span> <span data-ttu-id="920d8-194">Idéale pour les bases de données NoSQL, SQL et Big Data.</span><span class="sxs-lookup"><span data-stu-id="920d8-194">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| <span data-ttu-id="920d8-195">GPU</span><span class="sxs-lookup"><span data-stu-id="920d8-195">GPU</span></span>           | <span data-ttu-id="920d8-196">NV, NC</span><span class="sxs-lookup"><span data-stu-id="920d8-196">NV, NC</span></span>            | <span data-ttu-id="920d8-197">Machines virtuelles spécialisées conçues pour les opérations graphiques lourdes et la retouche vidéo.</span><span class="sxs-lookup"><span data-stu-id="920d8-197">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| <span data-ttu-id="920d8-198">Hautes performances</span><span class="sxs-lookup"><span data-stu-id="920d8-198">High performance</span></span> | <span data-ttu-id="920d8-199">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="920d8-199">H, A8-11</span></span>          | <span data-ttu-id="920d8-200">Nos machines virtuelles dotées des processeurs les plus puissants avec interfaces réseau haut débit en option (RDMA).</span><span class="sxs-lookup"><span data-stu-id="920d8-200">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="920d8-201">Rechercher les tailles de machines virtuelles disponibles</span><span class="sxs-lookup"><span data-stu-id="920d8-201">Find available VM sizes</span></span>

<span data-ttu-id="920d8-202">toosee une liste des ordinateurs virtuels des tailles disponibles dans une région particulière, utilisez hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) commande.</span><span class="sxs-lookup"><span data-stu-id="920d8-202">toosee a list of VM sizes available in a particular region, use hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command.</span></span>

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a><span data-ttu-id="920d8-203">Redimensionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="920d8-203">Resize a VM</span></span>

<span data-ttu-id="920d8-204">Après avoir déployé une machine virtuelle, il peut être redimensionné tooincrease ou diminuer l’allocation de ressources.</span><span class="sxs-lookup"><span data-stu-id="920d8-204">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="920d8-205">Avant de redimensionner une machine virtuelle, vérifiez si hello taille souhaitée est disponible sur le cluster d’ordinateurs virtuels en cours hello.</span><span class="sxs-lookup"><span data-stu-id="920d8-205">Before resizing a VM, check if hello desired size is available on hello current VM cluster.</span></span> <span data-ttu-id="920d8-206">Hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) commande renvoie une liste de tailles.</span><span class="sxs-lookup"><span data-stu-id="920d8-206">hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command returns a list of sizes.</span></span> 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

<span data-ttu-id="920d8-207">Si hello souhaité de taille n’est disponible, hello machine virtuelle peut être redimensionnée à partir d’un état sous tension, mais il est redémarré au cours de l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="920d8-207">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

<span data-ttu-id="920d8-208">Si vous le souhaitez hello taille n’est pas sur le cluster actuel hello, hello VM besoins toobe libérée avant que l’opération de redimensionnement hello peut se produire.</span><span class="sxs-lookup"><span data-stu-id="920d8-208">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="920d8-209">Notez que, quand hello VM est sous tension précédent, toutes les données sur le disque temporaire de hello sont supprimées et adresse IP publique de hello modifier, sauf si une adresse IP statique est utilisée.</span><span class="sxs-lookup"><span data-stu-id="920d8-209">Note, when hello VM is powered back on, any data on hello temp disk are removed, and hello public IP address change unless a static IP address is being used.</span></span> 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a><span data-ttu-id="920d8-210">États d’alimentation de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="920d8-210">VM power states</span></span>

<span data-ttu-id="920d8-211">Une machine virtuelle Azure peut présenter différents états d’alimentation.</span><span class="sxs-lookup"><span data-stu-id="920d8-211">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="920d8-212">Cet état représente état actuel de hello Hello machine virtuelle à partir du point de vue hello de hello hyperviseur.</span><span class="sxs-lookup"><span data-stu-id="920d8-212">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="920d8-213">États d’alimentation</span><span class="sxs-lookup"><span data-stu-id="920d8-213">Power states</span></span>

| <span data-ttu-id="920d8-214">État d’alimentation</span><span class="sxs-lookup"><span data-stu-id="920d8-214">Power State</span></span> | <span data-ttu-id="920d8-215">Description</span><span class="sxs-lookup"><span data-stu-id="920d8-215">Description</span></span>
|----|----|
| <span data-ttu-id="920d8-216">Starting</span><span class="sxs-lookup"><span data-stu-id="920d8-216">Starting</span></span> | <span data-ttu-id="920d8-217">Indique l’ordinateur virtuel de hello est en cours de démarrage.</span><span class="sxs-lookup"><span data-stu-id="920d8-217">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="920d8-218">Exécution</span><span class="sxs-lookup"><span data-stu-id="920d8-218">Running</span></span> | <span data-ttu-id="920d8-219">Indique que l’ordinateur virtuel hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="920d8-219">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="920d8-220">En cours d’arrêt</span><span class="sxs-lookup"><span data-stu-id="920d8-220">Stopping</span></span> | <span data-ttu-id="920d8-221">Indique que l’ordinateur virtuel hello est en cours d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="920d8-221">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="920d8-222">Arrêté</span><span class="sxs-lookup"><span data-stu-id="920d8-222">Stopped</span></span> | <span data-ttu-id="920d8-223">Indique que l’ordinateur virtuel hello est arrêté.</span><span class="sxs-lookup"><span data-stu-id="920d8-223">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="920d8-224">Notez que les ordinateurs virtuels en état de hello arrêté peut toujours occasionner des frais de calcul.</span><span class="sxs-lookup"><span data-stu-id="920d8-224">Note that virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="920d8-225">Libération</span><span class="sxs-lookup"><span data-stu-id="920d8-225">Deallocating</span></span> | <span data-ttu-id="920d8-226">Indique que l’ordinateur virtuel hello est désalloué.</span><span class="sxs-lookup"><span data-stu-id="920d8-226">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="920d8-227">Libéré</span><span class="sxs-lookup"><span data-stu-id="920d8-227">Deallocated</span></span> | <span data-ttu-id="920d8-228">Indique que l’ordinateur virtuel hello est entièrement supprimé du hyperviseur hello mais restent disponibles dans le plan de contrôle hello.</span><span class="sxs-lookup"><span data-stu-id="920d8-228">Indicates that hello virtual machine is completely removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="920d8-229">Machines virtuelles dans hello désallouée état n’entraînent aucun frais de calcul.</span><span class="sxs-lookup"><span data-stu-id="920d8-229">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="920d8-230">Indique que l’état de l’alimentation de l’ordinateur virtuel de hello hello est inconnu.</span><span class="sxs-lookup"><span data-stu-id="920d8-230">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="920d8-231">Rechercher un état d’alimentation</span><span class="sxs-lookup"><span data-stu-id="920d8-231">Find power state</span></span>

<span data-ttu-id="920d8-232">état de hello tooretrieve d’un ordinateur virtuel, utilisez hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) commande.</span><span class="sxs-lookup"><span data-stu-id="920d8-232">tooretrieve hello state of a particular VM, use hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span> <span data-ttu-id="920d8-233">Être vraiment toospecify un nom valide pour un ordinateur virtuel et le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="920d8-233">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

<span data-ttu-id="920d8-234">Output:</span><span class="sxs-lookup"><span data-stu-id="920d8-234">Output:</span></span>

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a><span data-ttu-id="920d8-235">Tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="920d8-235">Management tasks</span></span>

<span data-ttu-id="920d8-236">Au cours de hello du cycle de vie d’un ordinateur virtuel, vous souhaiterez toorun des tâches de gestion telles que le démarrage, arrêt ou suppression d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="920d8-236">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="920d8-237">En outre, vous souhaiterez toocreate scripts tooautomate répétitives ou complexes des tâches.</span><span class="sxs-lookup"><span data-stu-id="920d8-237">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="920d8-238">À l’aide d’Azure PowerShell, nombreuses tâches courantes de gestion peuvent être exécutées à partir de la ligne de commande hello ou dans des scripts.</span><span class="sxs-lookup"><span data-stu-id="920d8-238">Using Azure PowerShell, many common management tasks can be run from hello command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="920d8-239">Arrêt d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="920d8-239">Stop virtual machine</span></span>

<span data-ttu-id="920d8-240">Arrêtez et libérez une machine virtuelle avec [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) :</span><span class="sxs-lookup"><span data-stu-id="920d8-240">Stop and deallocate a virtual machine with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

<span data-ttu-id="920d8-241">Si vous voulez tookeep hello virtual machine dans un état configuré, utilisez le paramètre de - StayProvisioned de hello.</span><span class="sxs-lookup"><span data-stu-id="920d8-241">If you want tookeep hello virtual machine in a provisioned state, use hello -StayProvisioned parameter.</span></span>

### <a name="start-virtual-machine"></a><span data-ttu-id="920d8-242">Démarrage d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="920d8-242">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="920d8-243">Supprimer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="920d8-243">Delete resource group</span></span>

<span data-ttu-id="920d8-244">La suppression d’un groupe de ressources supprime également toutes les ressources qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="920d8-244">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a><span data-ttu-id="920d8-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="920d8-245">Next steps</span></span>

<span data-ttu-id="920d8-246">Ce didacticiel vous a montré les tâches de base de création et de gestion de machines virtuelles, notamment :</span><span class="sxs-lookup"><span data-stu-id="920d8-246">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="920d8-247">Créer et connecter tooa machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="920d8-247">Create and connect tooa VM</span></span>
> * <span data-ttu-id="920d8-248">Sélectionner et utiliser des images de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="920d8-248">Select and use VM images</span></span>
> * <span data-ttu-id="920d8-249">Afficher et utiliser des tailles de machine virtuelle spécifiques</span><span class="sxs-lookup"><span data-stu-id="920d8-249">View and use specific VM sizes</span></span>
> * <span data-ttu-id="920d8-250">Redimensionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="920d8-250">Resize a VM</span></span>
> * <span data-ttu-id="920d8-251">Consulter et comprendre l’état d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="920d8-251">View and understand VM state</span></span>

<span data-ttu-id="920d8-252">Avance toohello toolearn de didacticiel suivant sur les disques de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="920d8-252">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="920d8-253">Créer et gérer des disques de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="920d8-253">Create and Manage VM disks</span></span>](./tutorial-manage-data-disk.md)
