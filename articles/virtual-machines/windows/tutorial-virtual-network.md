---
title: "aaaAzure réseaux virtuels et des Machines virtuelles Windows | Documents Microsoft"
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
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="eae03-103">Gérer des réseaux virtuels Azure et des machines virtuelles Windows avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="eae03-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="eae03-104">Les machines virtuelles Azure utilisent la gestion réseau Azure pour la communication réseau interne et externe.</span><span class="sxs-lookup"><span data-stu-id="eae03-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="eae03-105">Dans ce didacticiel, vous apprendrez à créer plusieurs machines virtuelles dans un réseau virtuel et à configurer leur connectivité réseau.</span><span class="sxs-lookup"><span data-stu-id="eae03-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="eae03-106">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="eae03-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eae03-107">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="eae03-107">Create a virtual network</span></span>
> * <span data-ttu-id="eae03-108">Créer des sous-réseaux de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="eae03-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="eae03-109">Contrôler le trafic réseau avec les groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="eae03-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="eae03-110">Afficher les règles de trafic en action</span><span class="sxs-lookup"><span data-stu-id="eae03-110">View traffic rules in action</span></span>

<span data-ttu-id="eae03-111">Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module.</span><span class="sxs-lookup"><span data-stu-id="eae03-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="eae03-112">Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="eae03-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="eae03-113">Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="eae03-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="eae03-114">Créer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="eae03-114">Create VNet</span></span>

<span data-ttu-id="eae03-115">Un réseau virtuel est une représentation de votre propre réseau dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="eae03-115">A VNet is a representation of your own network in hello cloud.</span></span> <span data-ttu-id="eae03-116">Un réseau virtuel est une isolation logique de hello Azure cloud dédié tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="eae03-116">A VNet is a logical isolation of hello Azure cloud dedicated tooyour subscription.</span></span> <span data-ttu-id="eae03-117">Au sein d’un réseau virtuel, vous trouverez des sous-réseaux, les règles pour les sous-réseaux toothose de connectivité et des connexions à partir des sous-réseaux toohello hello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="eae03-117">Within a VNet, you find subnets, rules for connectivity toothose subnets, and connections from hello VMs toohello subnets.</span></span>

<span data-ttu-id="eae03-118">Avant de pouvoir créer d’autres ressources Azure, vous devez toocreate un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="eae03-118">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="eae03-119">Hello exemple suivant crée un groupe de ressources nommé *myRGNetwork* Bonjour *EastUS* emplacement :</span><span class="sxs-lookup"><span data-stu-id="eae03-119">hello following example creates a resource group named *myRGNetwork* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="eae03-120">Un sous-réseau est une ressource enfant d’un réseau virtuel, et permet de définir des segments d’espaces d’adressage dans un bloc CIDR, à l’aide de préfixes d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="eae03-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="eae03-121">Cartes réseau peut être ajoutés toosubnets et tooVMs connecté, en offrant une connectivité pour différentes charges de travail.</span><span class="sxs-lookup"><span data-stu-id="eae03-121">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="eae03-122">Créez un sous-réseau avec [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) :</span><span class="sxs-lookup"><span data-stu-id="eae03-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="eae03-123">Créez un réseau virtuel nommé *myVNet* en utilisant *myFrontendSubnet* avec [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) :</span><span class="sxs-lookup"><span data-stu-id="eae03-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="eae03-124">Créer une machine virtuelle frontale</span><span class="sxs-lookup"><span data-stu-id="eae03-124">Create front-end VM</span></span>

