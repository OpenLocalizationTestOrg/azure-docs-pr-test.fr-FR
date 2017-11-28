---
title: "aaaCreate une image non managée d’une machine virtuelle généralisée dans Azure | Documents Microsoft"
description: "Créer une image non managé d’un toocreate toouse de machine virtuelle Windows généralisée plusieurs copies d’une machine virtuelle dans Azure."
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
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="18427-103">Comment toocreate une machine virtuelle non managée de l’image à partir d’une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="18427-103">How toocreate an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="18427-104">Cet article traite de l’utilisation de comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="18427-104">This article covers using storage accounts.</span></span> <span data-ttu-id="18427-105">Nous vous recommandons d’utiliser des disques managés et des images managées plutôt qu’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="18427-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="18427-106">Pour plus d’informations, consultez [Capturer une image managée d’une machine virtuelle généralisée dans Azure](capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="18427-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="18427-107">Cet article vous montre comment toouse Azure PowerShell toocreate une image d’une machine virtuelle Azure généralisé à l’aide d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="18427-107">This article shows you how toouse Azure PowerShell toocreate an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="18427-108">Vous pouvez ensuite utiliser hello image toocreate une autre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="18427-108">You can then use hello image toocreate another VM.</span></span> <span data-ttu-id="18427-109">image de Hello inclut le disque du système d’exploitation hello et des disques de données hello toohello joint de l’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="18427-109">hello image includes hello OS disk and hello data disks that are attached toohello virtual machine.</span></span> <span data-ttu-id="18427-110">image de Hello n’inclut pas les ressources de réseau virtuel hello, donc vous devez tooset ces ressources lorsque vous créez hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="18427-110">hello image doesn't include hello virtual network resources, so you need tooset up those resources when you create hello new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="18427-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="18427-111">Prerequisites</span></span>
<span data-ttu-id="18427-112">Vous devez toohave Azure PowerShell version 1.0.x ou version plus récente.</span><span class="sxs-lookup"><span data-stu-id="18427-112">You need toohave Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="18427-113">Si vous n’avez pas déjà installé PowerShell, lisez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour les étapes d’installation.</span><span class="sxs-lookup"><span data-stu-id="18427-113">If you haven't already installed PowerShell, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-hello-vm"></a><span data-ttu-id="18427-114">Généraliser hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="18427-114">Generalize hello VM</span></span> 
<span data-ttu-id="18427-115">Cette section vous montre comment toogeneralize votre machine virtuelle de Windows pour une utilisation en tant qu’image.</span><span class="sxs-lookup"><span data-stu-id="18427-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="18427-116">La généralisation d’un ordinateur virtuel supprime toutes vos informations de compte personnel, entre autres choses et prépare hello machine toobe est utilisé en tant qu’image.</span><span class="sxs-lookup"><span data-stu-id="18427-116">Generalizing a VM removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="18427-117">Pour plus d’informations sur Sysprep, consultez [comment tooUse Sysprep : Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="18427-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="18427-118">Assurez-vous que les rôles de serveur hello en cours d’exécution sur l’ordinateur de hello sont pris en charge par Sysprep.</span><span class="sxs-lookup"><span data-stu-id="18427-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="18427-119">Pour plus d’informations, consultez [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="18427-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18427-120">Si vous téléchargez votre tooAzure de disque dur virtuel pour hello première fois, vérifiez que vous disposez [préparé votre machine virtuelle](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avant d’exécuter Sysprep.</span><span class="sxs-lookup"><span data-stu-id="18427-120">If you are uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="18427-121">Vous pouvez généraliser également un VM Linux à l’aide de `sudo waagent -deprovision+user` , puis utilisez PowerShell toocapture hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="18427-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell toocapture hello VM.</span></span> <span data-ttu-id="18427-122">Pour plus d’informations sur l’utilisation de hello CLI toocapture une machine virtuelle, consultez [comment toogeneralize et une machine virtuelle Linux à l’aide de la capture hello CLI d’Azure ](../linux/capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="18427-122">For information about using hello CLI toocapture a VM, see [How toogeneralize and capture a Linux virtual machine using hello Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="18427-123">Se connecter toohello machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="18427-123">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="18427-124">Ouvrez la fenêtre d’invite de commandes hello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="18427-124">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="18427-125">Basculez hello trop**%windir%\system32\sysprep**, puis exécutez `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="18427-125">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="18427-126">Bonjour **outil de préparation système** boîte de dialogue, sélectionnez **entrer le système Out-of-Box Experience (OOBE)**et assurez-vous que hello **Generalize** case à cocher est activée.</span><span class="sxs-lookup"><span data-stu-id="18427-126">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="18427-127">Dans **Options d’arrêt**, sélectionnez **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="18427-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="18427-128">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="18427-128">Click **OK**.</span></span>
   
    ![Démarrer Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="18427-130">Quand Sysprep se termine, il arrête de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="18427-130">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="18427-131">Ne redémarrez pas hello machine virtuelle jusqu'à ce que vous avez terminé tooAzure de disque dur virtuel hello téléchargement ou de la création d’une image à partir de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="18427-131">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="18427-132">Si hello VM obtient accidentellement redémarré, exécutez Sysprep toogeneralize nouveau.</span><span class="sxs-lookup"><span data-stu-id="18427-132">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 

## <a name="log-in-tooazure-powershell"></a><span data-ttu-id="18427-133">Connectez-vous à tooAzure PowerShell</span><span class="sxs-lookup"><span data-stu-id="18427-133">Log in tooAzure PowerShell</span></span>
1. <span data-ttu-id="18427-134">Ouvrez Azure PowerShell et connectez-vous à tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="18427-134">Open Azure PowerShell and sign in tooyour Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="18427-135">Une fenêtre contextuelle s’ouvre pour vous tooenter vos informations d’identification de compte Azure.</span><span class="sxs-lookup"><span data-stu-id="18427-135">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
2. <span data-ttu-id="18427-136">Obtenir l’ID d’abonnement hello pour vos abonnements disponibles.</span><span class="sxs-lookup"><span data-stu-id="18427-136">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="18427-137">Définir l’abonnement approprié de hello à l’aide des ID d’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="18427-137">Set hello correct subscription using hello subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a><span data-ttu-id="18427-138">Désallouer hello machine virtuelle et de définir hello état toogeneralized</span><span class="sxs-lookup"><span data-stu-id="18427-138">Deallocate hello VM and set hello state toogeneralized</span></span>
1. <span data-ttu-id="18427-139">Libérer des ressources d’ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="18427-139">Deallocate hello VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="18427-140">Hello *état* pour hello VM Bonjour Azure portal passe de **arrêté** trop**arrêté (désallouée)**.</span><span class="sxs-lookup"><span data-stu-id="18427-140">hello *Status* for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="18427-141">Définir le statut de hello de machine virtuelle de hello trop**généralisé**.</span><span class="sxs-lookup"><span data-stu-id="18427-141">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="18427-142">Vérifier l’état de hello Hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="18427-142">Check hello status of hello VM.</span></span> <span data-ttu-id="18427-143">Hello **OSState/généralisés** section hello machine virtuelle doit avoir hello **DisplayStatus** défini trop**généralisé de machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="18427-143">hello **OSState/generalized** section for hello VM should have hello **DisplayStatus** set too**VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a><span data-ttu-id="18427-144">Création d’image de hello</span><span class="sxs-lookup"><span data-stu-id="18427-144">Create hello image</span></span>

<span data-ttu-id="18427-145">Créer une image de machine virtuelle non gérée dans le conteneur de stockage de destination hello à l’aide de cette commande.</span><span class="sxs-lookup"><span data-stu-id="18427-145">Create an unmanaged virtual machine image in hello destination storage container using this command.</span></span> <span data-ttu-id="18427-146">Hello image est créée dans hello même compte de stockage comme hello d’ordinateur virtuel d’origine.</span><span class="sxs-lookup"><span data-stu-id="18427-146">hello image is created in hello same storage account as hello original virtual machine.</span></span> <span data-ttu-id="18427-147">Hello `-Path` paramètre enregistre une copie du modèle JSON hello pour ordinateur local du tooyour machine virtuelle source hello.</span><span class="sxs-lookup"><span data-stu-id="18427-147">hello `-Path` parameter saves a copy of hello JSON template for hello source VM tooyour local computer.</span></span> <span data-ttu-id="18427-148">Hello `-DestinationContainerName` paramètre désigne hello conteneur hello que vous souhaitez que toohold vos images.</span><span class="sxs-lookup"><span data-stu-id="18427-148">hello `-DestinationContainerName` parameter is hello name of hello container that you want toohold your images.</span></span> <span data-ttu-id="18427-149">Si le conteneur de hello n’existe pas, il est créé pour vous.</span><span class="sxs-lookup"><span data-stu-id="18427-149">If hello container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="18427-150">Vous pouvez obtenir hello les URL de votre image de modèle de fichier JSON hello.</span><span class="sxs-lookup"><span data-stu-id="18427-150">You can get hello URL of your image from hello JSON file template.</span></span> <span data-ttu-id="18427-151">Accédez toohello **ressources** > **storageProfile** > **osDisk** > **image**  >  **uri** section de chemin d’accès complet de hello de votre image.</span><span class="sxs-lookup"><span data-stu-id="18427-151">Go toohello **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for hello complete path of your image.</span></span> <span data-ttu-id="18427-152">URL de Hello d’image de hello est similaire à : `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="18427-152">hello URL of hello image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="18427-153">Vous pouvez également vérifier hello URI dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="18427-153">You can also verify hello URI in hello portal.</span></span> <span data-ttu-id="18427-154">image de Hello est conteneur tooa copié nommé **système** dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="18427-154">hello image is copied tooa container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-hello-image"></a><span data-ttu-id="18427-155">Créer une machine virtuelle à partir de l’image de hello</span><span class="sxs-lookup"><span data-stu-id="18427-155">Create a VM from hello image</span></span>

<span data-ttu-id="18427-156">Vous pouvez désormais créer un ou plusieurs ordinateurs virtuels à partir de l’image de non managé hello.</span><span class="sxs-lookup"><span data-stu-id="18427-156">Now you can create one or more VMs from hello unmanaged image.</span></span>

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="18427-157">Ensemble hello URI de disque dur virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="18427-157">Set hello URI of hello VHD</span></span>

<span data-ttu-id="18427-158">Hello URI pour toouse de disque dur virtuel hello est au format de hello : https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="18427-158">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="18427-159">Dans cet exemple hello disque dur virtuel nommé **myVHD** est dans un compte de stockage hello **mystorageaccount** dans le conteneur de hello **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="18427-159">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="18427-160">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="18427-160">Create a virtual network</span></span>
<span data-ttu-id="18427-161">Créer le réseau virtuel de hello et un sous-réseau de hello [réseau virtuel](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="18427-161">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="18427-162">Créer un sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="18427-162">Create hello subnet.</span></span> <span data-ttu-id="18427-163">Hello exemple suivant crée un sous-réseau nommé **mySubnet** dans le groupe de ressources hello **myResourceGroup** avec un préfixe d’adresse de hello **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="18427-163">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="18427-164">Créer un réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="18427-164">Create hello virtual network.</span></span> <span data-ttu-id="18427-165">Hello exemple suivant crée un réseau virtuel nommé **myVnet** Bonjour **ouest des États-Unis** emplacement avec un préfixe d’adresse de hello **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="18427-165">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="18427-166">Création d'une adresse IP publique et une interface réseau</span><span class="sxs-lookup"><span data-stu-id="18427-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="18427-167">tooenable une communication avec l’ordinateur virtuel de hello dans le réseau virtuel de hello, vous devez un [adresse IP publique](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) et une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="18427-167">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="18427-168">Créez une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="18427-168">Create a public IP address.</span></span> <span data-ttu-id="18427-169">Cet exemple crée une adresse IP publique nommée **myPip**.</span><span class="sxs-lookup"><span data-stu-id="18427-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="18427-170">Créer la carte de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="18427-170">Create hello NIC.</span></span> <span data-ttu-id="18427-171">Cet exemple crée une carte réseau nommée **myNic**.</span><span class="sxs-lookup"><span data-stu-id="18427-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="18427-172">Créer une règle RDP et groupe de sécurité réseau hello</span><span class="sxs-lookup"><span data-stu-id="18427-172">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="18427-173">toolog en mesure de toobe dans tooyour machine virtuelle à l’aide du protocole RDP, vous devez toohave une règle de sécurité qui autorise l’accès RDP sur le port 3389.</span><span class="sxs-lookup"><span data-stu-id="18427-173">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="18427-174">Cet exemple crée un groupe de sécurité réseau nommé **myNsg** qui contient une règle nommée **myRdpRule** autorisant le trafic RDP sur le port 3389.</span><span class="sxs-lookup"><span data-stu-id="18427-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="18427-175">Pour plus d’informations sur les groupes de sécurité réseau, consultez [l’ouverture de ports tooa machine virtuelle dans Azure à l’aide de PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="18427-175">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="18427-176">Créez une variable pour le réseau virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="18427-176">Create a variable for hello virtual network</span></span>
<span data-ttu-id="18427-177">Créez une variable pour le réseau virtuel de hello s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="18427-177">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="18427-178">Créer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="18427-178">Create hello VM</span></span>
<span data-ttu-id="18427-179">Hello PowerShell suivant termine les configurations d’ordinateur virtuel hello et non managée image en tant que source de hello pour une nouvelle installation de hello.</span><span class="sxs-lookup"><span data-stu-id="18427-179">hello following PowerShell completes hello virtual machine configurations and uses unmanaged image as hello source for hello new installation.</span></span>

</br>

```powershell
    # Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="18427-180">Vérifiez que hello que machine virtuelle a été créée.</span><span class="sxs-lookup"><span data-stu-id="18427-180">Verify that hello VM was created</span></span>
<span data-ttu-id="18427-181">Lorsque vous avez terminé, vous devez voir hello nouvellement créé VM dans hello [portail Azure](https://portal.azure.com) sous **Parcourir** > **virtuels**, ou en utilisant hello Commandes PowerShell :</span><span class="sxs-lookup"><span data-stu-id="18427-181">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="18427-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="18427-182">Next steps</span></span>
<span data-ttu-id="18427-183">reportez-vous à votre nouvelle machine virtuelle avec Azure PowerShell, toomanage [gérer des ordinateurs virtuels à l’aide du Gestionnaire de ressources Azure et PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="18427-183">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


