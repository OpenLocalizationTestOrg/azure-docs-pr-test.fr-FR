---
title: "Réseaux virtuels Azure et machines virtuelles Windows | Microsoft Docs"
description: "Didacticiel : Gérer des réseaux virtuels Azure et des machines virtuelles Windows avec Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: c71c07f8ecd123a7e27848ba5043d46e315fcf03
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="d306d-103">Gérer des réseaux virtuels Azure et des machines virtuelles Windows avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d306d-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="d306d-104">Les machines virtuelles Azure utilisent la gestion réseau Azure pour la communication réseau interne et externe.</span><span class="sxs-lookup"><span data-stu-id="d306d-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="d306d-105">Dans ce didacticiel, vous apprendrez à créer plusieurs machines virtuelles dans un réseau virtuel et à configurer leur connectivité réseau.</span><span class="sxs-lookup"><span data-stu-id="d306d-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="d306d-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="d306d-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d306d-107">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="d306d-107">Create a virtual network</span></span>
> * <span data-ttu-id="d306d-108">Créer des sous-réseaux de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="d306d-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="d306d-109">Contrôler le trafic réseau avec les groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="d306d-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="d306d-110">Afficher les règles de trafic en action</span><span class="sxs-lookup"><span data-stu-id="d306d-110">View traffic rules in action</span></span>

<span data-ttu-id="d306d-111">Ce didacticiel requiert le module Azure PowerShell version 3.6 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d306d-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="d306d-112">Exécutez ` Get-Module -ListAvailable AzureRM` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="d306d-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="d306d-113">Si vous devez effectuer une mise à niveau, consultez [Installer le module Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="d306d-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="d306d-114">Créer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="d306d-114">Create VNet</span></span>

<span data-ttu-id="d306d-115">Un réseau virtuel est une représentation de votre propre réseau dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="d306d-115">A VNet is a representation of your own network in the cloud.</span></span> <span data-ttu-id="d306d-116">Il s’agit d’un isolement logique du cloud Azure dédié à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="d306d-116">A VNet is a logical isolation of the Azure cloud dedicated to your subscription.</span></span> <span data-ttu-id="d306d-117">Un réseau virtuel comporte des sous-réseaux, des règles de connectivité vers ces sous-réseaux, et des connexions entre les machines virtuelles et les sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="d306d-117">Within a VNet, you find subnets, rules for connectivity to those subnets, and connections from the VMs to the subnets.</span></span>

<span data-ttu-id="d306d-118">Vous devez créer un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) pour pouvoir créer d’autres ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d306d-118">Before you can create any other Azure resources, you need to create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="d306d-119">L’exemple suivant crée un groupe de ressources nommé *myRGNetwork* à l’emplacement *EastUS* :</span><span class="sxs-lookup"><span data-stu-id="d306d-119">The following example creates a resource group named *myRGNetwork* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="d306d-120">Un sous-réseau est une ressource enfant d’un réseau virtuel, et permet de définir des segments d’espaces d’adressage dans un bloc CIDR, à l’aide de préfixes d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="d306d-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="d306d-121">Les cartes d’interface réseau (NIC) peuvent être ajoutées aux sous-réseaux et connectées aux machines virtuelles, ce qui fournit une connectivité pour différentes charges de travail.</span><span class="sxs-lookup"><span data-stu-id="d306d-121">NICs can be added to subnets, and connected to VMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="d306d-122">Créez un sous-réseau avec [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) :</span><span class="sxs-lookup"><span data-stu-id="d306d-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="d306d-123">Créez un réseau virtuel nommé *myVNet* en utilisant *myFrontendSubnet* avec [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) :</span><span class="sxs-lookup"><span data-stu-id="d306d-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="d306d-124">Créer une machine virtuelle frontale</span><span class="sxs-lookup"><span data-stu-id="d306d-124">Create front-end VM</span></span>

<span data-ttu-id="d306d-125">Pour communiquer avec un réseau virtuel, une machine virtuelle a besoin d’une interface réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d306d-125">For a VM to communicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="d306d-126">*myFrontendVM* est accessible à partir d’Internet et a donc aussi besoin d’une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="d306d-126">The *myFrontendVM* is accessed from the internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="d306d-127">Créez une adresse IP publique avec [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) :</span><span class="sxs-lookup"><span data-stu-id="d306d-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="d306d-128">Créez une carte réseau avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) :</span><span class="sxs-lookup"><span data-stu-id="d306d-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="d306d-129">Définissez le nom d’utilisateur et le mot de passe pour le compte Administrateur sur la machine virtuelle avec [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) :</span><span class="sxs-lookup"><span data-stu-id="d306d-129">Set the username and password needed for the administrator account on the VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="d306d-130">Créez les machines virtuelles avec [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) et [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="d306d-130">Create the VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a><span data-ttu-id="d306d-131">Installer le serveur web</span><span class="sxs-lookup"><span data-stu-id="d306d-131">Install web server</span></span>

