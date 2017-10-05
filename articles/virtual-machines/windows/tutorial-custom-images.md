---
title: "Créer des images de machine virtuelle personnalisées avec Azure PowerShell | Microsoft Docs"
description: "Tutoriel : créez une image de machine virtuelle personnalisée à l’aide d’Azure PowerShell."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 96be2872a902a7d7063bf1dff7b4ca209a5b67c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="3e90f-103">Créer une image personnalisée d’une machine virtuelle Azure à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e90f-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="3e90f-104">Les images personnalisées sont comme des images de la Place de marché, sauf que vous les créez vous-même.</span><span class="sxs-lookup"><span data-stu-id="3e90f-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="3e90f-105">Les images personnalisées peuvent être utilisées pour amorcer des configurations comme le préchargement des applications, les configurations d’application et d’autres configurations de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="3e90f-105">Custom images can be used to bootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="3e90f-106">Ce didacticiel explique comment créer votre propre image personnalisée d’une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="3e90f-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="3e90f-107">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="3e90f-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3e90f-108">Exécuter Sysprep et généraliser les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="3e90f-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="3e90f-109">Créer une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="3e90f-109">Create a custom image</span></span>
> * <span data-ttu-id="3e90f-110">Créer une machine virtuelle à partir d’une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="3e90f-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="3e90f-111">Répertorier toutes les images dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="3e90f-111">List all the images in your subscription</span></span>
> * <span data-ttu-id="3e90f-112">Supprimer une image</span><span class="sxs-lookup"><span data-stu-id="3e90f-112">Delete an image</span></span>

<span data-ttu-id="3e90f-113">Ce didacticiel requiert le module Azure PowerShell version 3.6 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3e90f-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="3e90f-114">Exécutez ` Get-Module -ListAvailable AzureRM` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="3e90f-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="3e90f-115">Si vous devez effectuer une mise à niveau, consultez [Installer le module Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="3e90f-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3e90f-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="3e90f-116">Before you begin</span></span>

<span data-ttu-id="3e90f-117">Les étapes ci-dessous expliquent comment prendre une machine virtuelle existante et la transformer en une image personnalisée réutilisable que vous pouvez utiliser pour créer de nouvelles instances de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="3e90f-117">The steps below detail how to take an existing VM and turn it into a re-usable custom image that you can use to create new VM instances.</span></span>

<span data-ttu-id="3e90f-118">Pour exécuter l’exemple dans ce didacticiel, vous devez disposer d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3e90f-118">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="3e90f-119">Si nécessaire, cet [exemple de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) peut en créer une pour vous.</span><span class="sxs-lookup"><span data-stu-id="3e90f-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="3e90f-120">Au cours du didacticiel, remplacez les noms du groupe de ressources et de la machine virtuelle si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3e90f-120">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="3e90f-121">Préparer la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3e90f-121">Prepare VM</span></span>

<span data-ttu-id="3e90f-122">Pour créer une image de machine virtuelle, vous devez préparer la machine virtuelle en la généralisant, en la libérant et en la marquant comme généralisée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3e90f-122">To create an image of a virtual machine, you need to prepare the VM by generalizing the VM, deallocating, and then marking the source VM as generalized in Azure.</span></span>

### <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="3e90f-123">Généraliser la machine virtuelle Windows à l’aide de Sysprep</span><span class="sxs-lookup"><span data-stu-id="3e90f-123">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="3e90f-124">Sysprep supprime toutes les informations personnelles de votre compte, entre autres, et prépare la machine de façon à pouvoir l’utiliser comme image.</span><span class="sxs-lookup"><span data-stu-id="3e90f-124">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="3e90f-125">Pour plus d’informations sur Sysprep, voir [Introduction à l’utilisation de Sysprep](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e90f-125">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="3e90f-126">Connectez-vous à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3e90f-126">Connect to the virtual machine.</span></span>
2. <span data-ttu-id="3e90f-127">Ouvrez la fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="3e90f-127">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="3e90f-128">Remplacez le répertoire par *%windir%\system32\sysprep*, puis exécutez *sysprep.exe*.</span><span class="sxs-lookup"><span data-stu-id="3e90f-128">Change the directory to *%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="3e90f-129">Dans la boîte de dialogue **Outil de préparation du système**, sélectionnez *Entrer en mode OOBE (Out-of-Box Experience)* et vérifiez que la case *Généraliser* est cochée.</span><span class="sxs-lookup"><span data-stu-id="3e90f-129">In the **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that the *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="3e90f-130">Dans **Options d’arrêt**, sélectionnez *Arrêter*, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3e90f-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="3e90f-131">Une fois l’opération Sysprep terminée, elle arrête la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3e90f-131">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="3e90f-132">**Ne redémarrez pas la machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="3e90f-132">**Do not restart the VM**.</span></span>

### <a name="deallocate-and-mark-the-vm-as-generalized"></a><span data-ttu-id="3e90f-133">Libérer la machine virtuelle et la marquer comme généralisée</span><span class="sxs-lookup"><span data-stu-id="3e90f-133">Deallocate and mark the VM as generalized</span></span>

