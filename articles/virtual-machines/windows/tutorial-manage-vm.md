---
title: "Créer et gérer des machines virtuelles Windows avec le module Azure PowerShell | Microsoft Docs"
description: "Didacticiel : créer et gérer des machines virtuelles Windows avec le module Azure PowerShell"
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
ms.openlocfilehash: ec1bb7834beb66dc28dd5b1db764bd358243292c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-windows-vms-with-the-azure-powershell-module"></a><span data-ttu-id="5d0e6-103">Créer et gérer des machines virtuelles Windows avec le module Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d0e6-103">Create and Manage Windows VMs with the Azure PowerShell module</span></span>

<span data-ttu-id="5d0e6-104">Les machines virtuelles fournissent un environnement informatique entièrement configurable et flexible.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="5d0e6-105">Ce didacticiel traite d’aspects de base du déploiement de machines virtuelles Azure, tels que la sélection d’une taille de machine virtuelle, la sélection d’une image de machine virtuelle et le déploiement d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="5d0e6-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5d0e6-107">Créer une machine virtuelle et vous y connecter</span><span class="sxs-lookup"><span data-stu-id="5d0e6-107">Create and connect to a VM</span></span>
> * <span data-ttu-id="5d0e6-108">Sélectionner et utiliser des images de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5d0e6-108">Select and use VM images</span></span>
> * <span data-ttu-id="5d0e6-109">Afficher et utiliser des tailles de machine virtuelle spécifiques</span><span class="sxs-lookup"><span data-stu-id="5d0e6-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="5d0e6-110">Redimensionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5d0e6-110">Resize a VM</span></span>
> * <span data-ttu-id="5d0e6-111">Consulter et comprendre l’état d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5d0e6-111">View and understand VM state</span></span>

