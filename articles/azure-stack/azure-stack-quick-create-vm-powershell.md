---
title: "Créer une machine virtuelle Windows à l’aide de PowerShell dans Azure Stack | Microsoft Docs"
description: "Créer une machine virtuelle Windows à l’aide de PowerShell dans Azure Stack."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 4b6706b289e323706009c40e9d1ad0149f8accc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-windows-virtual-machine-by-using-powershell-in-azure-stack"></a><span data-ttu-id="0b499-103">Créer une machine virtuelle Windows à l’aide de PowerShell dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="0b499-103">Create a Windows virtual machine by using PowerShell in Azure Stack</span></span>

<span data-ttu-id="0b499-104">Dans Azure Stack, les machines virtuelles vous donnent la flexibilité de la virtualisation sans devoir acheter le matériel physique qui l’exécute ni en assurer la maintenance.</span><span class="sxs-lookup"><span data-stu-id="0b499-104">Virtual machines in Azure Stack give you the flexibility of virtualization without having to buy and maintain the physical hardware that runs it.</span></span> <span data-ttu-id="0b499-105">Quand vous utilisez des machines virtuelles, vous devez savoir qu’il existe des différences entre les fonctionnalités disponibles dans Azure et celles disponibles dans Azure Stack. Reportez-vous à la rubrique [Considérations relatives aux machines virtuelles dans Azure Stack](azure-stack-vm-considerations.md) pour en savoir plus sur ces différences.</span><span class="sxs-lookup"><span data-stu-id="0b499-105">When you use Virtual Machines, understand that there are some differences between the features that are available in Azure and Azure Stack, refer to the [Considerations for virtual machines in Azure Stack](azure-stack-vm-considerations.md) topic to learn about these differences.</span></span> 

<span data-ttu-id="0b499-106">Ce guide explique comment utiliser PowerShell pour créer une machine virtuelle Windows Server 2016 dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="0b499-106">This guide details using PowerShell to create a Windows Server 2016 virtual machine in Azure Stack.</span></span> <span data-ttu-id="0b499-107">Vous pouvez exécuter les étapes décrites dans cet article à partir du Kit de développement Azure Stack ou à partir d’un client externe Windows si vous êtes connecté par le biais d’un VPN.</span><span class="sxs-lookup"><span data-stu-id="0b499-107">You can run the steps described in this article either from the Azure Stack Development Kit, or from a Windows-based external client if you are connected through VPN.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0b499-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0b499-108">Prerequisites</span></span>

1. <span data-ttu-id="0b499-109">La Place de Marché Azure Stack ne contient pas par défaut l’image Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="0b499-109">The Azure Stack marketplace doesn't contain the Windows Server 2016 image by default.</span></span> <span data-ttu-id="0b499-110">Par conséquent, avant de pouvoir créer une machine virtuelle, vérifiez que l’opérateur Azure Stack [ajoute l’image Windows Server 2016 à la Place de Marché Azure Stack](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="0b499-110">So, before you can create a virtual machine, make sure that the Azure Stack operator [adds the Windows Server 2016 image to the Azure Stack marketplace](azure-stack-add-default-image.md).</span></span> 
2. <span data-ttu-id="0b499-111">Azure Stack nécessite une version spécifique du module Azure PowerShell pour créer et gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="0b499-111">Azure Stack requires specific version of Azure PowerShell module to create and manage the resources.</span></span> <span data-ttu-id="0b499-112">Utilisez les étapes décrites dans la rubrique [Installer PowerShell pour Azure Stack](azure-stack-powershell-install.md) pour installer la version exigée.</span><span class="sxs-lookup"><span data-stu-id="0b499-112">Use the steps described in [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) topic to install the required version.</span></span>
3. [<span data-ttu-id="0b499-113">Configurer l’environnement PowerShell de l’utilisateur Azure Stack</span><span class="sxs-lookup"><span data-stu-id="0b499-113">Configure the Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md) 

## <a name="create-a-resource-group"></a><span data-ttu-id="0b499-114">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="0b499-114">Create a resource group</span></span>

