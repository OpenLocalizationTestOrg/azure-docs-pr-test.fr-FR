---
title: "aaaCreate machine virtuelle à partir d’une image managée de la machine virtuelle dans Azure | Documents Microsoft"
description: "Créer une machine virtuelle Windows à partir d’une image de machine virtuelle managée généralisée à l’aide d’Azure PowerShell, dans le modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a><span data-ttu-id="f64fb-103">Créer une machine virtuelle à partir d’une image gérée</span><span class="sxs-lookup"><span data-stu-id="f64fb-103">Create a VM from a managed image</span></span>

<span data-ttu-id="f64fb-104">Vous pouvez créer plusieurs machines virtuelles à partir d’une image de machine virtuelle managée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f64fb-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="f64fb-105">Une image de machine virtuelle gérée contient hello informations toocreate nécessaire une machine virtuelle, y compris les disques du système d’exploitation et les données de hello.</span><span class="sxs-lookup"><span data-stu-id="f64fb-105">A managed VM image contains hello information necessary toocreate a VM, including hello OS and data disks.</span></span> <span data-ttu-id="f64fb-106">Hello disques durs virtuels qui composent l’image hello, y compris les disques hello du système d’exploitation et les disques de données, sont stockées en tant que disques gérés.</span><span class="sxs-lookup"><span data-stu-id="f64fb-106">hello VHDs that make up hello image, including both hello OS disks and any data disks, are stored as managed disks.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="f64fb-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f64fb-107">Prerequisites</span></span>

<span data-ttu-id="f64fb-108">Vous devez toohave déjà [créé une image de machine virtuelle gérée](capture-image-resource.md) toouse pour la création de hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f64fb-108">You need toohave already [created a managed VM image](capture-image-resource.md) toouse for creating hello new VM.</span></span> 

<span data-ttu-id="f64fb-109">Assurez-vous que vous disposez des versions les plus récentes des modules de AzureRM.Compute et AzureRM.Network PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="f64fb-109">Make sure that you have hello latest versions of hello AzureRM.Compute and AzureRM.Network PowerShell modules.</span></span> <span data-ttu-id="f64fb-110">Ouvrez une invite PowerShell en tant qu’administrateur et exécutez hello suivant commande tooinstall les.</span><span class="sxs-lookup"><span data-stu-id="f64fb-110">Open a PowerShell prompt as an Administrator and run hello following command tooinstall them.</span></span>

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
<span data-ttu-id="f64fb-111">Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f64fb-111">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>



## <a name="collect-information-about-hello-image"></a><span data-ttu-id="f64fb-112">Collecter des informations sur l’image de hello</span><span class="sxs-lookup"><span data-stu-id="f64fb-112">Collect information about hello image</span></span>

