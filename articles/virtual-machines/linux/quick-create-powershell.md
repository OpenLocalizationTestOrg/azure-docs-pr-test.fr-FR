---
title: "aaaAzure démarrage rapide : créer un PowerShell VM | Documents Microsoft"
description: "Apprenez rapidement à toocreate un les ordinateurs virtuels Linux avec PowerShell"
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
ms.openlocfilehash: f05ea7fedafe4fda660dc6084ae57ebf9dced473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="17d38-103">Créer une machine virtuelle Linux avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="17d38-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="17d38-104">module d’Azure PowerShell Hello est toocreate utilisé et gérer des ressources Azure à partir de la ligne de commande PowerShell hello ou dans des scripts.</span><span class="sxs-lookup"><span data-stu-id="17d38-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="17d38-105">Ce guide décrit en détail à l’aide de hello Azure PowerShell module toodeploy une machine virtuelle exécutant Ubuntu server.</span><span class="sxs-lookup"><span data-stu-id="17d38-105">This guide details using hello Azure PowerShell module toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="17d38-106">Une fois que le serveur de hello est déployé, une connexion SSH est créée, et un serveur Web NGINX est installé.</span><span class="sxs-lookup"><span data-stu-id="17d38-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="17d38-107">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="17d38-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="17d38-108">Ce démarrage rapide nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module.</span><span class="sxs-lookup"><span data-stu-id="17d38-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="17d38-109">Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="17d38-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="17d38-110">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="17d38-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="17d38-111">Enfin, une clé SSH publique avec le nom de hello *id_rsa.pub* doit toobe stockée Bonjour *.ssh* répertoire de votre profil utilisateur Windows.</span><span class="sxs-lookup"><span data-stu-id="17d38-111">Finally, a public SSH key with hello name *id_rsa.pub* needs toobe stored in hello *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="17d38-112">Pour plus d’informations sur la création de clés SSH pour Azure, consultez [Création de clés SSH pour Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="17d38-112">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="17d38-113">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="17d38-113">Log in tooAzure</span></span>

<span data-ttu-id="17d38-114">Connectez-vous à tooyour abonnement Azure avec hello `Login-AzureRmAccount` commande et suivez hello à l’écran.</span><span class="sxs-lookup"><span data-stu-id="17d38-114">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="17d38-115">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="17d38-115">Create resource group</span></span>

<span data-ttu-id="17d38-116">Créez un groupe de ressources Azure avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="17d38-116">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="17d38-117">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="17d38-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a><span data-ttu-id="17d38-118">Création de ressources de mise en réseau</span><span class="sxs-lookup"><span data-stu-id="17d38-118">Create networking resources</span></span>

<span data-ttu-id="17d38-119">Créez un réseau virtuel, un sous-réseau et une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="17d38-119">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="17d38-120">Ces ressources tooprovide utilisés de connectivité réseau toohello l’ordinateur virtuel et le connecter toohello internet.</span><span class="sxs-lookup"><span data-stu-id="17d38-120">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

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

<span data-ttu-id="17d38-121">Créez un groupe de sécurité réseau et une règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="17d38-121">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="17d38-122">groupe de sécurité réseau Hello sécurise la machine virtuelle de hello à l’aide des règles de trafic entrants et sortants.</span><span class="sxs-lookup"><span data-stu-id="17d38-122">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="17d38-123">Dans ce cas, une règle entrante est créée pour le port 22, qui autorise les connexions SSH.</span><span class="sxs-lookup"><span data-stu-id="17d38-123">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="17d38-124">Nous souhaitons également toocreate une règle de trafic entrant pour le port 80, qui autorise le trafic web entrant.</span><span class="sxs-lookup"><span data-stu-id="17d38-124">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

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

<span data-ttu-id="17d38-125">Créer une carte réseau avec [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) pour la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="17d38-125">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="17d38-126">carte réseau de Hello connecte le sous-réseau de tooa d’ordinateurs virtuels hello, groupe de sécurité réseau et adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="17d38-126">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="17d38-127">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="17d38-127">Create virtual machine</span></span>