<span data-ttu-id="d306d-132">Vous pouvez installer IIS sur *myFrontendVM* à partir d’une session Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="d306d-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="d306d-133">Vous avez besoin de l’adresse IP publique de la machine virtuelle pour y accéder.</span><span class="sxs-lookup"><span data-stu-id="d306d-133">You need to get the public IP address of the VM to access it.</span></span>

<span data-ttu-id="d306d-134">Vous pouvez obtenir l’adresse IP publique de *myFrontendVM* avec [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="d306d-134">You can get the public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="d306d-135">L’exemple suivant obtient l’adresse IP pour l’adresse *myPublicIPAddress* créée précédemment :</span><span class="sxs-lookup"><span data-stu-id="d306d-135">The following example obtains the IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="d306d-136">Notez cette adresse IP : vous en aurez besoin lors des étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="d306d-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="d306d-137">Utilisez la commande suivante pour créer une session Bureau à distance avec *myFrontendVM*.</span><span class="sxs-lookup"><span data-stu-id="d306d-137">Use the following command to create a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="d306d-138">Remplacez *<publicIPAddress>* par l’adresse que vous avez enregistrée précédemment.</span><span class="sxs-lookup"><span data-stu-id="d306d-138">Replace *<publicIPAddress>* with the address that you previously recorded.</span></span> <span data-ttu-id="d306d-139">À l’invite, saisissez les informations d’identification que vous avez utilisées lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d306d-139">When prompted, enter the credentials used when you created the VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="d306d-140">Maintenant que vous êtes connecté à *myFrontendVM*, vous pouvez utiliser une seule ligne de PowerShell pour installer IIS et activer la règle de pare-feu local pour autoriser le trafic web.</span><span class="sxs-lookup"><span data-stu-id="d306d-140">Now that you have logged in to *myFrontendVM*, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="d306d-141">Ouvrez une invite PowerShell et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d306d-141">Open a PowerShell prompt and run the following command:</span></span>

<span data-ttu-id="d306d-142">Utilisez [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) pour exécuter l’extension de script personnalisé qui installe le serveur Web IIS :</span><span class="sxs-lookup"><span data-stu-id="d306d-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) to run the custom script extension that installs the IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="d306d-143">Vous pouvez maintenant utiliser l’adresse IP publique pour accéder à la machine virtuelle et afficher le site IIS.</span><span class="sxs-lookup"><span data-stu-id="d306d-143">Now you can use the public IP address to browse to the VM to see the IIS site.</span></span>

![Site IIS par défaut](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="d306d-145">Gérer le trafic interne</span><span class="sxs-lookup"><span data-stu-id="d306d-145">Manage internal traffic</span></span>

<span data-ttu-id="d306d-146">Un groupe de sécurité réseau contient une liste de règles de sécurité qui autorisent ou rejettent le trafic réseau vers les ressources connectées à un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="d306d-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic to resources connected to a VNet.</span></span> <span data-ttu-id="d306d-147">Les groupes de sécurité réseau peuvent être associés à des sous-réseaux ou à des cartes réseau distinctes qui sont attachées aux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d306d-147">NSGs can be associated to subnets or individual NICs attached to VMs.</span></span> <span data-ttu-id="d306d-148">L’ouverture et la fermeture de l’accès aux machines virtuelles par le biais des ports s’effectuent à l’aide des règles de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d306d-148">Opening or closing access to VMs through ports is done using NSG rules.</span></span> <span data-ttu-id="d306d-149">Quand vous avez créé *myFrontendVM*, le port d’entrée 3389 a été automatiquement ouvert pour la connectivité RDP.</span><span class="sxs-lookup"><span data-stu-id="d306d-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="d306d-150">La communication interne des machines virtuelles peut être configurée à l’aide d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d306d-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="d306d-151">Dans cette section, vous allez apprendre à créer un sous-réseau supplémentaire dans le réseau et à lui affecter un groupe de sécurité réseau pour autoriser une connexion de *myFrontendVM* vers *myBackendVM* sur le port 1433.</span><span class="sxs-lookup"><span data-stu-id="d306d-151">In this section, you learn how to create an additional subnet in the network and assign an NSG to it to allow a connection from *myFrontendVM* to *myBackendVM* on port 1433.</span></span> <span data-ttu-id="d306d-152">Le sous-réseau est ensuite affecté à la machine virtuelle lors de sa création.</span><span class="sxs-lookup"><span data-stu-id="d306d-152">The subnet is then assigned to the VM when it is created.</span></span>

<span data-ttu-id="d306d-153">Vous pouvez limiter le trafic interne vers *myBackendVM* en provenance uniquement de *myFrontendVM* en créant un groupe de sécurité réseau pour le sous-réseau back-end.</span><span class="sxs-lookup"><span data-stu-id="d306d-153">You can limit internal traffic to *myBackendVM* from only *myFrontendVM* by creating an NSG for the back-end subnet.</span></span> <span data-ttu-id="d306d-154">L’exemple suivant crée une règle de groupe de sécurité réseau nommée *myBackendNSGRule* avec [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) :</span><span class="sxs-lookup"><span data-stu-id="d306d-154">The following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

<span data-ttu-id="d306d-155">Ajoutez un groupe de sécurité réseau nommé *myBackendNSG* avec [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) :</span><span class="sxs-lookup"><span data-stu-id="d306d-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="d306d-156">Ajouter un sous-réseau principal</span><span class="sxs-lookup"><span data-stu-id="d306d-156">Add back-end subnet</span></span>

<span data-ttu-id="d306d-157">Ajoutez *myBackEndSubnet* à *myVNet* avec [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig) :</span><span class="sxs-lookup"><span data-stu-id="d306d-157">Add *myBackEndSubnet* to *myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a><span data-ttu-id="d306d-158">Créer une machine virtuelle principale</span><span class="sxs-lookup"><span data-stu-id="d306d-158">Create back-end VM</span></span>

<span data-ttu-id="d306d-159">Pour créer une machine virtuelle principale, le plus simple consiste à utiliser une image SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d306d-159">The easiest way to create the back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="d306d-160">Ce didacticiel crée la machine virtuelle avec le serveur de base de données, mais il ne fournit pas d’informations sur l’accès à la base de données.</span><span class="sxs-lookup"><span data-stu-id="d306d-160">This tutorial only creates the VM with the database server, but doesn't provide information about accessing the database.</span></span>

<span data-ttu-id="d306d-161">Créez *myBackendNic* :</span><span class="sxs-lookup"><span data-stu-id="d306d-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="d306d-162">Définissez le nom d’utilisateur et le mot de passe pour le compte Administrateur sur la machine virtuelle avec Get-Credential :</span><span class="sxs-lookup"><span data-stu-id="d306d-162">Set the username and password needed for the administrator account on the VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="d306d-163">Créez *myBackendVM* :</span><span class="sxs-lookup"><span data-stu-id="d306d-163">Create *myBackendVM*:</span></span>

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

<span data-ttu-id="d306d-164">L’image utilisée inclut SQL Server, mais elle n’est pas utilisée dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d306d-164">The image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="d306d-165">Elle est présentée pour vous montrer comment configurer une machine virtuelle afin de gérer le trafic web, et comment configurer une machine virtuelle afin de traiter la gestion de la base de données.</span><span class="sxs-lookup"><span data-stu-id="d306d-165">It is included to show you how you can configure a VM to handle web traffic and a VM to handle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d306d-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d306d-166">Next steps</span></span>

<span data-ttu-id="d306d-167">Dans ce didacticiel, vous avez créé et sécurisé des réseaux Azure concernant les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d306d-167">In this tutorial, you created and secured Azure networks as related to virtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="d306d-168">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="d306d-168">Create a virtual network</span></span>
> * <span data-ttu-id="d306d-169">Créer des sous-réseaux de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="d306d-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="d306d-170">Contrôler le trafic réseau avec les groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="d306d-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="d306d-171">Afficher les règles de trafic en action</span><span class="sxs-lookup"><span data-stu-id="d306d-171">View traffic rules in action</span></span>

<span data-ttu-id="d306d-172">Passez au didacticiel suivant pour découvrir comment sécuriser et surveiller les données sur des machines virtuelles avec Sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="d306d-172">Advance to the next tutorial to learn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="d306d-173">.</span><span class="sxs-lookup"><span data-stu-id="d306d-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d306d-174">Sauvegarde de machines virtuelles Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="d306d-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
