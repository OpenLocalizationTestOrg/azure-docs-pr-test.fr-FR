---
title: "aaaCreate machine virtuelle Windows à l’aide de PowerShell dans la pile de Azure | Documents Microsoft"
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
ms.openlocfilehash: de063eae6f0782d8916da991f285a9de6b41def4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-by-using-powershell-in-azure-stack"></a><span data-ttu-id="8ced0-103">Créer une machine virtuelle Windows à l’aide de PowerShell dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8ced0-103">Create a Windows virtual machine by using PowerShell in Azure Stack</span></span>

<span data-ttu-id="8ced0-104">Machines virtuelles dans donnent Azure pile hello flexibilité de la virtualisation sans avoir toobuy et de mettre à jour hello matériel physique qui l’exécute.</span><span class="sxs-lookup"><span data-stu-id="8ced0-104">Virtual machines in Azure Stack give you hello flexibility of virtualization without having toobuy and maintain hello physical hardware that runs it.</span></span> <span data-ttu-id="8ced0-105">Lorsque vous utilisez des Machines virtuelles, comprenez qu’il existe des différences entre les fonctionnalités de hello qui sont disponibles dans Azure et de la pile d’Azure, consultez le toohello [considérations relatives à des machines virtuelles dans Azure pile](azure-stack-vm-considerations.md) toolearn rubrique sur Ces différences.</span><span class="sxs-lookup"><span data-stu-id="8ced0-105">When you use Virtual Machines, understand that there are some differences between hello features that are available in Azure and Azure Stack, refer toohello [Considerations for virtual machines in Azure Stack](azure-stack-vm-considerations.md) topic toolearn about these differences.</span></span> 

<span data-ttu-id="8ced0-106">Ce guide des détails à l’aide de PowerShell toocreate machine virtuelle Windows Server 2016 dans la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="8ced0-106">This guide details using PowerShell toocreate a Windows Server 2016 virtual machine in Azure Stack.</span></span> <span data-ttu-id="8ced0-107">Vous pouvez exécuter des étapes de hello décrits dans cet article hello Kit de développement Azure pile ou d’un client externe basé sur Windows, si vous êtes connecté via VPN.</span><span class="sxs-lookup"><span data-stu-id="8ced0-107">You can run hello steps described in this article either from hello Azure Stack Development Kit, or from a Windows-based external client if you are connected through VPN.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8ced0-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8ced0-108">Prerequisites</span></span>

