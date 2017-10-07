---
title: "images de machine virtuelle personnalisées aaaCreate avec hello Azure PowerShell | Documents Microsoft"
description: "Didacticiel : créer une image de machine virtuelle personnalisée à l’aide de hello Azure PowerShell."
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
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="2f5fa-103">Créer une image personnalisée d’une machine virtuelle Azure à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f5fa-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="2f5fa-104">Les images personnalisées sont comme des images de la Place de marché, sauf que vous les créez vous-même.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="2f5fa-105">Images personnalisées peuvent être des configurations toobootstrap utilisés tels que le préchargement des applications, les configurations de l’application et les autres configurations de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="2f5fa-106">Ce didacticiel explique comment créer votre propre image personnalisée d’une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="2f5fa-107">Vous allez apprendre à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f5fa-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2f5fa-108">Exécuter Sysprep et généraliser les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="2f5fa-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="2f5fa-109">Créer une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="2f5fa-109">Create a custom image</span></span>
> * <span data-ttu-id="2f5fa-110">Créer une machine virtuelle à partir d’une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="2f5fa-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="2f5fa-111">La liste de toutes les images hello dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="2f5fa-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="2f5fa-112">Supprimer une image</span><span class="sxs-lookup"><span data-stu-id="2f5fa-112">Delete an image</span></span>

<span data-ttu-id="2f5fa-113">Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="2f5fa-114">Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="2f5fa-115">Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="2f5fa-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2f5fa-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="2f5fa-116">Before you begin</span></span>

<span data-ttu-id="2f5fa-117">étapes Hello ci-dessous décrit en détail comment tootake une machine virtuelle existante et les activer dans personnalisé réutilisable de l’image que vous peuvent utiliser toocreate de nouvelles instances de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="2f5fa-118">exemple de hello toocomplete dans ce didacticiel, vous devez disposer d’un ordinateur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="2f5fa-119">Si nécessaire, cet [exemple de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) peut en créer une pour vous.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="2f5fa-120">Lorsque le travail didacticiel de hello, remplacez machine virtuelle et groupe de ressources hello noms lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="2f5fa-121">Préparer la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="2f5fa-121">Prepare VM</span></span>

<span data-ttu-id="2f5fa-122">toocreate une image d’un ordinateur virtuel, vous devez tooprepare hello VM par hello généraliser machine virtuelle, désallocation et puis marque la source de hello machine virtuelle comme généralisé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-122">toocreate an image of a virtual machine, you need tooprepare hello VM by generalizing hello VM, deallocating, and then marking hello source VM as generalized in Azure.</span></span>

### <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="2f5fa-123">Généraliser hello virtuelle Windows à l’aide de Sysprep</span><span class="sxs-lookup"><span data-stu-id="2f5fa-123">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="2f5fa-124">Sysprep supprime toutes vos informations de compte personnel, entre autres choses et prépare hello machine toobe est utilisé en tant qu’image.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-124">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="2f5fa-125">Pour plus d’informations sur Sysprep, consultez [comment tooUse Sysprep : Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="2f5fa-125">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="2f5fa-126">Connecter l’ordinateur virtuel de toohello.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-126">Connect toohello virtual machine.</span></span>
2. <span data-ttu-id="2f5fa-127">Ouvrez la fenêtre d’invite de commandes hello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-127">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="2f5fa-128">Basculez hello trop*%windir%\system32\sysprep*, puis exécutez *sysprep.exe*.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-128">Change hello directory too*%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="2f5fa-129">Bonjour **outil de préparation système** boîte de dialogue, sélectionnez *entrer le système Out-of-Box Experience (OOBE)*et assurez-vous que hello *Generalize* case à cocher est activée.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-129">In hello **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that hello *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="2f5fa-130">Dans **Options d’arrêt**, sélectionnez *Arrêter*, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="2f5fa-131">Quand Sysprep se termine, il arrête de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-131">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="2f5fa-132">**Ne redémarrez pas hello VM**.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-132">**Do not restart hello VM**.</span></span>

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="2f5fa-133">Désallouer et marquer hello machine virtuelle comme généralisé</span><span class="sxs-lookup"><span data-stu-id="2f5fa-133">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="2f5fa-134">toocreate une image, hello machine virtuelle doit toobe désalloué et marquée comme généralisé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-134">toocreate an image, hello VM needs toobe deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="2f5fa-135">À l’aide de machine virtuelle libérée hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="2f5fa-135">Deallocated hello VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="2f5fa-136">Définir le statut de hello de machine virtuelle de hello trop`-Generalized` à l’aide de [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="2f5fa-136">Set hello status of hello virtual machine too`-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a><span data-ttu-id="2f5fa-137">Création d’image de hello</span><span class="sxs-lookup"><span data-stu-id="2f5fa-137">Create hello image</span></span>

