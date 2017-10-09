---
title: "aaaAzure démarrage rapide : créer Windows PowerShell de machine virtuelle | Documents Microsoft"
description: Apprendre rapidement toocreate des machines virtuelles Windows avec PowerShell
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a><span data-ttu-id="c6f81-103">Créer une machine virtuelle Windows avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6f81-103">Create a Windows virtual machine with PowerShell</span></span>

<span data-ttu-id="c6f81-104">module d’Azure PowerShell Hello est toocreate utilisé et gérer des ressources Azure à partir de la ligne de commande PowerShell hello ou dans des scripts.</span><span class="sxs-lookup"><span data-stu-id="c6f81-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="c6f81-105">Ce guide décrit en détail à l’aide de PowerShell toocreate et la machine virtuelle Azure exécutant Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="c6f81-105">This guide details using PowerShell toocreate and Azure virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="c6f81-106">Une fois le déploiement terminé, nous connecter toohello serveur et installez IIS.</span><span class="sxs-lookup"><span data-stu-id="c6f81-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>  

<span data-ttu-id="c6f81-107">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="c6f81-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="c6f81-108">Ce démarrage rapide nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module.</span><span class="sxs-lookup"><span data-stu-id="c6f81-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="c6f81-109">Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="c6f81-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="c6f81-110">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c6f81-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="c6f81-111">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="c6f81-111">Log in tooAzure</span></span>

<span data-ttu-id="c6f81-112">Connectez-vous à tooyour abonnement Azure avec hello `Login-AzureRmAccount` commande et suivez hello à l’écran.</span><span class="sxs-lookup"><span data-stu-id="c6f81-112">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="c6f81-113">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="c6f81-113">Create resource group</span></span>

<span data-ttu-id="c6f81-114">Créez un groupe de ressources Azure avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="c6f81-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="c6f81-115">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="c6f81-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a><span data-ttu-id="c6f81-116">Création de ressources de mise en réseau</span><span class="sxs-lookup"><span data-stu-id="c6f81-116">Create networking resources</span></span>

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a><span data-ttu-id="c6f81-117">Créez un réseau virtuel, un sous-réseau et une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="c6f81-117">Create a virtual network, subnet, and a public IP address.</span></span> 
<span data-ttu-id="c6f81-118">Ces ressources tooprovide utilisés de connectivité réseau toohello l’ordinateur virtuel et le connecter toohello internet.</span><span class="sxs-lookup"><span data-stu-id="c6f81-118">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="c6f81-119">Créez un groupe de sécurité réseau et une règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="c6f81-119">Create a network security group and a network security group rule.</span></span> 
<span data-ttu-id="c6f81-120">groupe de sécurité réseau Hello sécurise la machine virtuelle de hello à l’aide des règles de trafic entrants et sortants.</span><span class="sxs-lookup"><span data-stu-id="c6f81-120">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="c6f81-121">Dans ce cas, une règle entrante est créée pour le port 3389, qui autorise les connexions Bureau à distance entrantes.</span><span class="sxs-lookup"><span data-stu-id="c6f81-121">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span> <span data-ttu-id="c6f81-122">Nous souhaitons également toocreate une règle de trafic entrant pour le port 80, qui autorise le trafic web entrant.</span><span class="sxs-lookup"><span data-stu-id="c6f81-122">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-hello-virtual-machine"></a><span data-ttu-id="c6f81-123">Créer une carte réseau pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="c6f81-123">Create a network card for hello virtual machine.</span></span> 
<span data-ttu-id="c6f81-124">Créer une carte réseau avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="c6f81-124">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="c6f81-125">carte réseau de Hello connecte le sous-réseau de tooa d’ordinateurs virtuels hello, groupe de sécurité réseau et adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="c6f81-125">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="c6f81-126">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="c6f81-126">Create virtual machine</span></span>