<span data-ttu-id="0b499-115">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure Stack sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="0b499-115">A resource group is a logical container into which Azure Stack resources are deployed and managed.</span></span> <span data-ttu-id="0b499-116">Utilisez le bloc de code suivant pour créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0b499-116">Use the following code block to create a resource group.</span></span> <span data-ttu-id="0b499-117">Nous avons affecté des valeurs à toutes les variables de ce document. Vous pouvez les utiliser en l’état ou affecter une valeur différente.</span><span class="sxs-lookup"><span data-stu-id="0b499-117">We have assigned values for all variables in this document, you can use them as is or assign a different value.</span></span>  

```powershell
# Create variables to store the location and resource group names.
$location = "local"
$ResourceGroupName = "myResourceGroup"

New-AzureRmResourceGroup `
  -Name $ResourceGroupName `
  -Location $location
```

## <a name="create-storage-resources"></a><span data-ttu-id="0b499-118">Créer des ressources de stockage</span><span class="sxs-lookup"><span data-stu-id="0b499-118">Create storage resources</span></span> 

<span data-ttu-id="0b499-119">Créez un compte de stockage, ainsi qu’un conteneur de stockage pour stocker l’image Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="0b499-119">Create a storage account, and a storage container to store the Windows Server 2016 image.</span></span>

```powershell
# Create variables to store the storage account name and the storage account SKU information
$StorageAccountName = "mystorageaccount"
$SkuName = "Standard_LRS"

# Create a new storage account
$StorageAccount = New-AzureRMStorageAccount `
  -Location $location `
  -ResourceGroupName $ResourceGroupName `
  -Type $SkuName `
  -Name $StorageAccountName

Set-AzureRmCurrentStorageAccount `
  -StorageAccountName $storageAccountName `
  -ResourceGroupName $resourceGroupName

# Create a storage container to store the virtual machine image
$containerName = 'osdisks'
$container = New-AzureStorageContainer `
  -Name $containerName `
  -Permission Blob
```

## <a name="create-networking-resources"></a><span data-ttu-id="0b499-120">Création de ressources de mise en réseau</span><span class="sxs-lookup"><span data-stu-id="0b499-120">Create networking resources</span></span>

<span data-ttu-id="0b499-121">Créez un réseau virtuel, un sous-réseau et une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="0b499-121">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="0b499-122">Ces ressources sont utilisées pour fournir une connectivité réseau à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0b499-122">These resources are used to provide network connectivity to the virtual machine.</span></span>  

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name MyVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -AllocationMethod Static `
  -IdleTimeoutInMinutes 4 `
  -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="0b499-123">Créez un groupe de sécurité réseau et une règle de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="0b499-123">Create a network security group and a network security group rule</span></span>

<span data-ttu-id="0b499-124">Le groupe de sécurité réseau sécurise la machine virtuelle à l’aide de règles de trafic entrantes et sortantes.</span><span class="sxs-lookup"><span data-stu-id="0b499-124">The network security group secures the virtual machine by using inbound and outbound rules.</span></span> <span data-ttu-id="0b499-125">Créons une règle de trafic entrant pour le port 3389 pour autoriser les connexions Bureau à distance entrantes, et une règle de trafic entrant pour le port 80 pour autoriser le trafic web entrant.</span><span class="sxs-lookup"><span data-stu-id="0b499-125">Lets create an inbound rule for port 3389 to allow incoming Remote Desktop connections and an inbound rule for port 80 to allow incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRuleRDP `
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
  -Name myNetworkSecurityGroupRuleWWW `
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
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRuleRDP,$nsgRuleWeb 
```
 
### <a name="create-a-network-card-for-the-virtual-machine"></a><span data-ttu-id="0b499-126">Créer une carte réseau pour la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="0b499-126">Create a network card for the virtual machine</span></span>

<span data-ttu-id="0b499-127">La carte réseau connecte la machine virtuelle à un sous-réseau, un groupe de sécurité réseau et une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="0b499-127">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate it with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
  -Name myNic `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id `
  -NetworkSecurityGroupId $nsg.Id 
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="0b499-128">Création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="0b499-128">Create a virtual machine</span></span>

<span data-ttu-id="0b499-129">Créez une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0b499-129">Create a virtual machine configuration.</span></span> <span data-ttu-id="0b499-130">La configuration inclut les paramètres qui sont utilisés lors du déploiement de la machine virtuelle, comme une image, une taille et des informations d’identification de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0b499-130">The configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, credentials.</span></span>

```powershell
# Define a credential object to store the username and password for the virtual machine
$UserName='demouser'
$Password='Password@123'| ConvertTo-SecureString -Force -AsPlainText
$Credential=New-Object PSCredential($UserName,$Password)