<span data-ttu-id="17d38-128">Créez une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="17d38-128">Create a virtual machine configuration.</span></span> <span data-ttu-id="17d38-129">Cette configuration inclut des paramètres hello sont utilisées lors du déploiement d’ordinateur virtuel de hello comme une configuration de machine virtuelle image, la taille et l’authentification.</span><span class="sxs-lookup"><span data-stu-id="17d38-129">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

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

<span data-ttu-id="17d38-130">Créer la machine virtuelle hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="17d38-130">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="17d38-131">Connecter toovirtual machine</span><span class="sxs-lookup"><span data-stu-id="17d38-131">Connect toovirtual machine</span></span>

<span data-ttu-id="17d38-132">Après la fin du déploiement de hello, créez une connexion SSH avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="17d38-132">After hello deployment has completed, create an SSH connection with hello virtual machine.</span></span>

<span data-ttu-id="17d38-133">Hello d’utilisation [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) commande tooreturn hello adresse IP publique de l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="17d38-133">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="17d38-134">À partir d’un système avec SSH installé, suivant de hello utilisé la commande tooconnect toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="17d38-134">From a system with SSH installed, used hello following command tooconnect toohello virtual machine.</span></span> <span data-ttu-id="17d38-135">Si vous travaillez sur Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) peut être utilisé toocreate hello connexion.</span><span class="sxs-lookup"><span data-stu-id="17d38-135">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used toocreate hello connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="17d38-136">Lorsque vous y êtes invité, nom d’utilisateur hello est *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="17d38-136">When prompted, hello login user name is *azureuser*.</span></span> <span data-ttu-id="17d38-137">Si un mot de passe a été entré lors de la création de clés SSH, vous devez tooenter ce également.</span><span class="sxs-lookup"><span data-stu-id="17d38-137">If a passphrase was entered when creating SSH keys, you need tooenter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="17d38-138">Installer NGINX</span><span class="sxs-lookup"><span data-stu-id="17d38-138">Install NGINX</span></span>

<span data-ttu-id="17d38-139">Suivante de hello utilisez bash sources de package tooupdate de script et installer le dernier package de NGINX hello.</span><span class="sxs-lookup"><span data-stu-id="17d38-139">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a><span data-ttu-id="17d38-140">Page d’accueil de vue hello NGIX</span><span class="sxs-lookup"><span data-stu-id="17d38-140">View hello NGIX welcome page</span></span>

<span data-ttu-id="17d38-141">Avec NGINX installé et le port 80 maintenant ouvrir sur votre machine virtuelle à partir de hello Internet, vous pouvez utiliser un navigateur web de votre choix tooview hello par défaut NGINX page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="17d38-141">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="17d38-142">Être vraiment toouse hello adresse IP publique vous documenté au-dessus de la page par défaut toovisit hello.</span><span class="sxs-lookup"><span data-stu-id="17d38-142">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![Site par défaut NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="17d38-144">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="17d38-144">Clean up resources</span></span>

<span data-ttu-id="17d38-145">Lorsque vous n’est plus nécessaire, vous pouvez utiliser hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) groupe de ressources tooremove hello, machine virtuelle et toutes les ressources de la commande.</span><span class="sxs-lookup"><span data-stu-id="17d38-145">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="17d38-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="17d38-146">Next steps</span></span>

<span data-ttu-id="17d38-147">Dans ce guide de démarrage rapide, vous avez déployé une machine virtuelle simple ainsi qu’une règle de groupe de sécurité réseau, et installé un serveur web.</span><span class="sxs-lookup"><span data-stu-id="17d38-147">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="17d38-148">toolearn en savoir plus sur les machines virtuelles, continuer toohello didacticiel pour les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="17d38-148">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="17d38-149">Didacticiels sur les machines virtuelles Azure Linux</span><span class="sxs-lookup"><span data-stu-id="17d38-149">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
