---
title: "Démarrage rapide avec Azure - PowerShell pour la création d’une machine virtuelle | Microsoft Docs"
description: "Apprenez à créer rapidement des machines virtuelles Linux avec PowerShell"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: adcf492d4c2d935c880167675a1ed97566156ec7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="599ea-103">Créer une machine virtuelle Linux avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="599ea-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="599ea-104">Le module Azure PowerShell est utilisé pour créer et gérer des ressources Azure à partir de la ligne de commande PowerShell ou dans des scripts.</span><span class="sxs-lookup"><span data-stu-id="599ea-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span></span> <span data-ttu-id="599ea-105">Ce guide détaille l’utilisation du module Azure PowerShell pour le déploiement d’une machine virtuelle exécutant le serveur Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="599ea-105">This guide details using the Azure PowerShell module to deploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="599ea-106">Une fois le serveur déployé, une connexion SSH est créée, et un serveur web NGINX est installé.</span><span class="sxs-lookup"><span data-stu-id="599ea-106">Once the server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="599ea-107">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="599ea-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="599ea-108">Ce démarrage rapide requiert le module Azure PowerShell version 3.6 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="599ea-108">This quick start requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="599ea-109">Exécutez ` Get-Module -ListAvailable AzureRM` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="599ea-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="599ea-110">Si vous devez installer ou mettre à niveau, consultez [Installer le module Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="599ea-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="599ea-111">Enfin, une clé SSH publique portant le nom *id_rsa.pub* doit être stockée dans le répertoire *.ssh* de votre profil utilisateur Windows.</span><span class="sxs-lookup"><span data-stu-id="599ea-111">Finally, a public SSH key with the name *id_rsa.pub* needs to be stored in the *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="599ea-112">Pour plus d’informations sur la création de clés SSH pour Azure, consultez [Création de clés SSH pour Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="599ea-112">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="599ea-113">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="599ea-113">Log in to Azure</span></span>

<span data-ttu-id="599ea-114">Connectez-vous à votre abonnement Azure avec la commande `Login-AzureRmAccount` et suivez les instructions à l’écran.</span><span class="sxs-lookup"><span data-stu-id="599ea-114">Log in to your Azure subscription with the `Login-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="599ea-115">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="599ea-115">Create resource group</span></span>

<span data-ttu-id="599ea-116">Créez un groupe de ressources Azure avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="599ea-116">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="599ea-117">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="599ea-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a><span data-ttu-id="599ea-118">Création de ressources de mise en réseau</span><span class="sxs-lookup"><span data-stu-id="599ea-118">Create networking resources</span></span>

<span data-ttu-id="599ea-119">Créez un réseau virtuel, un sous-réseau et une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="599ea-119">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="599ea-120">Ces ressources sont utilisées pour fournir une connectivité réseau à la machine virtuelle et la connecter à Internet.</span><span class="sxs-lookup"><span data-stu-id="599ea-120">These resources are used to provide network connectivity to the virtual machine and connect it to the internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location eastus `
-Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location eastus `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

<span data-ttu-id="599ea-121">Créez un groupe de sécurité réseau et une règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="599ea-121">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="599ea-122">Le groupe de sécurité réseau permet sécurise la machine virtuelle avec des règles entrantes et sortantes.</span><span class="sxs-lookup"><span data-stu-id="599ea-122">The network security group secures the virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="599ea-123">Dans ce cas, une règle entrante est créée pour le port 22, qui autorise les connexions SSH.</span><span class="sxs-lookup"><span data-stu-id="599ea-123">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="599ea-124">Nous souhaitons également créer une règle entrante pour le port 80, qui autorise le trafic web entrant.</span><span class="sxs-lookup"><span data-stu-id="599ea-124">We also want to create an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleSSH  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location eastus `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

<span data-ttu-id="599ea-125">Créez une carte réseau avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="599ea-125">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for the virtual machine.</span></span> <span data-ttu-id="599ea-126">La carte réseau connecte la machine virtuelle à un sous-réseau, un groupe de sécurité réseau et une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="599ea-126">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="599ea-127">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="599ea-127">Create virtual machine</span></span>

<span data-ttu-id="599ea-128">Créez une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="599ea-128">Create a virtual machine configuration.</span></span> <span data-ttu-id="599ea-129">Cette configuration inclut les paramètres qui sont utilisés lors du déploiement de la machine virtuelle, comme une image de machine virtuelle, la taille et la configuration de l’authentification.</span><span class="sxs-lookup"><span data-stu-id="599ea-129">This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

```powershell
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName myVM -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName Canonical -Offer UbuntuServer -Skus 14.04.2-LTS -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

<span data-ttu-id="599ea-130">Créez la machine virtuelle avec [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="599ea-130">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="599ea-131">Connexion à la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="599ea-131">Connect to virtual machine</span></span>

<span data-ttu-id="599ea-132">Une fois le déploiement terminé, créez une connexion SSH avec la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="599ea-132">After the deployment has completed, create an SSH connection with the virtual machine.</span></span>

<span data-ttu-id="599ea-133">Utilisez la commande [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) pour renvoyer l’adresse IP publique de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="599ea-133">Use the [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command to return the public IP address of the virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="599ea-134">Sur un système avec SSH installé, utilisez la commande suivante pour vous connecter à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="599ea-134">From a system with SSH installed, used the following command to connect to the virtual machine.</span></span> <span data-ttu-id="599ea-135">Si vous travaillez sur Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) peut être utilisé pour créer la connexion.</span><span class="sxs-lookup"><span data-stu-id="599ea-135">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used to create the connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="599ea-136">Lorsque vous y êtes invité, le nom d’utilisateur à saisir est *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="599ea-136">When prompted, the login user name is *azureuser*.</span></span> <span data-ttu-id="599ea-137">Si une phrase secrète a été entrée lors de la création de clés SSH, vous devez également l’entrer.</span><span class="sxs-lookup"><span data-stu-id="599ea-137">If a passphrase was entered when creating SSH keys, you need to enter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="599ea-138">Installer NGINX</span><span class="sxs-lookup"><span data-stu-id="599ea-138">Install NGINX</span></span>

<span data-ttu-id="599ea-139">Utilisez le script Bash suivant pour mettre à jour les sources de package et installer le dernier package NGINX.</span><span class="sxs-lookup"><span data-stu-id="599ea-139">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-ngix-welcome-page"></a><span data-ttu-id="599ea-140">Afficher la page d’accueil NGNIX</span><span class="sxs-lookup"><span data-stu-id="599ea-140">View the NGIX welcome page</span></span>

<span data-ttu-id="599ea-141">Une fois NGINX installé et le port 80 ouvert sur votre machine virtuelle à partir d’Internet, vous pouvez utiliser un navigateur web de votre choix pour afficher la page d’accueil NGINX par défaut.</span><span class="sxs-lookup"><span data-stu-id="599ea-141">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="599ea-142">Veillez à utiliser l’adresse IP publique indiquée ci-dessus pour vous rendre sur la page par défaut.</span><span class="sxs-lookup"><span data-stu-id="599ea-142">Be sure to use the public IP address you documented above to visit the default page.</span></span> 

![Site par défaut NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="599ea-144">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="599ea-144">Clean up resources</span></span>

<span data-ttu-id="599ea-145">Lorsque vous n’en avez plus besoin, vous pouvez utiliser la commande [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="599ea-145">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="599ea-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="599ea-146">Next steps</span></span>

<span data-ttu-id="599ea-147">Dans ce guide de démarrage rapide, vous avez déployé une machine virtuelle simple ainsi qu’une règle de groupe de sécurité réseau, et installé un serveur web.</span><span class="sxs-lookup"><span data-stu-id="599ea-147">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="599ea-148">Pour en savoir plus sur les machines virtuelles Azure, suivez le didacticiel pour les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="599ea-148">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="599ea-149">Didacticiels sur les machines virtuelles Azure Linux</span><span class="sxs-lookup"><span data-stu-id="599ea-149">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