# Create the virtual machine configuration object
$VmName = "VirtualMachinelatest"
$VmSize = "Standard_A1"
$VirtualMachine = New-AzureRmVMConfig `
  -VMName $VmName `
  -VMSize $VmSize 

$VirtualMachine = Set-AzureRmVMOperatingSystem `
  -VM $VirtualMachine `
  -Windows `
  -ComputerName "MainComputer" `
  -Credential $Credential 

$VirtualMachine = Set-AzureRmVMSourceImage `
  -VM $VirtualMachine `
  -PublisherName "MicrosoftWindowsServer" `
  -Offer "WindowsServer" `
  -Skus "2016-Datacenter" `
  -Version "latest"

$osDiskName = "OsDisk"
$osDiskUri = '{0}vhds/{1}-{2}.vhd' -f `
  $StorageAccount.PrimaryEndpoints.Blob.ToString(),`
  $vmName.ToLower(), `
  $osDiskName

# Sets the operating system disk properties on a virtual machine. 
$VirtualMachine = Set-AzureRmVMOSDisk `
  -VM $VirtualMachine `
  -Name $osDiskName `
  -VhdUri $OsDiskUri `
  -CreateOption FromImage | `
  Add-AzureRmVMNetworkInterface -Id $nic.Id 

#Create the virtual machine.
New-AzureRmVM `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -VM $VirtualMachine
```

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="0b499-131">Connectez-vous à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0b499-131">Connect to the virtual machine</span></span>

<span data-ttu-id="0b499-132">Une fois la machine virtuelle correctement créée, ouvrez une connexion Bureau à distance à la machine virtuelle à partir du kit de développement, ou à partir d’un client externe Windows si vous êtes connecté par le biais d’un VPN.</span><span class="sxs-lookup"><span data-stu-id="0b499-132">After the virtual machine is successfully created, open a Remote Desktop connection to the virtual machine from the development kit, or from a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="0b499-133">Pour accéder à distance à la machine virtuelle créée à l’étape précédente, vous avez besoin de son adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="0b499-133">To remote into the virtual machine that you created in the previous step, you need its public IP address.</span></span> <span data-ttu-id="0b499-134">Exécutez la commande suivante pour obtenir l’adresse IP publique de la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="0b499-134">Run the following command to get the public IP address of the virtual machine:</span></span> 

```powershell
Get-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName | Select IpAddress
```
 
<span data-ttu-id="0b499-135">Utilisez la commande suivante pour créer une session Bureau à distance avec la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0b499-135">Use the following command to create a Remote Desktop session with the virtual machine.</span></span> <span data-ttu-id="0b499-136">Remplacez l’adresse IP par l’adresse publicIPAddress de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0b499-136">Replace the IP address with the publicIPAddress of your virtual machine.</span></span> <span data-ttu-id="0b499-137">Quand vous y êtes invité, entrez le nom d’utilisateur et le mot de passe que vous avez utilisés lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0b499-137">When prompted, enter the username and password that you used when creating the virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```
## <a name="delete-the-virtual-machine"></a><span data-ttu-id="0b499-138">Supprimer la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="0b499-138">Delete the virtual machine</span></span>

<span data-ttu-id="0b499-139">Quand vous n’en avez plus besoin, utilisez la commande suivante pour supprimer le groupe de ressources qui contient la machine virtuelle et les ressources qui lui sont associées :</span><span class="sxs-lookup"><span data-stu-id="0b499-139">When no longer needed, use the following command to remove the resource group that contains the virtual machine and its related resources:</span></span>

```powershell
Remove-AzureRmResourceGroup `
  -Name $ResourceGroupName
```

## <a name="next-steps"></a><span data-ttu-id="0b499-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0b499-140">Next steps</span></span>

<span data-ttu-id="0b499-141">Pour en savoir plus sur le stockage dans Azure Stack, reportez-vous à la rubrique [Vue d’ensemble du stockage](azure-stack-storage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0b499-141">To learn about Storage in Azure Stack, refer to the [storage overview](azure-stack-storage-overview.md) topic.</span></span>