<span data-ttu-id="f64fb-113">Tout d’abord, nous toogather les informations de base sur l’image de hello et créez une variable pour l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="f64fb-113">First we need toogather basic information about hello image and create a variable for hello image.</span></span> <span data-ttu-id="f64fb-114">Cet exemple utilise une image de machine virtuelle gérée nommée **myImage** qui est en hello **myResourceGroup** groupe de ressources dans hello **ouest des États-Unis** emplacement.</span><span class="sxs-lookup"><span data-stu-id="f64fb-114">This example uses a managed VM image named **myImage** that is in hello **myResourceGroup** resource group in hello **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="f64fb-115">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f64fb-115">Create a virtual network</span></span>
<span data-ttu-id="f64fb-116">Créer le réseau virtuel de hello et un sous-réseau de hello [réseau virtuel](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f64fb-116">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="f64fb-117">Créer un sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="f64fb-117">Create hello subnet.</span></span> <span data-ttu-id="f64fb-118">Cet exemple crée un sous-réseau nommé **mySubnet** avec le préfixe d’adresse de hello **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="f64fb-118">This example creates a subnet named **mySubnet** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="f64fb-119">Créer un réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="f64fb-119">Create hello virtual network.</span></span> <span data-ttu-id="f64fb-120">Cet exemple crée un réseau virtuel nommé **myVnet** avec le préfixe d’adresse de hello **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="f64fb-120">This example creates a virtual network named **myVnet** with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="f64fb-121">Création d'une adresse IP publique et une interface réseau</span><span class="sxs-lookup"><span data-stu-id="f64fb-121">Create a public IP address and network interface</span></span>

<span data-ttu-id="f64fb-122">tooenable une communication avec l’ordinateur virtuel de hello dans le réseau virtuel de hello, vous devez un [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) et une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="f64fb-122">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="f64fb-123">Créez une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="f64fb-123">Create a public IP address.</span></span> <span data-ttu-id="f64fb-124">Cet exemple crée une adresse IP publique nommée **myPip**.</span><span class="sxs-lookup"><span data-stu-id="f64fb-124">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="f64fb-125">Créer la carte de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="f64fb-125">Create hello NIC.</span></span> <span data-ttu-id="f64fb-126">Cet exemple crée une carte réseau nommée **myNic**.</span><span class="sxs-lookup"><span data-stu-id="f64fb-126">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="f64fb-127">Créer une règle RDP et groupe de sécurité réseau hello</span><span class="sxs-lookup"><span data-stu-id="f64fb-127">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="f64fb-128">toolog en mesure de toobe dans tooyour machine virtuelle à l’aide du protocole RDP, vous devez toohave une règle de sécurité réseau (NSG) qui autorise l’accès RDP sur le port 3389.</span><span class="sxs-lookup"><span data-stu-id="f64fb-128">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="f64fb-129">Cet exemple crée un groupe de sécurité réseau nommé **myNsg** qui contient une règle nommée **myRdpRule** autorisant le trafic RDP sur le port 3389.</span><span class="sxs-lookup"><span data-stu-id="f64fb-129">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="f64fb-130">Pour plus d’informations sur les groupes de sécurité réseau, consultez [l’ouverture de ports tooa machine virtuelle dans Azure à l’aide de PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f64fb-130">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="f64fb-131">Créez une variable pour le réseau virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="f64fb-131">Create a variable for hello virtual network</span></span>

<span data-ttu-id="f64fb-132">Créez une variable pour le réseau virtuel de hello s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="f64fb-132">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="f64fb-133">Obtenir des informations d’identification de hello pour hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f64fb-133">Get hello credentials for hello VM</span></span>

<span data-ttu-id="f64fb-134">Hello applet de commande suivante ouvre une fenêtre dans laquelle vous entrerez un toouse nouveau du nom et mot de passe utilisateur en tant que compte d’administrateur local hello pour accéder à distance aux hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f64fb-134">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a><span data-ttu-id="f64fb-135">Les variables définies pour hello VM name, nom de l’ordinateur et hello taille de machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="f64fb-135">Set variables for hello VM name, computer name and hello size of hello VM</span></span>

1. <span data-ttu-id="f64fb-136">Créer des variables pour nom d’ordinateur virtuel hello et le nom de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f64fb-136">Create variables for hello VM name and computer name.</span></span> <span data-ttu-id="f64fb-137">Cet exemple définit le nom de machine virtuelle hello en tant que **myVM** et nom de l’ordinateur en tant que hello **poste de travail**.</span><span class="sxs-lookup"><span data-stu-id="f64fb-137">This example sets hello VM name as **myVM** and hello computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="f64fb-138">Définir la taille hello de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="f64fb-138">Set hello size of hello virtual machine.</span></span> <span data-ttu-id="f64fb-139">Cet exemple crée une machine virtuelle de taille **Standard_DS1_v2**.</span><span class="sxs-lookup"><span data-stu-id="f64fb-139">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="f64fb-140">Consultez hello [tailles de machine virtuelle](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="f64fb-140">See hello [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="f64fb-141">Ajoutez hello nom d’ordinateur virtuel et configuration d’ordinateur virtuel de taille toohello.</span><span class="sxs-lookup"><span data-stu-id="f64fb-141">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="f64fb-142">Image de machine virtuelle hello ensemble en tant qu’image source pour hello nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f64fb-142">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="f64fb-143">Définir l’image source de hello à l’aide de code hello d’image de machine virtuelle hello géré.</span><span class="sxs-lookup"><span data-stu-id="f64fb-143">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="f64fb-144">Définir la configuration du système d’exploitation hello et ajouter de carte réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="f64fb-144">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="f64fb-145">Entrez le type de stockage de hello (PremiumLRS ou StandardLRS) et la taille de hello du disque du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="f64fb-145">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="f64fb-146">Cet exemple définit le type de compte hello trop**PremiumLRS**, hello trop de taille de disque**128 Go** et mise en cache disque trop**ReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="f64fb-146">This example sets hello account type too**PremiumLRS**, hello disk size too**128 GB** and disk caching too**ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="f64fb-147">Créer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f64fb-147">Create hello VM</span></span>

<span data-ttu-id="f64fb-148">Créer hello nouvelle machine virtuelle à l’aide de la configuration de hello que nous avons généré et stocké dans hello **$vm** variable.</span><span class="sxs-lookup"><span data-stu-id="f64fb-148">Create hello new Vm using hello configuration that we have built and stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="f64fb-149">Vérifiez que hello que machine virtuelle a été créée.</span><span class="sxs-lookup"><span data-stu-id="f64fb-149">Verify that hello VM was created</span></span>
<span data-ttu-id="f64fb-150">Lorsque vous avez terminé, vous devez voir hello nouvellement créé VM dans hello [portail Azure](https://portal.azure.com) sous **Parcourir** > **virtuels**, ou en utilisant hello Commandes PowerShell :</span><span class="sxs-lookup"><span data-stu-id="f64fb-150">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="f64fb-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f64fb-151">Next steps</span></span>
<span data-ttu-id="f64fb-152">reportez-vous à votre nouvelle machine virtuelle avec Azure PowerShell, toomanage [créer et gérer des machines virtuelles Windows avec module d’Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f64fb-152">toomanage your new virtual machine with Azure PowerShell, see [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

