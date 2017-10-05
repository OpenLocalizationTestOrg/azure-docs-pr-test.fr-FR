---
title: "Créer une image non managée d’une machine virtuelle généralisée dans Azure | Microsoft Docs"
description: "Créez une image non managé d’une machine virtuelle Windows généralisée à utiliser pour créer plusieurs copies d’une machine virtuelle dans Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: d7f4a9558175835eba9096e6845726f21c7459d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="dfc82-103">Comment créer une image de machine virtuelle non managée à partir d’une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="dfc82-103">How to create an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="dfc82-104">Cet article traite de l’utilisation de comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="dfc82-104">This article covers using storage accounts.</span></span> <span data-ttu-id="dfc82-105">Nous vous recommandons d’utiliser des disques managés et des images managées plutôt qu’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dfc82-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="dfc82-106">Pour plus d’informations, consultez [Capturer une image managée d’une machine virtuelle généralisée dans Azure](capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="dfc82-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="dfc82-107">Cet article vous montre comment utiliser Azure PowerShell pour créer une image d’une machine virtuelle Azure généralisée à l’aide d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dfc82-107">This article shows you how to use Azure PowerShell to create an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="dfc82-108">Vous pouvez ensuite utiliser l’image pour créer une autre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dfc82-108">You can then use the image to create another VM.</span></span> <span data-ttu-id="dfc82-109">L’image comprend le disque du système d’exploitation, ainsi que les disques de données attachés à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dfc82-109">The image includes the OS disk and the data disks that are attached to the virtual machine.</span></span> <span data-ttu-id="dfc82-110">L’image n’inclut pas les ressources du réseau virtuel. Vous devez donc configurer les ressources lorsque vous créez la nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dfc82-110">The image doesn't include the virtual network resources, so you need to set up those resources when you create the new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dfc82-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dfc82-111">Prerequisites</span></span>
<span data-ttu-id="dfc82-112">Vous devez disposer d’une installation d’Azure PowerShell version 1.0.x ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="dfc82-112">You need to have Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="dfc82-113">Si vous n’avez pas déjà installé PowerShell, consultez la rubrique [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="dfc82-113">If you haven't already installed PowerShell, read [How to install and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-the-vm"></a><span data-ttu-id="dfc82-114">Généraliser la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="dfc82-114">Generalize the VM</span></span> 
<span data-ttu-id="dfc82-115">Cette section vous montre comment généraliser votre machine virtuelle Windows de façon à l’utiliser comme image.</span><span class="sxs-lookup"><span data-stu-id="dfc82-115">This section shows you how to generalize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="dfc82-116">La généralisation d’une machine virtuelle supprime toutes les informations personnelles de votre compte, entre autres, et prépare la machine de façon à pouvoir l’utiliser comme image.</span><span class="sxs-lookup"><span data-stu-id="dfc82-116">Generalizing a VM removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="dfc82-117">Pour plus d’informations sur Sysprep, voir [Introduction à l’utilisation de Sysprep](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="dfc82-117">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="dfc82-118">Vérifiez que les rôles serveur exécutés sur la machine sont pris en charge par Sysprep.</span><span class="sxs-lookup"><span data-stu-id="dfc82-118">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="dfc82-119">Pour plus d’informations, consultez [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="dfc82-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dfc82-120">Si vous chargez votre disque dur virtuel sur Azure pour la première fois, vérifiez que vous avez [préparé votre machine virtuelle](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avant d’exécuter Sysprep.</span><span class="sxs-lookup"><span data-stu-id="dfc82-120">If you are uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="dfc82-121">Vous pouvez également généraliser une machine virtuelle Linux à l’aide de `sudo waagent -deprovision+user`, puis utiliser PowerShell pour capturer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dfc82-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell to capture the VM.</span></span> <span data-ttu-id="dfc82-122">Pour plus d’informations sur l’utilisation de l’interface de ligne de commande pour capturer une machine virtuelle, consultez [Guide pratique pour généraliser et capturer une machine virtuelle Linux à l’aide de l’interface de ligne de commande Azure](../linux/capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="dfc82-122">For information about using the CLI to capture a VM, see [How to generalize and capture a Linux virtual machine using the Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="dfc82-123">Connectez-vous à la machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="dfc82-123">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="dfc82-124">Ouvrez la fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dfc82-124">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="dfc82-125">Remplacez le répertoire par **%windir%\system32\sysprep**, puis exécutez `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="dfc82-125">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="dfc82-126">Dans la boîte de dialogue **Outil de préparation du système**, sélectionnez **Entrer en mode OOBE (Out-of-Box Experience)** et vérifiez que la case **Généraliser** est cochée.</span><span class="sxs-lookup"><span data-stu-id="dfc82-126">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="dfc82-127">Dans **Options d’arrêt**, sélectionnez **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="dfc82-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="dfc82-128">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="dfc82-128">Click **OK**.</span></span>
   
    ![Démarrer Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="dfc82-130">Une fois l’opération Sysprep terminée, elle arrête la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dfc82-130">When Sysprep completes, it shuts down the virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="dfc82-131">Ne redémarrez pas la machine virtuelle tant que vous n’avez pas terminé de télécharger le disque dur virtuel dans Azure ou de créer une image à partir de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dfc82-131">Do not restart the VM until you are done uploading the VHD to Azure or creating an image from the VM.</span></span> <span data-ttu-id="dfc82-132">Si la machine virtuelle est accidentellement redémarrée, exécutez Sysprep pour la généraliser à nouveau.</span><span class="sxs-lookup"><span data-stu-id="dfc82-132">If the VM accidentally gets restarted, run Sysprep to generalize it again.</span></span>
> 
> 

## <a name="log-in-to-azure-powershell"></a><span data-ttu-id="dfc82-133">Connexion à Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfc82-133">Log in to Azure PowerShell</span></span>
1. <span data-ttu-id="dfc82-134">Ouvrez Azure PowerShell et connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="dfc82-134">Open Azure PowerShell and sign in to your Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="dfc82-135">Une fenêtre contextuelle s’ouvre pour vous permettre d’entrer les informations d’identification de votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="dfc82-135">A pop-up window opens for you to enter your Azure account credentials.</span></span>
2. <span data-ttu-id="dfc82-136">Obtenez les ID d’abonnement de vos abonnements disponibles.</span><span class="sxs-lookup"><span data-stu-id="dfc82-136">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="dfc82-137">Définissez l’abonnement approprié à l’aide de l’ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="dfc82-137">Set the correct subscription using the subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-the-vm-and-set-the-state-to-generalized"></a><span data-ttu-id="dfc82-138">Libération de la machine virtuelle et définition de l’état sur généralisé</span><span class="sxs-lookup"><span data-stu-id="dfc82-138">Deallocate the VM and set the state to generalized</span></span>
1. <span data-ttu-id="dfc82-139">Libérez les ressources de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dfc82-139">Deallocate the VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="dfc82-140">*L’état* de la machine virtuelle dans le Portail Azure passe de **Arrêté** à **Arrêté (libéré)**.</span><span class="sxs-lookup"><span data-stu-id="dfc82-140">The *Status* for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="dfc82-141">Définissez l’état de la machine virtuelle sur **Généralisé**.</span><span class="sxs-lookup"><span data-stu-id="dfc82-141">Set the status of the virtual machine to **Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="dfc82-142">Vérifiez l’état de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="dfc82-142">Check the status of the VM.</span></span> <span data-ttu-id="dfc82-143">La section **OSState/généralisé** pour la machine virtuelle doit avoir la valeur de **DisplayStatus** définie sur **Machine virtuelle généralisée**.</span><span class="sxs-lookup"><span data-stu-id="dfc82-143">The **OSState/generalized** section for the VM should have the **DisplayStatus** set to **VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-the-image"></a><span data-ttu-id="dfc82-144">Création de l’image</span><span class="sxs-lookup"><span data-stu-id="dfc82-144">Create the image</span></span>

<span data-ttu-id="dfc82-145">Créez une image de machine virtuelle non gérée dans le conteneur de stockage de destination à l’aide de cette commande.</span><span class="sxs-lookup"><span data-stu-id="dfc82-145">Create an unmanaged virtual machine image in the destination storage container using this command.</span></span> <span data-ttu-id="dfc82-146">L’image est créée dans le même compte de stockage que la machine virtuelle d’origine.</span><span class="sxs-lookup"><span data-stu-id="dfc82-146">The image is created in the same storage account as the original virtual machine.</span></span> <span data-ttu-id="dfc82-147">Le paramètre `-Path` enregistre une copie du modèle JSON pour la machine virtuelle source sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="dfc82-147">The `-Path` parameter saves a copy of the JSON template for the source VM to your local computer.</span></span> <span data-ttu-id="dfc82-148">Le paramètre `-DestinationContainerName` est le nom du conteneur dans lequel vous souhaitez stocker vos images.</span><span class="sxs-lookup"><span data-stu-id="dfc82-148">The `-DestinationContainerName` parameter is the name of the container that you want to hold your images.</span></span> <span data-ttu-id="dfc82-149">Si le conteneur n’existe pas, il est créé pour vous.</span><span class="sxs-lookup"><span data-stu-id="dfc82-149">If the container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="dfc82-150">Vous pouvez obtenir l’URL de l’image à partir du modèle de fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="dfc82-150">You can get the URL of your image from the JSON file template.</span></span> <span data-ttu-id="dfc82-151">Accédez à la section **resources** > **storageProfile** > **osDisk** > **image** > **uri** pour obtenir le chemin d’accès complet de votre image.</span><span class="sxs-lookup"><span data-stu-id="dfc82-151">Go to the **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for the complete path of your image.</span></span> <span data-ttu-id="dfc82-152">L’URL de l’image ressemble a le format suivant : `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="dfc82-152">The URL of the image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="dfc82-153">Vous pouvez également vérifier l’URI dans le portail.</span><span class="sxs-lookup"><span data-stu-id="dfc82-153">You can also verify the URI in the portal.</span></span> <span data-ttu-id="dfc82-154">L’image est copiée dans un conteneur nommé **system** dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="dfc82-154">The image is copied to a container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-the-image"></a><span data-ttu-id="dfc82-155">Créer une machine virtuelle à partir de l’image</span><span class="sxs-lookup"><span data-stu-id="dfc82-155">Create a VM from the image</span></span>

<span data-ttu-id="dfc82-156">Vous pouvez maintenant créer une ou plusieurs machines virtuelles à partir de l’image non managée.</span><span class="sxs-lookup"><span data-stu-id="dfc82-156">Now you can create one or more VMs from the unmanaged image.</span></span>

### <a name="set-the-uri-of-the-vhd"></a><span data-ttu-id="dfc82-157">Définir l’URI du disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="dfc82-157">Set the URI of the VHD</span></span>

<span data-ttu-id="dfc82-158">L’URI du disque dur virtuel à utiliser est au format : https://**moncomptedestockage**.blob.core.windows.net/**monconteneur**/**mondisquedurvirtuel**.vhd.</span><span class="sxs-lookup"><span data-stu-id="dfc82-158">The URI for the VHD to use is in the format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="dfc82-159">Dans cet exemple, le disque dur virtuel nommé **mondisquedurvirtuel** se trouve dans le compte de stockage **moncomptedestockage** dans le conteneur **monconteneur**.</span><span class="sxs-lookup"><span data-stu-id="dfc82-159">In this example the VHD named **myVHD** is in the storage account **mystorageaccount** in the container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="dfc82-160">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="dfc82-160">Create a virtual network</span></span>
<span data-ttu-id="dfc82-161">Créez le réseau virtuel et le sous-réseau du [réseau virtuel](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dfc82-161">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="dfc82-162">Créez le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="dfc82-162">Create the subnet.</span></span> <span data-ttu-id="dfc82-163">L’exemple suivant crée un sous-réseau nommé **mySubnet** dans le groupe de ressources **myResourceGroup** avec le préfixe d’adresse **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="dfc82-163">The following sample creates a subnet named **mySubnet** in the resource group **myResourceGroup** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="dfc82-164">Création du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="dfc82-164">Create the virtual network.</span></span> <span data-ttu-id="dfc82-165">L’exemple suivant crée un réseau virtuel nommé **myVnet** à l’emplacement **Ouest des États-Unis** avec le préfixe d’adresse **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="dfc82-165">The following sample creates a virtual network named **myVnet** in the **West US** location with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="dfc82-166">Création d'une adresse IP publique et une interface réseau</span><span class="sxs-lookup"><span data-stu-id="dfc82-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="dfc82-167">Pour établir la communication avec la machine virtuelle dans le réseau virtuel, vous avez besoin d’une [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) et d’une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="dfc82-167">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="dfc82-168">Créez une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="dfc82-168">Create a public IP address.</span></span> <span data-ttu-id="dfc82-169">Cet exemple crée une adresse IP publique nommée **myPip**.</span><span class="sxs-lookup"><span data-stu-id="dfc82-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="dfc82-170">Créez la carte réseau.</span><span class="sxs-lookup"><span data-stu-id="dfc82-170">Create the NIC.</span></span> <span data-ttu-id="dfc82-171">Cet exemple crée une carte réseau nommée **myNic**.</span><span class="sxs-lookup"><span data-stu-id="dfc82-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="dfc82-172">Créer le groupe de sécurité réseau et une règle RDP</span><span class="sxs-lookup"><span data-stu-id="dfc82-172">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="dfc82-173">Pour pouvoir vous connecter à votre machine virtuelle avec le protocole RDP, vous devez disposer d’une règle de sécurité qui autorise l’accès RDP sur le port 3389.</span><span class="sxs-lookup"><span data-stu-id="dfc82-173">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="dfc82-174">Cet exemple crée un groupe de sécurité réseau nommé **myNsg** qui contient une règle nommée **myRdpRule** autorisant le trafic RDP sur le port 3389.</span><span class="sxs-lookup"><span data-stu-id="dfc82-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="dfc82-175">Pour plus d’informations sur les groupes de sécurité réseau, consultez [Ouverture de ports sur une machine virtuelle dans Azure avec PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dfc82-175">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="dfc82-176">Créer une variable pour le réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="dfc82-176">Create a variable for the virtual network</span></span>
<span data-ttu-id="dfc82-177">Créez une variable pour le réseau virtuel terminé.</span><span class="sxs-lookup"><span data-stu-id="dfc82-177">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-the-vm"></a><span data-ttu-id="dfc82-178">Création de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="dfc82-178">Create the VM</span></span>
<span data-ttu-id="dfc82-179">Le script PowerShell suivant effectue les configurations de machine virtuelle et utilise l’image non managée comme source de la nouvelle installation.</span><span class="sxs-lookup"><span data-stu-id="dfc82-179">The following PowerShell completes the virtual machine configurations and uses unmanaged image as the source for the new installation.</span></span>

</br>

```powershell
    # Enter a new user name and password to use as the local administrator account 
    # for remotely accessing the VM.
    $cred = Get-Credential

    # Name of the storage account where the VHD is located. This example sets the 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of the virtual machine. This example sets the VM name as "myVM".
    $vmName = "myVM"

    # Size of the virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See the VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for the VM. This examples sets the computer name as "myComputer".
    $computerName = "myComputer"

    # Name of the disk that holds the OS. This example sets the 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets the SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get the storage account where the uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set the VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set the Windows operating system configuration and add the NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create the OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure the OS disk to be created from the existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create the new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="dfc82-180">Vérifier que la machine virtuelle a été créée</span><span class="sxs-lookup"><span data-stu-id="dfc82-180">Verify that the VM was created</span></span>
<span data-ttu-id="dfc82-181">Lorsque vous avez terminé, vous devez voir la machine virtuelle nouvellement créée dans le [Portail Azure](https://portal.azure.com) sous **Parcourir** > **Machines virtuelles** ou en utilisant les commandes PowerShell suivantes :</span><span class="sxs-lookup"><span data-stu-id="dfc82-181">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="dfc82-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dfc82-182">Next steps</span></span>
<span data-ttu-id="dfc82-183">Pour gérer votre nouvelle machine virtuelle avec Azure PowerShell, consultez [Gestion des machines virtuelles Azure à l’aide de modèles Resource Manager et de PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dfc82-183">To manage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