1. <span data-ttu-id="8ced0-109">marketplace d’Azure pile Hello ne contient pas les images hello Windows Server 2016 par défaut.</span><span class="sxs-lookup"><span data-stu-id="8ced0-109">hello Azure Stack marketplace doesn't contain hello Windows Server 2016 image by default.</span></span> <span data-ttu-id="8ced0-110">Par conséquent, avant de pouvoir créer un ordinateur virtuel, assurez-vous que cet opérateur de pile de Azure hello [ajoute marketplace d’Azure pile hello Windows Server 2016 image toohello](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="8ced0-110">So, before you can create a virtual machine, make sure that hello Azure Stack operator [adds hello Windows Server 2016 image toohello Azure Stack marketplace](azure-stack-add-default-image.md).</span></span> 
2. <span data-ttu-id="8ced0-111">Pile Azure nécessite une version spécifique du toocreate du module Azure PowerShell et gérer les ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="8ced0-111">Azure Stack requires specific version of Azure PowerShell module toocreate and manage hello resources.</span></span> <span data-ttu-id="8ced0-112">Utilisez les étapes hello décrites dans [installer PowerShell pour Azure pile](azure-stack-powershell-install.md) version requise de rubrique tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="8ced0-112">Use hello steps described in [Install PowerShell for Azure Stack](azure-stack-powershell-install.md) topic tooinstall hello required version.</span></span>
3. [<span data-ttu-id="8ced0-113">Configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ced0-113">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md) 

## <a name="create-a-resource-group"></a><span data-ttu-id="8ced0-114">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="8ced0-114">Create a resource group</span></span>

<span data-ttu-id="8ced0-115">Un groupe de ressources est un conteneur logique dans lequel les ressources Azure Stack sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="8ced0-115">A resource group is a logical container into which Azure Stack resources are deployed and managed.</span></span> <span data-ttu-id="8ced0-116">Utilisez hello suivant le bloc de code toocreate un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8ced0-116">Use hello following code block toocreate a resource group.</span></span> <span data-ttu-id="8ced0-117">Nous avons affecté des valeurs à toutes les variables de ce document. Vous pouvez les utiliser en l’état ou affecter une valeur différente.</span><span class="sxs-lookup"><span data-stu-id="8ced0-117">We have assigned values for all variables in this document, you can use them as is or assign a different value.</span></span>  

```powershell
# Create variables toostore hello location and resource group names.
$location = "local"
$ResourceGroupName = "myResourceGroup"

New-AzureRmResourceGroup `
  -Name $ResourceGroupName `
  -Location $location
```

## <a name="create-storage-resources"></a><span data-ttu-id="8ced0-118">Créer des ressources de stockage</span><span class="sxs-lookup"><span data-stu-id="8ced0-118">Create storage resources</span></span> 

<span data-ttu-id="8ced0-119">Créer un compte de stockage et une image de stockage conteneur toostore hello Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="8ced0-119">Create a storage account, and a storage container toostore hello Windows Server 2016 image.</span></span>

```powershell
# Create variables toostore hello storage account name and hello storage account SKU information
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

# Create a storage container toostore hello virtual machine image
$containerName = 'osdisks'
$container = New-AzureStorageContainer `
  -Name $containerName `
  -Permission Blob
```

## <a name="create-networking-resources"></a><span data-ttu-id="8ced0-120">Création de ressources de mise en réseau</span><span class="sxs-lookup"><span data-stu-id="8ced0-120">Create networking resources</span></span>

<span data-ttu-id="8ced0-121">Créez un réseau virtuel, un sous-réseau et une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="8ced0-121">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="8ced0-122">Ces ressources sont utilisées tooprovide réseau connectivité toohello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8ced0-122">These resources are used tooprovide network connectivity toohello virtual machine.</span></span>  

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

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="8ced0-123">Créez un groupe de sécurité réseau et une règle de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="8ced0-123">Create a network security group and a network security group rule</span></span>

<span data-ttu-id="8ced0-124">groupe de sécurité réseau Hello sécurise hello virtuels à l’aide de règles de trafic entrants et sortants.</span><span class="sxs-lookup"><span data-stu-id="8ced0-124">hello network security group secures hello virtual machine by using inbound and outbound rules.</span></span> <span data-ttu-id="8ced0-125">Permet de créer une règle de trafic entrant pour le port 3389 tooallow Bureau à distance les connexions entrantes et une règle de trafic entrant pour le trafic web entrant port 80 tooallow.</span><span class="sxs-lookup"><span data-stu-id="8ced0-125">Lets create an inbound rule for port 3389 tooallow incoming Remote Desktop connections and an inbound rule for port 80 tooallow incoming web traffic.</span></span>

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
 
### <a name="create-a-network-card-for-hello-virtual-machine"></a><span data-ttu-id="8ced0-126">Créer une carte réseau pour la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="8ced0-126">Create a network card for hello virtual machine</span></span>

<span data-ttu-id="8ced0-127">carte réseau de Hello connecte le sous-réseau de tooa d’ordinateurs virtuels hello, groupe de sécurité réseau et adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="8ced0-127">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="8ced0-128">Création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8ced0-128">Create a virtual machine</span></span>

<span data-ttu-id="8ced0-129">Créez une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8ced0-129">Create a virtual machine configuration.</span></span> <span data-ttu-id="8ced0-130">configuration de Hello inclut des paramètres hello sont utilisées lors du déploiement d’ordinateur virtuel de hello telles que les informations d’identification, de la taille, de l’image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8ced0-130">hello configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, credentials.</span></span>

```powershell
# Define a credential object toostore hello username and password for hello virtual machine
$UserName='demouser'
$Password='Password@123'| ConvertTo-SecureString -Force -AsPlainText
$Credential=New-Object PSCredential($UserName,$Password)

# Create hello virtual machine configuration object
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

# Sets hello operating system disk properties on a virtual machine. 
$VirtualMachine = Set-AzureRmVMOSDisk `
  -VM $VirtualMachine `
  -Name $osDiskName `
  -VhdUri $OsDiskUri `
  -CreateOption FromImage | `
  Add-AzureRmVMNetworkInterface -Id $nic.Id 

#Create hello virtual machine.
New-AzureRmVM `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -VM $VirtualMachine
```

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="8ced0-131">Connecter l’ordinateur virtuel de toohello</span><span class="sxs-lookup"><span data-stu-id="8ced0-131">Connect toohello virtual machine</span></span>

<span data-ttu-id="8ced0-132">Une fois la machine virtuelle de hello est correctement créé, ouvrir une machine virtuelle de bureau à distance connexion toohello du kit de développement hello ou à partir d’un client externe Windows si vous êtes connecté via VPN.</span><span class="sxs-lookup"><span data-stu-id="8ced0-132">After hello virtual machine is successfully created, open a Remote Desktop connection toohello virtual machine from hello development kit, or from a Windows-based external client if you are connected through VPN.</span></span> <span data-ttu-id="8ced0-133">tooremote en machine virtuelle hello que vous avez créé à l’étape précédente de hello, vous avez besoin de son adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="8ced0-133">tooremote into hello virtual machine that you created in hello previous step, you need its public IP address.</span></span> <span data-ttu-id="8ced0-134">Exécutez hello suivant commande tooget hello adresse IP publique de l’ordinateur virtuel de hello :</span><span class="sxs-lookup"><span data-stu-id="8ced0-134">Run hello following command tooget hello public IP address of hello virtual machine:</span></span> 

```powershell
Get-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName | Select IpAddress
```
 
<span data-ttu-id="8ced0-135">La commande suivante de hello utilisation toocreate une session Bureau à distance avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="8ced0-135">Use hello following command toocreate a Remote Desktop session with hello virtual machine.</span></span> <span data-ttu-id="8ced0-136">Remplacez l’adresse IP de hello avec l’adresse IP publique hello de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8ced0-136">Replace hello IP address with hello publicIPAddress of your virtual machine.</span></span> <span data-ttu-id="8ced0-137">Lorsque vous y êtes invité, entrez le nom d’utilisateur hello et un mot de passe que vous avez utilisé lors de la création d’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="8ced0-137">When prompted, enter hello username and password that you used when creating hello virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```
## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="8ced0-138">Supprimer la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="8ced0-138">Delete hello virtual machine</span></span>

<span data-ttu-id="8ced0-139">Lorsque vous n’est plus nécessaire, utilisez hello suivant commande tooremove hello groupe de ressources qui contient l’ordinateur virtuel de hello et ses ressources connexes :</span><span class="sxs-lookup"><span data-stu-id="8ced0-139">When no longer needed, use hello following command tooremove hello resource group that contains hello virtual machine and its related resources:</span></span>

```powershell
Remove-AzureRmResourceGroup `
  -Name $ResourceGroupName
```

## <a name="next-steps"></a><span data-ttu-id="8ced0-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8ced0-140">Next steps</span></span>

<span data-ttu-id="8ced0-141">toolearn sur le stockage dans la pile d’Azure, consultez toohello [vue d’ensemble du stockage](azure-stack-storage-overview.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="8ced0-141">toolearn about Storage in Azure Stack, refer toohello [storage overview](azure-stack-storage-overview.md) topic.</span></span>