<span data-ttu-id="eae03-125">Pour une machine virtuelle toocommunicate dans un réseau virtuel, il a besoin d’une interface réseau virtuelle (NIC).</span><span class="sxs-lookup"><span data-stu-id="eae03-125">For a VM toocommunicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="eae03-126">Hello *myFrontendVM* est accessible à partir de hello internet, par conséquent, il doit également une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="eae03-126">hello *myFrontendVM* is accessed from hello internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="eae03-127">Créez une adresse IP publique avec [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) :</span><span class="sxs-lookup"><span data-stu-id="eae03-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="eae03-128">Créez une carte réseau avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) :</span><span class="sxs-lookup"><span data-stu-id="eae03-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="eae03-129">Définir le nom d’utilisateur hello et un mot de passe nécessaire pour le compte d’administrateur hello hello machine virtuelle avec [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="eae03-129">Set hello username and password needed for hello administrator account on hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="eae03-130">Créer des machines virtuelles hello avec [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [AzureRmVMOperatingSystem de jeu](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [AzureRmVMNetworkInterface ajouter](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), et [AzureRmVM-nouvelle](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="eae03-130">Create hello VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

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

## <a name="install-web-server"></a><span data-ttu-id="eae03-131">Installer le serveur web</span><span class="sxs-lookup"><span data-stu-id="eae03-131">Install web server</span></span>

<span data-ttu-id="eae03-132">Vous pouvez installer IIS sur *myFrontendVM* à partir d’une session Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="eae03-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="eae03-133">Vous devez tooget hello adresse IP publique de hello VM tooaccess il.</span><span class="sxs-lookup"><span data-stu-id="eae03-133">You need tooget hello public IP address of hello VM tooaccess it.</span></span>

<span data-ttu-id="eae03-134">Vous pouvez obtenir d’adresse IP publique de hello de *myFrontendVM* avec [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="eae03-134">You can get hello public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="eae03-135">exemple Hello obtient adresse IP hello *myPublicIPAddress* créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="eae03-135">hello following example obtains hello IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="eae03-136">Notez cette adresse IP : vous en aurez besoin lors des étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="eae03-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="eae03-137">Suivant de hello utilisez commande toocreate une session Bureau à distance avec *myFrontendVM*.</span><span class="sxs-lookup"><span data-stu-id="eae03-137">Use hello following command toocreate a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="eae03-138">Remplacez  *<publicIPAddress>*  avec l’adresse hello que vous avez enregistrée précédemment.</span><span class="sxs-lookup"><span data-stu-id="eae03-138">Replace *<publicIPAddress>* with hello address that you previously recorded.</span></span> <span data-ttu-id="eae03-139">Lorsque vous y êtes invité, entrez les informations d’identification de l’hello utilisées lors de la création de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="eae03-139">When prompted, enter hello credentials used when you created hello VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="eae03-140">Maintenant que vous avez ouvert une session trop*myFrontendVM*, vous pouvez utiliser une seule ligne de PowerShell tooinstall IIS et activer le trafic web tooallow hello pare-feu local règle.</span><span class="sxs-lookup"><span data-stu-id="eae03-140">Now that you have logged in too*myFrontendVM*, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="eae03-141">Ouvrez une invite de PowerShell et exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="eae03-141">Open a PowerShell prompt and run hello following command:</span></span>

<span data-ttu-id="eae03-142">Utilisez [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) extension de script personnalisé hello toorun qui installe le serveur Web IIS de hello :</span><span class="sxs-lookup"><span data-stu-id="eae03-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello custom script extension that installs hello IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="eae03-143">Vous pouvez désormais utiliser hello publique IP adresse toobrowse toohello VM toosee hello site IIS.</span><span class="sxs-lookup"><span data-stu-id="eae03-143">Now you can use hello public IP address toobrowse toohello VM toosee hello IIS site.</span></span>

![Site IIS par défaut](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="eae03-145">Gérer le trafic interne</span><span class="sxs-lookup"><span data-stu-id="eae03-145">Manage internal traffic</span></span>

<span data-ttu-id="eae03-146">Un groupe de sécurité réseau (NSG) contient une liste de règles de sécurité qui autorisent ou refusent tooa tooresources connecté de trafic réseau réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="eae03-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooa VNet.</span></span> <span data-ttu-id="eae03-147">Groupes de sécurité réseau peuvent être associé à toosubnets ou des cartes réseau attachée tooVMs.</span><span class="sxs-lookup"><span data-stu-id="eae03-147">NSGs can be associated toosubnets or individual NICs attached tooVMs.</span></span> <span data-ttu-id="eae03-148">Ouvrir ou de fermer tooVMs accès via des ports s’effectue à l’aide de règles de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="eae03-148">Opening or closing access tooVMs through ports is done using NSG rules.</span></span> <span data-ttu-id="eae03-149">Quand vous avez créé *myFrontendVM*, le port d’entrée 3389 a été automatiquement ouvert pour la connectivité RDP.</span><span class="sxs-lookup"><span data-stu-id="eae03-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="eae03-150">La communication interne des machines virtuelles peut être configurée à l’aide d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="eae03-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="eae03-151">Dans cette section, vous apprendrez comment toocreate un sous-réseau supplémentaire Bonjour réseau et affecter un tooallow tooit de groupe de sécurité réseau à une connexion à partir de *myFrontendVM* trop*myBackendVM* sur le port 1433.</span><span class="sxs-lookup"><span data-stu-id="eae03-151">In this section, you learn how toocreate an additional subnet in hello network and assign an NSG tooit tooallow a connection from *myFrontendVM* too*myBackendVM* on port 1433.</span></span> <span data-ttu-id="eae03-152">sous-réseau de Hello est ensuite assigné toohello machine virtuelle lors de sa création.</span><span class="sxs-lookup"><span data-stu-id="eae03-152">hello subnet is then assigned toohello VM when it is created.</span></span>

<span data-ttu-id="eae03-153">Vous pouvez limiter le trafic interne trop*myBackendVM* depuis une seule *myFrontendVM* en créant un groupe de sécurité réseau pour le sous-réseau principal de hello.</span><span class="sxs-lookup"><span data-stu-id="eae03-153">You can limit internal traffic too*myBackendVM* from only *myFrontendVM* by creating an NSG for hello back-end subnet.</span></span> <span data-ttu-id="eae03-154">Hello exemple suivant crée une règle de groupe de sécurité réseau nommée *myBackendNSGRule* avec [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span><span class="sxs-lookup"><span data-stu-id="eae03-154">hello following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

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

<span data-ttu-id="eae03-155">Ajoutez un groupe de sécurité réseau nommé *myBackendNSG* avec [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) :</span><span class="sxs-lookup"><span data-stu-id="eae03-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="eae03-156">Ajouter un sous-réseau principal</span><span class="sxs-lookup"><span data-stu-id="eae03-156">Add back-end subnet</span></span>

<span data-ttu-id="eae03-157">Ajouter *myBackEndSubnet* trop*myVNet* avec [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="eae03-157">Add *myBackEndSubnet* too*myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

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

## <a name="create-back-end-vm"></a><span data-ttu-id="eae03-158">Créer une machine virtuelle principale</span><span class="sxs-lookup"><span data-stu-id="eae03-158">Create back-end VM</span></span>

<span data-ttu-id="eae03-159">hello toocreate moyen plus simple de Hello machine virtuelle de serveur principal est à l’aide d’une image de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="eae03-159">hello easiest way toocreate hello back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="eae03-160">Ce didacticiel crée hello machine virtuelle avec le serveur de base de données hello uniquement, mais ne fournit pas d’informations sur l’accès à la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="eae03-160">This tutorial only creates hello VM with hello database server, but doesn't provide information about accessing hello database.</span></span>

<span data-ttu-id="eae03-161">Créez *myBackendNic* :</span><span class="sxs-lookup"><span data-stu-id="eae03-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="eae03-162">Définir le nom d’utilisateur hello et le mot de passe de compte d’administrateur hello hello machine virtuelle avec Get-Credential :</span><span class="sxs-lookup"><span data-stu-id="eae03-162">Set hello username and password needed for hello administrator account on hello VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="eae03-163">Créez *myBackendVM* :</span><span class="sxs-lookup"><span data-stu-id="eae03-163">Create *myBackendVM*:</span></span>

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

<span data-ttu-id="eae03-164">image Hello utilisée a SQL Server est installé, mais n’est pas utilisé dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="eae03-164">hello image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="eae03-165">Il est inclus tooshow vous comment vous pouvez configurer de trafic web toohandle de machine virtuelle et une gestion de base de données de machine virtuelle toohandle.</span><span class="sxs-lookup"><span data-stu-id="eae03-165">It is included tooshow you how you can configure a VM toohandle web traffic and a VM toohandle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eae03-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eae03-166">Next steps</span></span>

<span data-ttu-id="eae03-167">Dans ce didacticiel, vous créé et sécurisé de réseaux Azure en tant que machines de toovirtual connexes.</span><span class="sxs-lookup"><span data-stu-id="eae03-167">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="eae03-168">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="eae03-168">Create a virtual network</span></span>
> * <span data-ttu-id="eae03-169">Créer des sous-réseaux de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="eae03-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="eae03-170">Contrôler le trafic réseau avec les groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="eae03-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="eae03-171">Afficher les règles de trafic en action</span><span class="sxs-lookup"><span data-stu-id="eae03-171">View traffic rules in action</span></span>

<span data-ttu-id="eae03-172">Avance toohello toolearn de didacticiel suivant sur l’analyse de protection des données sur des machines virtuelles à l’aide de la sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="eae03-172">Advance toohello next tutorial toolearn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="eae03-173">.</span><span class="sxs-lookup"><span data-stu-id="eae03-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eae03-174">Sauvegarde de machines virtuelles Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="eae03-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