<span data-ttu-id="2f5fa-138">Vous pouvez désormais créer une image de machine virtuelle de hello à l’aide de [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) et [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span><span class="sxs-lookup"><span data-stu-id="2f5fa-138">Now you can create an image of hello VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="2f5fa-139">Hello exemple suivant crée une image nommée *myImage* à partir d’un ordinateur virtuel nommé *myVM*.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-139">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="2f5fa-140">Obtenir un ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-140">Get hello virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="2f5fa-141">Créer la configuration de l’image hello.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-141">Create hello image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="2f5fa-142">Créer l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-142">Create hello image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="2f5fa-143">Créer des ordinateurs virtuels à partir de l’image de hello</span><span class="sxs-lookup"><span data-stu-id="2f5fa-143">Create VMs from hello image</span></span>

<span data-ttu-id="2f5fa-144">Maintenant que vous disposez d’une image, vous pouvez créer un ou plusieurs nouveaux ordinateurs virtuels à partir de l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-144">Now that you have an image, you can create one or more new VMs from hello image.</span></span> <span data-ttu-id="2f5fa-145">Création d’une machine virtuelle à partir d’une image personnalisée est très similaire toocreating une machine virtuelle à l’aide d’une image de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-145">Creating a VM from a custom image is very similar toocreating a VM using a Marketplace image.</span></span> <span data-ttu-id="2f5fa-146">Lorsque vous utilisez une image de Marketplace, vous avez tooinformation sur les images de hello, fournisseur d’images, offre, référence (SKU) et version.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-146">When you use a Marketplace image, you have tooinformation about hello image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="2f5fa-147">Avec une image personnalisée, vous devez simplement des ID de hello tooprovide de ressource d’image personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-147">With a custom image, you just need tooprovide hello ID of hello custom image resource.</span></span> 

<span data-ttu-id="2f5fa-148">Dans hello le script suivant, nous créons une variable *$image* toostore plus d’informations sur l’utilisation d’une image personnalisée hello [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) puis nous les utilisons [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)et spécifiez l’ID de hello à l’aide de hello *$image* variable nous venons de créer.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-148">In hello following script, we create a variable *$image* toostore information about hello custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify hello ID using hello *$image* variable we just created.</span></span> 

<span data-ttu-id="2f5fa-149">script de Hello crée un ordinateur virtuel nommé *myVMfromImage* à partir de notre image personnalisée dans un groupe de ressources nommé *myResourceGroupFromImage* Bonjour *ouest des États-Unis* emplacement.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-149">hello script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in hello *West US* location.</span></span>


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

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

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a><span data-ttu-id="2f5fa-150">Gestion d’image</span><span class="sxs-lookup"><span data-stu-id="2f5fa-150">Image management</span></span> 

<span data-ttu-id="2f5fa-151">Voici quelques exemples de tâches courantes de gestion image et comment toocomplete les à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-151">Here are some examples of common management image tasks and how toocomplete them using PowerShell.</span></span>

<span data-ttu-id="2f5fa-152">Répertoriez toutes les images par nom.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="2f5fa-153">Supprimez une image.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-153">Delete an image.</span></span> <span data-ttu-id="2f5fa-154">Cet exemple supprime hello image nommée *myOldImage* de hello *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-154">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="2f5fa-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2f5fa-155">Next steps</span></span>

<span data-ttu-id="2f5fa-156">Ce didacticiel vous montré comment créer une image de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="2f5fa-157">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f5fa-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2f5fa-158">Exécuter Sysprep et généraliser les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="2f5fa-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="2f5fa-159">Créer une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="2f5fa-159">Create a custom image</span></span>
> * <span data-ttu-id="2f5fa-160">Créer une machine virtuelle à partir d’une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="2f5fa-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="2f5fa-161">La liste de toutes les images hello dans votre abonnement</span><span class="sxs-lookup"><span data-stu-id="2f5fa-161">List all hello images in your subscription</span></span>
> * <span data-ttu-id="2f5fa-162">Supprimer une image</span><span class="sxs-lookup"><span data-stu-id="2f5fa-162">Delete an image</span></span>

<span data-ttu-id="2f5fa-163">Avance toohello toolearn de didacticiel suivant sur les ordinateurs virtuels comment hautement disponibles.</span><span class="sxs-lookup"><span data-stu-id="2f5fa-163">Advance toohello next tutorial toolearn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2f5fa-164">Créer des machines virtuelles hautement disponibles</span><span class="sxs-lookup"><span data-stu-id="2f5fa-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)