<span data-ttu-id="c6f81-127">Créez une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c6f81-127">Create a virtual machine configuration.</span></span> <span data-ttu-id="c6f81-128">Cette configuration inclut des paramètres hello sont utilisées lors du déploiement d’ordinateur virtuel de hello comme une configuration de machine virtuelle image, la taille et l’authentification.</span><span class="sxs-lookup"><span data-stu-id="c6f81-128">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span> <span data-ttu-id="c6f81-129">Lors de l’exécution de cette étape, vous êtes invité à saisir vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="c6f81-129">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="c6f81-130">les valeurs Hello que vous entrez sont configurés en tant que nom d’utilisateur hello et un mot de passe pour l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="c6f81-130">hello values that you enter are configured as hello user name and password for hello virtual machine.</span></span>

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

<span data-ttu-id="c6f81-131">Créer la machine virtuelle hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="c6f81-131">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="c6f81-132">Connecter toovirtual machine</span><span class="sxs-lookup"><span data-stu-id="c6f81-132">Connect toovirtual machine</span></span>

<span data-ttu-id="c6f81-133">Après que le déploiement de hello terminée, créez une connexion Bureau à distance avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="c6f81-133">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="c6f81-134">Hello d’utilisation [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) commande tooreturn hello adresse IP publique de l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="c6f81-134">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="c6f81-135">Prenez note de cette adresse IP pour pouvoir vous connecter tooit reliées votre navigateur tootest web dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c6f81-135">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="c6f81-136">La commande suivante de hello utilisation toocreate une session Bureau à distance avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="c6f81-136">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="c6f81-137">Remplacer l’adresse IP de hello avec hello *publicIPAddress* de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c6f81-137">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="c6f81-138">Lorsque vous y êtes invité, entrez les informations d’identification de l’hello utilisées lors de la création d’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="c6f81-138">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="c6f81-139">Installer IIS à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6f81-139">Install IIS via PowerShell</span></span>

<span data-ttu-id="c6f81-140">Maintenant que vous êtes connecté toohello machine virtuelle Azure, vous pouvez utiliser une seule ligne de PowerShell tooinstall IIS et activer le trafic web tooallow hello pare-feu local règle.</span><span class="sxs-lookup"><span data-stu-id="c6f81-140">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="c6f81-141">Ouvrez une invite de PowerShell et exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c6f81-141">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="c6f81-142">Hello d’affichage page d’accueil IIS</span><span class="sxs-lookup"><span data-stu-id="c6f81-142">View hello IIS welcome page</span></span>

<span data-ttu-id="c6f81-143">Avec les services IIS sont installés et le port 80 maintenant ouvrir sur votre machine virtuelle à partir de hello Internet, vous pouvez utiliser un navigateur web de votre choix tooview hello par défaut IIS page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="c6f81-143">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="c6f81-144">Être vraiment toouse hello *publicIpAddress* vous documenté au-dessus de la page par défaut toovisit hello.</span><span class="sxs-lookup"><span data-stu-id="c6f81-144">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Site IIS par défaut](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="c6f81-146">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="c6f81-146">Clean up resources</span></span>

<span data-ttu-id="c6f81-147">Lorsque vous n’est plus nécessaire, vous pouvez utiliser hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) groupe de ressources tooremove hello, machine virtuelle et toutes les ressources de la commande.</span><span class="sxs-lookup"><span data-stu-id="c6f81-147">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="c6f81-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c6f81-148">Next steps</span></span>

<span data-ttu-id="c6f81-149">Dans ce guide de démarrage rapide, vous avez déployé une machine virtuelle simple ainsi qu’une règle de groupe de sécurité réseau, et installé un serveur web.</span><span class="sxs-lookup"><span data-stu-id="c6f81-149">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="c6f81-150">toolearn en savoir plus sur les machines virtuelles, continuer toohello didacticiel pour les machines virtuelles Windows.</span><span class="sxs-lookup"><span data-stu-id="c6f81-150">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c6f81-151">Didacticiels sur les machines virtuelles Azure Windows</span><span class="sxs-lookup"><span data-stu-id="c6f81-151">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