<span data-ttu-id="5d0e6-112">Ce didacticiel requiert le module Azure PowerShell version 3.6 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-112">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="5d0e6-113">Exécutez ` Get-Module -ListAvailable AzureRM` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-113">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="5d0e6-114">Si vous devez effectuer une mise à niveau, consultez [Installer le module Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="5d0e6-114">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="5d0e6-115">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="5d0e6-115">Create resource group</span></span>

<span data-ttu-id="5d0e6-116">Créez un groupe de ressources avec la commande [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="5d0e6-116">Create a resource group with the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> 

<span data-ttu-id="5d0e6-117">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="5d0e6-118">Un groupe de ressources doit être créé avant les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="5d0e6-119">Dans cet exemple, un groupe de ressources nommé *myResourceGroupVM* est créé dans la région *EastUS*.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-119">In this example, a resource group named *myResourceGroupVM* is created in the *EastUS* region.</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

<span data-ttu-id="5d0e6-120">Le groupe de ressources est spécifié lors de la création ou de la modification d’une machine virtuelle, qui peut être vue dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-120">The resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="5d0e6-121">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="5d0e6-121">Create virtual machine</span></span>

<span data-ttu-id="5d0e6-122">Une machine virtuelle doit être connectée à un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-122">A virtual machine must be connected to a virtual network.</span></span> <span data-ttu-id="5d0e6-123">Vous communiquez avec la machine virtuelle à l’aide d’une adresse IP publique via une carte réseau (NIC).</span><span class="sxs-lookup"><span data-stu-id="5d0e6-123">You communicate with the virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="5d0e6-124">Création d’un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="5d0e6-124">Create virtual network</span></span>

<span data-ttu-id="5d0e6-125">Créez un sous-réseau avec [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-125">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="5d0e6-126">Créez un réseau virtuel avec [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-126">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="5d0e6-127">Création d’une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="5d0e6-127">Create public IP address</span></span>

<span data-ttu-id="5d0e6-128">Créez une adresse IP publique avec [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-128">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="5d0e6-129">Création de la carte réseau</span><span class="sxs-lookup"><span data-stu-id="5d0e6-129">Create network interface card</span></span>

<span data-ttu-id="5d0e6-130">Créez une carte réseau avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-130">Create a network interface card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="5d0e6-131">Création d’un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="5d0e6-131">Create network security group</span></span>

<span data-ttu-id="5d0e6-132">Un [groupe de sécurité réseau](../../virtual-network/virtual-networks-nsg.md) (NSG) Azure contrôle le trafic entrant et sortant pour une ou plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="5d0e6-133">Les règles de groupe de sécurité réseau autorisent ou refusent le trafic réseau sur un port ou une plage de ports spécifique.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="5d0e6-134">Ces règles peuvent également inclure un préfixe d’adresse source afin que seul le trafic provenant d’une source prédéfinie puisse communiquer avec une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="5d0e6-135">Pour accéder au serveur web IIS que vous installez, vous devez ajouter une règle de groupe de sécurité réseau entrante.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-135">To access the IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="5d0e6-136">Pour créer une règle de groupe de sécurité réseau entrante, utilisez [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="5d0e6-136">To create an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="5d0e6-137">L’exemple suivant crée une règle de groupe de sécurité réseau nommée *myNSGRule* qui ouvre le port *3389* pour la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-137">The following example creates an NSG rule named *myNSGRule* that opens port *3389* for the virtual machine:</span></span>

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

<span data-ttu-id="5d0e6-138">Créez le groupe de sécurité réseau *myNSGRule* avec [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-138">Create the NSG using *myNSGRule* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

<span data-ttu-id="5d0e6-139">Ajoutez le groupe de sécurité réseau au sous-groupe dans le réseau virtuel avec [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-139">Add the NSG to the subnet in the virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="5d0e6-140">Mettez à jour le réseau virtuel avec [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-140">Update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="5d0e6-141">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="5d0e6-141">Create virtual machine</span></span>

<span data-ttu-id="5d0e6-142">Lorsque vous créez une machine virtuelle, plusieurs options sont disponibles, comme l’image de système d’exploitation, les informations d’identification d’administration ou le dimensionnement des disques.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-142">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="5d0e6-143">Dans cet exemple, une machine virtuelle est créée avec le nom *myVM* ; elle exécute la dernière version de Windows Server 2016 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-143">In this example, a virtual machine is created with a name of *myVM* running the latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="5d0e6-144">Définissez le nom d’utilisateur et le mot de passe pour le compte d’administrateur sur la machine virtuelle avec [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-144">Set the username and password needed for the administrator account on the virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="5d0e6-145">Créez la configuration initiale de la machine virtuelle avec [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-145">Create the initial configuration for the virtual machine with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="5d0e6-146">Ajoutez les informations relatives au système d’exploitation à la configuration de la machine virtuelle avec [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-146">Add the operating system information to the virtual machine configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="5d0e6-147">Ajoutez les informations relatives à l’image à la configuration de la machine virtuelle avec [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-147">Add the image information to the virtual machine configuration with [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

<span data-ttu-id="5d0e6-148">Ajoutez les paramètres du disque du système d’exploitation à la configuration de la machine virtuelle avec [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-148">Add the operating system disk settings to the virtual machine configuration with [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

<span data-ttu-id="5d0e6-149">Ajoutez la carte réseau que vous avez créée précédemment à la configuration de la machine virtuelle avec [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-149">Add the network interface card that you previously created to the virtual machine configuration with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="5d0e6-150">Créez la machine virtuelle avec [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="5d0e6-150">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-to-vm"></a><span data-ttu-id="5d0e6-151">Se connecter à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5d0e6-151">Connect to VM</span></span>

<span data-ttu-id="5d0e6-152">Une fois le déploiement terminé, créez une connexion Bureau à distance avec la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-152">After the deployment has completed, create a remote desktop connection with the virtual machine.</span></span>

<span data-ttu-id="5d0e6-153">Exécutez les commandes suivantes pour renvoyer l’adresse IP publique de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-153">Run the following commands to return the public IP address of the virtual machine.</span></span> <span data-ttu-id="5d0e6-154">Prenez note de cette adresse IP, afin de pouvoir vous y connecter ultérieurement avec votre navigateur de manière à tester la connectivité web.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-154">Take note of this IP Address so you can connect to it with your browser to test web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

<span data-ttu-id="5d0e6-155">Utilisez la commande suivante pour créer une session Bureau à distance avec la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-155">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="5d0e6-156">Remplacez l’adresse IP par l’adresse *publicIPAddress* de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-156">Replace the IP address with the *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="5d0e6-157">À l'invite, saisissez les informations d’identification que vous avez utilisées lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-157">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a><span data-ttu-id="5d0e6-158">Comprendre les images de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5d0e6-158">Understand VM images</span></span>

<span data-ttu-id="5d0e6-159">La Place de marché Azure comprend de nombreuses images de machine virtuelle qui permettent de créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-159">The Azure marketplace includes many virtual machine images that can be used to create a new virtual machine.</span></span> <span data-ttu-id="5d0e6-160">Dans les étapes précédentes, une machine virtuelle a été créée à l’aide de l’image Windows Server 2016 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-160">In the previous steps, a virtual machine was created using the Windows Server 2016-Datacenter image.</span></span> <span data-ttu-id="5d0e6-161">Dans cette étape, le module PowerShell est utilisé pour rechercher d’autres images Windows dans la place de marché, qui peuvent également servir de base pour les nouvelles machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-161">In this step, the PowerShell module is used to search the marketplace for other Windows images, which can also as a base for new VMs.</span></span> <span data-ttu-id="5d0e6-162">Ce processus consiste à rechercher l’éditeur, l’offre et le nom de l’image (SKU).</span><span class="sxs-lookup"><span data-stu-id="5d0e6-162">This process consists of finding the publisher, offer, and the image name (Sku).</span></span> 

<span data-ttu-id="5d0e6-163">Utilisez la commande [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) pour retourner une liste d’éditeurs d’images.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-163">Use the [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command to return a list of image publishers.</span></span>  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

<span data-ttu-id="5d0e6-164">Utilisez la commande [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) pour retourner une liste d’offres d’images.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-164">Use the [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) to return a list of image offers.</span></span> <span data-ttu-id="5d0e6-165">Cette commande permet de filtrer la liste retournée en fonction de l’éditeur spécifié.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-165">With this command, the returned list is filtered on the specified publisher.</span></span> 

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

<span data-ttu-id="5d0e6-166">La commande [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) filtre ensuite les résultats en fonction du nom de l’éditeur et de l’offre pour retourner une liste de noms d’images.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-166">The [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) command will then filter on the publisher and offer name to return a list of image names.</span></span>

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

<span data-ttu-id="5d0e6-167">Ces informations peuvent être utilisées pour déployer une machine virtuelle avec une image spécifique.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-167">This information can be used to deploy a VM with a specific image.</span></span> <span data-ttu-id="5d0e6-168">Cet exemple définit le nom de l’image sur l’objet de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-168">This example sets the image name on the VM object.</span></span> <span data-ttu-id="5d0e6-169">Reportez-vous aux exemples indiqués précédemment dans ce didacticiel pour effectuer les étapes de déploiement.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-169">Refer to the previous examples in this tutorial for complete deployment steps.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="5d0e6-170">Comprendre les tailles de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5d0e6-170">Understand VM sizes</span></span>

<span data-ttu-id="5d0e6-171">Une taille de machine virtuelle détermine la quantité de ressources de calcul comme le processeur, le processeur graphique (GPU) et la mémoire qui sont mises à la disposition de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-171">A virtual machine size determines the amount of compute resources such as CPU, GPU, and memory that are made available to the virtual machine.</span></span> <span data-ttu-id="5d0e6-172">Les machines virtuelles doivent être créées avec une taille adaptée à la charge de travail attendue.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-172">Virtual machines need to be created with a size appropriate for the expect work load.</span></span> <span data-ttu-id="5d0e6-173">Si la charge de travail augmente, une machine virtuelle existante peut être redimensionnée.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-173">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="5d0e6-174">Tailles de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5d0e6-174">VM Sizes</span></span>

<span data-ttu-id="5d0e6-175">Le tableau suivant classe les tailles en fonction des cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-175">The following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="5d0e6-176">Type</span><span class="sxs-lookup"><span data-stu-id="5d0e6-176">Type</span></span>                     | <span data-ttu-id="5d0e6-177">Tailles</span><span class="sxs-lookup"><span data-stu-id="5d0e6-177">Sizes</span></span>           |    <span data-ttu-id="5d0e6-178">Description</span><span class="sxs-lookup"><span data-stu-id="5d0e6-178">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5d0e6-179">Usage général</span><span class="sxs-lookup"><span data-stu-id="5d0e6-179">General purpose</span></span>         |<span data-ttu-id="5d0e6-180">DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="5d0e6-180">DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="5d0e6-181">Ratio processeur/mémoire équilibré.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-181">Balanced CPU-to-memory.</span></span> <span data-ttu-id="5d0e6-182">Idéale pour le développement/test et pour les petites et moyennes applications et solutions de données.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-182">Ideal for dev / test and small to medium applications and data solutions.</span></span>  |
| <span data-ttu-id="5d0e6-183">Optimisé pour le calcul</span><span class="sxs-lookup"><span data-stu-id="5d0e6-183">Compute optimized</span></span>      | <span data-ttu-id="5d0e6-184">Fs, F</span><span class="sxs-lookup"><span data-stu-id="5d0e6-184">Fs, F</span></span>             | <span data-ttu-id="5d0e6-185">Ratio processeur/mémoire élevé.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-185">High CPU-to-memory.</span></span> <span data-ttu-id="5d0e6-186">Convient pour les applications au trafic moyen, les appliances réseau et les processus de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-186">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| <span data-ttu-id="5d0e6-187">Mémoire optimisée</span><span class="sxs-lookup"><span data-stu-id="5d0e6-187">Memory optimized</span></span>       | <span data-ttu-id="5d0e6-188">GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="5d0e6-188">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="5d0e6-189">Ratio mémoire/cœur élevé.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-189">High memory-to-core.</span></span> <span data-ttu-id="5d0e6-190">Idéale pour les bases de données relationnelles, les caches moyens à grands et l’analytique en mémoire.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-190">Great for relational databases, medium to large caches, and in-memory analytics.</span></span>                 |
| <span data-ttu-id="5d0e6-191">Optimisé pour le stockage</span><span class="sxs-lookup"><span data-stu-id="5d0e6-191">Storage optimized</span></span>       | <span data-ttu-id="5d0e6-192">Ls</span><span class="sxs-lookup"><span data-stu-id="5d0e6-192">Ls</span></span>                | <span data-ttu-id="5d0e6-193">Débit de disque et E/S élevés.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-193">High disk throughput and IO.</span></span> <span data-ttu-id="5d0e6-194">Idéale pour les bases de données NoSQL, SQL et Big Data.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-194">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| <span data-ttu-id="5d0e6-195">GPU</span><span class="sxs-lookup"><span data-stu-id="5d0e6-195">GPU</span></span>           | <span data-ttu-id="5d0e6-196">NV, NC</span><span class="sxs-lookup"><span data-stu-id="5d0e6-196">NV, NC</span></span>            | <span data-ttu-id="5d0e6-197">Machines virtuelles spécialisées conçues pour les opérations graphiques lourdes et la retouche vidéo.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-197">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| <span data-ttu-id="5d0e6-198">Hautes performances</span><span class="sxs-lookup"><span data-stu-id="5d0e6-198">High performance</span></span> | <span data-ttu-id="5d0e6-199">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="5d0e6-199">H, A8-11</span></span>          | <span data-ttu-id="5d0e6-200">Nos machines virtuelles dotées des processeurs les plus puissants avec interfaces réseau haut débit en option (RDMA).</span><span class="sxs-lookup"><span data-stu-id="5d0e6-200">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="5d0e6-201">Rechercher les tailles de machines virtuelles disponibles</span><span class="sxs-lookup"><span data-stu-id="5d0e6-201">Find available VM sizes</span></span>

<span data-ttu-id="5d0e6-202">Pour afficher la liste des tailles de machines virtuelles disponibles dans une région particulière, utilisez la commande [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize).</span><span class="sxs-lookup"><span data-stu-id="5d0e6-202">To see a list of VM sizes available in a particular region, use the [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command.</span></span>

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a><span data-ttu-id="5d0e6-203">Redimensionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5d0e6-203">Resize a VM</span></span>

<span data-ttu-id="5d0e6-204">Après avoir déployé une machine virtuelle, vous pouvez la redimensionner pour augmenter ou diminuer l’allocation des ressources.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-204">After a VM has been deployed, it can be resized to increase or decrease resource allocation.</span></span>

<span data-ttu-id="5d0e6-205">Avant de redimensionner une machine virtuelle, vérifiez si la taille souhaitée est disponible dans le cluster de machines virtuelles actuel.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-205">Before resizing a VM, check if the desired size is available on the current VM cluster.</span></span> <span data-ttu-id="5d0e6-206">La commande [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) retourne une liste de tailles.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-206">The [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command returns a list of sizes.</span></span> 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

<span data-ttu-id="5d0e6-207">Si la taille souhaitée est disponible, la machine virtuelle peut être redimensionnée à partir d’un état sous tension, mais elle est redémarrée au cours de l’opération.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-207">If the desired size is available, the VM can be resized from a powered-on state, however it is rebooted during the operation.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

<span data-ttu-id="5d0e6-208">Si la taille souhaitée ne figure pas dans le cluster actuel, la machine virtuelle doit être libérée avant de procéder au redimensionnement.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-208">If the desired size is not on the current cluster, the VM needs to be deallocated before the resize operation can occur.</span></span> <span data-ttu-id="5d0e6-209">Lorsque la machine virtuelle est de nouveau sous tension, notez que toutes les données du disque temporaire sont supprimées et que l’adresse IP publique est modifiée, sauf si une adresse IP statique est utilisée.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-209">Note, when the VM is powered back on, any data on the temp disk are removed, and the public IP address change unless a static IP address is being used.</span></span> 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a><span data-ttu-id="5d0e6-210">États d’alimentation de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5d0e6-210">VM power states</span></span>

<span data-ttu-id="5d0e6-211">Une machine virtuelle Azure peut présenter différents états d’alimentation.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-211">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="5d0e6-212">Cet état représente l’état actuel de la machine virtuelle du point de vue de l’hyperviseur.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-212">This state represents the current state of the VM from the standpoint of the hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="5d0e6-213">États d’alimentation</span><span class="sxs-lookup"><span data-stu-id="5d0e6-213">Power states</span></span>

| <span data-ttu-id="5d0e6-214">État d’alimentation</span><span class="sxs-lookup"><span data-stu-id="5d0e6-214">Power State</span></span> | <span data-ttu-id="5d0e6-215">Description</span><span class="sxs-lookup"><span data-stu-id="5d0e6-215">Description</span></span>
|----|----|
| <span data-ttu-id="5d0e6-216">Starting</span><span class="sxs-lookup"><span data-stu-id="5d0e6-216">Starting</span></span> | <span data-ttu-id="5d0e6-217">Indique que la machine virtuelle est en cours de démarrage.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-217">Indicates the virtual machine is being started.</span></span> |
| <span data-ttu-id="5d0e6-218">Exécution</span><span class="sxs-lookup"><span data-stu-id="5d0e6-218">Running</span></span> | <span data-ttu-id="5d0e6-219">Indique que la machine virtuelle est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-219">Indicates that the virtual machine is running.</span></span> |
| <span data-ttu-id="5d0e6-220">En cours d’arrêt</span><span class="sxs-lookup"><span data-stu-id="5d0e6-220">Stopping</span></span> | <span data-ttu-id="5d0e6-221">Indique que la machine virtuelle est en cours d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-221">Indicates that the virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="5d0e6-222">Arrêté</span><span class="sxs-lookup"><span data-stu-id="5d0e6-222">Stopped</span></span> | <span data-ttu-id="5d0e6-223">Indique que la machine virtuelle est arrêtée.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-223">Indicates that the virtual machine is stopped.</span></span> <span data-ttu-id="5d0e6-224">Notez que les machines virtuelles à l’état arrêté entraînent toujours des frais de calcul.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-224">Note that virtual machines in the stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="5d0e6-225">Libération</span><span class="sxs-lookup"><span data-stu-id="5d0e6-225">Deallocating</span></span> | <span data-ttu-id="5d0e6-226">Indique que la machine virtuelle est en cours de libération.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-226">Indicates that the virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="5d0e6-227">Libéré</span><span class="sxs-lookup"><span data-stu-id="5d0e6-227">Deallocated</span></span> | <span data-ttu-id="5d0e6-228">Indique que la machine virtuelle est totalement supprimée de l’hyperviseur, mais reste disponible dans le plan de contrôle.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-228">Indicates that the virtual machine is completely removed from the hypervisor but still available in the control plane.</span></span> <span data-ttu-id="5d0e6-229">Les machines virtuelles à l’état Libéré n’entraînent pas de frais de calcul.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-229">Virtual machines in the Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="5d0e6-230">Indique que l’état d’alimentation de la machine virtuelle est inconnu.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-230">Indicates that the power state of the virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="5d0e6-231">Rechercher un état d’alimentation</span><span class="sxs-lookup"><span data-stu-id="5d0e6-231">Find power state</span></span>

<span data-ttu-id="5d0e6-232">Pour récupérer l’état d’une machine virtuelle spécifique, utilisez la commande [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="5d0e6-232">To retrieve the state of a particular VM, use the [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span> <span data-ttu-id="5d0e6-233">Veillez à spécifier le nom valide d’une machine virtuelle et d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-233">Be sure to specify a valid name for a virtual machine and resource group.</span></span> 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

<span data-ttu-id="5d0e6-234">Output:</span><span class="sxs-lookup"><span data-stu-id="5d0e6-234">Output:</span></span>

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a><span data-ttu-id="5d0e6-235">Tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="5d0e6-235">Management tasks</span></span>

<span data-ttu-id="5d0e6-236">Pendant le cycle de vie d’une machine virtuelle, vous souhaiterez exécuter des tâches de gestion telles que le démarrage, l’arrêt ou la suppression d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-236">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="5d0e6-237">En outre, vous souhaiterez peut-être créer des scripts pour automatiser les tâches répétitives ou complexes.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-237">Additionally, you may want to create scripts to automate repetitive or complex tasks.</span></span> <span data-ttu-id="5d0e6-238">À l’aide d’Azure PowerShell, de nombreuses tâches courantes de gestion peuvent être exécutées à partir de la ligne de commande ou dans des scripts.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-238">Using Azure PowerShell, many common management tasks can be run from the command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="5d0e6-239">Arrêt d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5d0e6-239">Stop virtual machine</span></span>

<span data-ttu-id="5d0e6-240">Arrêtez et libérez une machine virtuelle avec [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-240">Stop and deallocate a virtual machine with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

<span data-ttu-id="5d0e6-241">Si vous souhaitez conserver la machine virtuelle dans un état approvisionné, utilisez le paramètre -StayProvisioned.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-241">If you want to keep the virtual machine in a provisioned state, use the -StayProvisioned parameter.</span></span>

### <a name="start-virtual-machine"></a><span data-ttu-id="5d0e6-242">Démarrage d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5d0e6-242">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="5d0e6-243">Supprimer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="5d0e6-243">Delete resource group</span></span>

<span data-ttu-id="5d0e6-244">La suppression d’un groupe de ressources supprime également toutes les ressources qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-244">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a><span data-ttu-id="5d0e6-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5d0e6-245">Next steps</span></span>

<span data-ttu-id="5d0e6-246">Ce didacticiel vous a montré les tâches de base de création et de gestion de machines virtuelles, notamment :</span><span class="sxs-lookup"><span data-stu-id="5d0e6-246">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5d0e6-247">Créer une machine virtuelle et vous y connecter</span><span class="sxs-lookup"><span data-stu-id="5d0e6-247">Create and connect to a VM</span></span>
> * <span data-ttu-id="5d0e6-248">Sélectionner et utiliser des images de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5d0e6-248">Select and use VM images</span></span>
> * <span data-ttu-id="5d0e6-249">Afficher et utiliser des tailles de machine virtuelle spécifiques</span><span class="sxs-lookup"><span data-stu-id="5d0e6-249">View and use specific VM sizes</span></span>
> * <span data-ttu-id="5d0e6-250">Redimensionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5d0e6-250">Resize a VM</span></span>
> * <span data-ttu-id="5d0e6-251">Consulter et comprendre l’état d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5d0e6-251">View and understand VM state</span></span>

<span data-ttu-id="5d0e6-252">Passez au didacticiel suivant pour en savoir plus sur les disques de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5d0e6-252">Advance to the next tutorial to learn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="5d0e6-253">Créer et gérer des disques de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5d0e6-253">Create and Manage VM disks</span></span>](./tutorial-manage-data-disk.md)
