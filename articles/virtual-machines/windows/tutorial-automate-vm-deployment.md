---
title: aaaCustomize un ordinateur virtuel Windows Azure | Documents Microsoft
description: "Découvrez comment toouse hello extension de script personnalisé et le coffre de clés toocustomize machines virtuelles Windows Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c03b2bb6d70875134c63ea2fe4c2e2c1777c2188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="682ff-103">Comment toocustomize une machine virtuelle de Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="682ff-103">How toocustomize a Windows virtual machine in Azure</span></span>
<span data-ttu-id="682ff-104">tooconfigure, machines virtuelles (VM) de manière rapide et cohérente, une forme d’automatisation est généralement souhaité.</span><span class="sxs-lookup"><span data-stu-id="682ff-104">tooconfigure virtual machines (VMs) in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="682ff-105">Un toocustomize approche commune une machine virtuelle Windows est toouse [Extension de Script personnalisé pour Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="682ff-105">A common approach toocustomize a Windows VM is toouse [Custom Script Extension for Windows](extensions-customscript.md).</span></span> <span data-ttu-id="682ff-106">Ce didacticiel vous explique comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="682ff-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="682ff-107">Utiliser l’Extension de Script personnalisé de hello tooinstall IIS</span><span class="sxs-lookup"><span data-stu-id="682ff-107">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="682ff-108">Créer une machine virtuelle qui utilise l’Extension de Script personnalisé de hello</span><span class="sxs-lookup"><span data-stu-id="682ff-108">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="682ff-109">Afficher un site IIS en cours d’exécution une fois que l’extension de hello est appliquée</span><span class="sxs-lookup"><span data-stu-id="682ff-109">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="682ff-110">Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module.</span><span class="sxs-lookup"><span data-stu-id="682ff-110">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="682ff-111">Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="682ff-111">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="682ff-112">Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="682ff-112">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="custom-script-extension-overview"></a><span data-ttu-id="682ff-113">Vue d’ensemble de l’extension de script personnalisé</span><span class="sxs-lookup"><span data-stu-id="682ff-113">Custom script extension overview</span></span>
<span data-ttu-id="682ff-114">Extension de Script personnalisé de Hello télécharge et exécute des scripts sur les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="682ff-114">hello Custom Script Extension downloads and executes scripts on Azure VMs.</span></span> <span data-ttu-id="682ff-115">Cette extension est utile pour la configuration post-déploiement, l’installation de logiciels ou toute autre tâche de configuration ou de gestion.</span><span class="sxs-lookup"><span data-stu-id="682ff-115">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="682ff-116">Scripts pouvant être téléchargés à partir de GitHub ou de stockage Azure, ou toohello portail Azure à l’extension de durée d’exécution.</span><span class="sxs-lookup"><span data-stu-id="682ff-116">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span>

<span data-ttu-id="682ff-117">Hello, extension de Script personnalisé s’intègre aux modèles Azure Resource Manager et peut également être exécuté à l’aide de hello CLI d’Azure, PowerShell, portail Azure ou hello API REST de Machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="682ff-117">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="682ff-118">Vous pouvez utiliser hello Extension de Script personnalisé avec les machines virtuelles Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="682ff-118">You can use hello Custom Script Extension with both Windows and Linux VMs.</span></span>


## <a name="create-virtual-machine"></a><span data-ttu-id="682ff-119">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="682ff-119">Create virtual machine</span></span>
<span data-ttu-id="682ff-120">Avant de créer une machine virtuelle, créez un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="682ff-120">Before you can create a VM, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="682ff-121">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupAutomate* Bonjour *EastUS* emplacement :</span><span class="sxs-lookup"><span data-stu-id="682ff-121">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

<span data-ttu-id="682ff-122">Définir un administrateur de nom d’utilisateur et mot de passe pour les machines virtuelles hello avec [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="682ff-122">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="682ff-123">Vous pouvez désormais créer de machine virtuelle avec hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="682ff-123">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="682ff-124">Hello exemple suivant crée les composants de réseau virtuel hello requis, configuration de hello du système d’exploitation et crée ensuite un ordinateur virtuel nommé *myVM*:</span><span class="sxs-lookup"><span data-stu-id="682ff-124">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName myResourceGroupAutomate -Location EastUS -VM $vmConfig
```

<span data-ttu-id="682ff-125">Il prend quelques minutes avant que les ressources hello et toobe de machine virtuelle créée.</span><span class="sxs-lookup"><span data-stu-id="682ff-125">It takes a few minutes for hello resources and VM toobe created.</span></span>


## <a name="automate-iis-install"></a><span data-ttu-id="682ff-126">Automatiser l’installation d’IIS</span><span class="sxs-lookup"><span data-stu-id="682ff-126">Automate IIS install</span></span>
<span data-ttu-id="682ff-127">Utilisez [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Extension de Script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="682ff-127">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="682ff-128">Hello extension exécute `powershell Add-WindowsFeature Web-Server` tooinstall hello serveur Web d’IIS, puis hello de mises à jour *Default.htm* page tooshow hello nom d’hôte de hello machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="682ff-128">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName myResourceGroupAutomate `
    -ExtensionName IIS `
    -VMName myVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
```


## <a name="test-web-site"></a><span data-ttu-id="682ff-129">Tester le site web</span><span class="sxs-lookup"><span data-stu-id="682ff-129">Test web site</span></span>
<span data-ttu-id="682ff-130">Obtenir hello une adresse IP publique de votre équilibreur de charge avec [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="682ff-130">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="682ff-131">exemple Hello obtient adresse IP hello *myPublicIP* créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="682ff-131">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

<span data-ttu-id="682ff-132">Vous pouvez entrer ensuite des adresse IP publique de hello dans tooa navigateur.</span><span class="sxs-lookup"><span data-stu-id="682ff-132">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="682ff-133">site Web de Hello est affichée, notamment le nom d’hôte hello Hello VM cet équilibrage de charge hello distributed tooas trafic Bonjour l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="682ff-133">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Site web IIS en cours d’exécution](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a><span data-ttu-id="682ff-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="682ff-135">Next steps</span></span>

<span data-ttu-id="682ff-136">Dans ce didacticiel, vous avez automatisé hello IIS est installé sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="682ff-136">In this tutorial, you automated hello IIS install on a VM.</span></span> <span data-ttu-id="682ff-137">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="682ff-137">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="682ff-138">Utiliser l’Extension de Script personnalisé de hello tooinstall IIS</span><span class="sxs-lookup"><span data-stu-id="682ff-138">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="682ff-139">Créer une machine virtuelle qui utilise l’Extension de Script personnalisé de hello</span><span class="sxs-lookup"><span data-stu-id="682ff-139">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="682ff-140">Afficher un site IIS en cours d’exécution une fois que l’extension de hello est appliquée</span><span class="sxs-lookup"><span data-stu-id="682ff-140">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="682ff-141">Avancer toolearn de didacticiel suivant toohello comment toocreate les images de machine virtuelle personnalisées.</span><span class="sxs-lookup"><span data-stu-id="682ff-141">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="682ff-142">Créer des images de machine virtuelle personnalisées</span><span class="sxs-lookup"><span data-stu-id="682ff-142">Create custom VM images</span></span>](./tutorial-custom-images.md)