<span data-ttu-id="3e90f-134">Pour créer une image, la machine virtuelle doit être libérée et marquée comme généralisée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3e90f-134">To create an image, the VM needs to be deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="3e90f-135">Libérez la machine virtuelle à l’aide de [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="3e90f-135">Deallocated the VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="3e90f-136">Définissez l’état de la machine virtuelle sur `-Generalized` à l’aide de [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="3e90f-136">Set the status of the virtual machine to `-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-the-image"></a><span data-ttu-id="3e90f-137">Création de l’image</span><span class="sxs-lookup"><span data-stu-id="3e90f-137">Create the image</span></span>

<span data-ttu-id="3e90f-138">Créez à présent une image de la machine virtuelle à l’aide de [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) et [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span><span class="sxs-lookup"><span data-stu-id="3e90f-138">Now you can create an image of the VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="3e90f-139">L’exemple suivant crée une image nommée *myimage* à partir d’une machine virtuelle nommée *myimage*.</span><span class="sxs-lookup"><span data-stu-id="3e90f-139">The following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="3e90f-140">Accédez à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3e90f-140">Get the virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="3e90f-141">Créez la configuration de l’image.</span><span class="sxs-lookup"><span data-stu-id="3e90f-141">Create the image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="3e90f-142">Créez l’image.</span><span class="sxs-lookup"><span data-stu-id="3e90f-142">Create the image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-the-image"></a><span data-ttu-id="3e90f-143">Créer des machines virtuelles à partir de l’image</span><span class="sxs-lookup"><span data-stu-id="3e90f-143">Create VMs from the image</span></span>

<span data-ttu-id="3e90f-144">Maintenant que vous avez une image, vous pouvez créer une ou plusieurs nouvelles machines virtuelles à partir de l’image.</span><span class="sxs-lookup"><span data-stu-id="3e90f-144">Now that you have an image, you can create one or more new VMs from the image.</span></span> <span data-ttu-id="3e90f-145">La création d’une machine virtuelle à partir d’une image personnalisée est très similaire à la création d’une machine virtuelle à l’aide d’une image de la Place de marché.</span><span class="sxs-lookup"><span data-stu-id="3e90f-145">Creating a VM from a custom image is very similar to creating a VM using a Marketplace image.</span></span> <span data-ttu-id="3e90f-146">Lorsque vous utilisez une image de la Place de marché, vous devez entrer des informations sur l’image, le fournisseur de l’image, l’offre, la référence et la version.</span><span class="sxs-lookup"><span data-stu-id="3e90f-146">When you use a Marketplace image, you have to information about the image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="3e90f-147">Avec une image personnalisée, vous devez simplement fournir l’ID de la ressource d’image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="3e90f-147">With a custom image, you just need to provide the ID of the custom image resource.</span></span> 

<span data-ttu-id="3e90f-148">Dans le script suivant, nous créons une variable *$image* pour stocker des informations sur l’image personnalisée à l’aide de [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) et nous utilisons ensuite [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) et spécifions l’ID à l’aide de la variable *$image* que nous venons de créer.</span><span class="sxs-lookup"><span data-stu-id="3e90f-148">In the following script, we create a variable *$image* to store information about the custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify the ID using the *$image* variable we just created.</span></span> 

<span data-ttu-id="3e90f-149">Le script crée une machine virtuelle nommée *myVMfromImage* à partir de notre image personnalisée dans un groupe de ressources nommé *myResourceGroupFromImage* dans l’emplacement *Ouest des États-Unis*.</span><span class="sxs-lookup"><span data-stu-id="3e90f-149">The script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in the *West US* location.</span></span>


```powershell
$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

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

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable to store information about the image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want to create the VM from and image and provide the image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a><span data-ttu-id="3e90f-150">Gestion d’image</span><span class="sxs-lookup"><span data-stu-id="3e90f-150">Image management</span></span> 

<span data-ttu-id="3e90f-151">Voici quelques exemples de tâches d’images de gestion courantes et comment les exécuter à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e90f-151">Here are some examples of common management image tasks and how to complete them using PowerShell.</span></span>

<span data-ttu-id="3e90f-152">Répertoriez toutes les images par nom.</span><span class="sxs-lookup"><span data-stu-id="3e90f-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="3e90f-153">Supprimez une image.</span><span class="sxs-lookup"><span data-stu-id="3e90f-153">Delete an image.</span></span> <span data-ttu-id="3e90f-154">Cet exemple supprime l’image nommée *myOldImage* à partir du groupe *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="3e90f-154">This example deletes the image named *myOldImage* from the *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="3e90f-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3e90f-155">Next steps</span></span>

<span data-ttu-id="3e90f-156">Ce didacticiel vous montré comment créer une image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3e90f-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="3e90f-157">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="3e90f-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3e90f-158">Exécuter Sysprep et généraliser les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="3e90f-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="3e90f-159">Créer une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="3e90f-159">Create a custom image</span></span>
> * <span data-ttu-id="3e90f-160">Créer une machine virtuelle à partir d’une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="3e90f-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="3e90f-161">Répertorier toutes les images dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="3e90f-161">List all the images in your subscription</span></span>
> * <span data-ttu-id="3e90f-162">Supprimer une image</span><span class="sxs-lookup"><span data-stu-id="3e90f-162">Delete an image</span></span>

<span data-ttu-id="3e90f-163">Passez au didacticiel suivant pour en savoir plus sur les machines virtuelles hautement disponibles.</span><span class="sxs-lookup"><span data-stu-id="3e90f-163">Advance to the next tutorial to learn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3e90f-164">Créer des machines virtuelles hautement disponibles</span><span class="sxs-lookup"><span data-stu-id="3e90f-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)



