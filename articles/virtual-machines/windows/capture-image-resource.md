---
title: "aaaCreate une image managée dans Azure | Documents Microsoft"
description: "Créer une image managée d’une machine virtuelle ou d’un disque dur virtuel généralisé(e) dans Azure. Les images peut être utilisé toocreate plusieurs machines virtuelles qui utilisent des disques gérés."
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
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="c1810-104">Créer une image managée d’une machine virtuelle généralisée dans Azure</span><span class="sxs-lookup"><span data-stu-id="c1810-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="c1810-105">Une ressource d’image managée peut être créée à partir d’une machine virtuelle généralisée stockée comme un disque géré ou non géré dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c1810-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="c1810-106">Hello image peut ensuite être utilisé toocreate plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="c1810-106">hello image can then be used toocreate multiple VMs.</span></span> 


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="c1810-107">Généraliser hello virtuelle Windows à l’aide de Sysprep</span><span class="sxs-lookup"><span data-stu-id="c1810-107">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="c1810-108">Sysprep supprime toutes vos informations de compte personnel, entre autres choses et prépare hello machine toobe est utilisé en tant qu’image.</span><span class="sxs-lookup"><span data-stu-id="c1810-108">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="c1810-109">Pour plus d’informations sur Sysprep, consultez [comment tooUse Sysprep : Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1810-109">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="c1810-110">Assurez-vous que les rôles de serveur hello en cours d’exécution sur l’ordinateur de hello sont pris en charge par Sysprep.</span><span class="sxs-lookup"><span data-stu-id="c1810-110">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="c1810-111">Pour plus d’informations, consultez [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="c1810-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c1810-112">Si vous exécutez Sysprep avant de télécharger votre tooAzure de disque dur virtuel pour hello première fois, vérifiez que vous disposez [préparé votre machine virtuelle](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avant d’exécuter Sysprep.</span><span class="sxs-lookup"><span data-stu-id="c1810-112">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="c1810-113">Se connecter toohello machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="c1810-113">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="c1810-114">Ouvrez la fenêtre d’invite de commandes hello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c1810-114">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="c1810-115">Basculez hello trop**%windir%\system32\sysprep**, puis exécutez `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="c1810-115">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="c1810-116">Bonjour **outil de préparation système** boîte de dialogue, sélectionnez **entrer le système Out-of-Box Experience (OOBE)**et assurez-vous que hello **Generalize** case à cocher est activée.</span><span class="sxs-lookup"><span data-stu-id="c1810-116">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="c1810-117">Dans **Options d’arrêt**, sélectionnez **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="c1810-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="c1810-118">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c1810-118">Click **OK**.</span></span>
   
    ![Démarrer Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="c1810-120">Quand Sysprep se termine, il arrête de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="c1810-120">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="c1810-121">Ne redémarrez pas hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c1810-121">Do not restart hello VM.</span></span>


## <a name="create-a-managed-image-in-hello-portal"></a><span data-ttu-id="c1810-122">Créer une image managée dans le portail de hello</span><span class="sxs-lookup"><span data-stu-id="c1810-122">Create a managed image in hello portal</span></span> 

1. <span data-ttu-id="c1810-123">Ouvrez hello [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c1810-123">Open hello [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c1810-124">Cliquez sur hello signe toocreate une nouvelle ressource.</span><span class="sxs-lookup"><span data-stu-id="c1810-124">Click hello plus sign toocreate a new resource.</span></span>
3. <span data-ttu-id="c1810-125">Dans la recherche de filtre hello, tapez **Image**.</span><span class="sxs-lookup"><span data-stu-id="c1810-125">In hello filter search, type **Image**.</span></span>
4. <span data-ttu-id="c1810-126">Sélectionnez **Image** à partir des résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="c1810-126">Select **Image** from hello results.</span></span>
5. <span data-ttu-id="c1810-127">Bonjour **Image** panneau, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="c1810-127">In hello **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="c1810-128">Dans **nom**, tapez un nom pour l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="c1810-128">In **Name**, type a name for hello image.</span></span>
7. <span data-ttu-id="c1810-129">Si vous avez plusieurs abonnements, sélectionnez hello un correct à partir de hello **abonnement** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="c1810-129">If you have more than one subscription, select hello correct one from hello **Subscription** drop-down.</span></span>
7. <span data-ttu-id="c1810-130">Dans **groupe de ressources** sélectionnez **nouvel** et tapez un nom ou sélectionnez **partir d’un** et sélectionnez un toouse de groupe de ressources à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="c1810-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group toouse from hello drop-down list.</span></span>
8. <span data-ttu-id="c1810-131">Dans **emplacement**, choisissez l’emplacement hello de votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c1810-131">In **Location**, choose hello location of your resource group.</span></span>
9. <span data-ttu-id="c1810-132">Dans **type de système d’exploitation** sélectionner type hello du système d’exploitation, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="c1810-132">In **OS type** select hello type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="c1810-133">Dans **objet blob de stockage**, cliquez sur **Parcourir** toolook pour hello disque dur virtuel dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c1810-133">In **Storage blob**, click **Browse** toolook for hello VHD in your Azure storage.</span></span>
12. <span data-ttu-id="c1810-134">Dans **Type de compte**, choisissez Standard_LRS ou Premium_LRS.</span><span class="sxs-lookup"><span data-stu-id="c1810-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="c1810-135">Le type Standard utilise des disques durs et Premium, des disques SSD.</span><span class="sxs-lookup"><span data-stu-id="c1810-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="c1810-136">Les deux utilisent le stockage localement redondant.</span><span class="sxs-lookup"><span data-stu-id="c1810-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="c1810-137">Dans **mise en cache disque** sélectionnez hello option mise en cache de disque approprié.</span><span class="sxs-lookup"><span data-stu-id="c1810-137">In **Disk caching** select hello appropriate disk caching option.</span></span> <span data-ttu-id="c1810-138">options de Hello sont **aucun**, **en lecture seule** et **en lecture-écriture**.</span><span class="sxs-lookup"><span data-stu-id="c1810-138">hello options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="c1810-139">Facultatif : Vous pouvez également ajouter une image de toohello de disque de données existante en cliquant sur **+ disque de données ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c1810-139">Optional: You can also add an existing data disk toohello image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="c1810-140">Une fois les sélections terminées, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="c1810-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="c1810-141">Après la création d’image de hello, vous verrez comme un **Image** ressource dans la liste hello de ressources dans le groupe de ressources hello choisis.</span><span class="sxs-lookup"><span data-stu-id="c1810-141">After hello image is created, you will see it as an **Image** resource in hello list of resources in hello resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="c1810-142">Créer une image managée d’une machine virtuelle à l’aide de Powershell</span><span class="sxs-lookup"><span data-stu-id="c1810-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="c1810-143">Création d’une image directement à partir de hello que VM garantit cette image hello inclut tous les disques hello associés hello machine virtuelle, y compris hello disque de système d’exploitation et les disques de données.</span><span class="sxs-lookup"><span data-stu-id="c1810-143">Creating an image directly from hello VM ensures that hello image includes all of hello disks associated with hello VM, including hello OS Disk and any data disks.</span></span>


<span data-ttu-id="c1810-144">Avant de commencer, assurez-vous d’avoir hello dernière version du module PowerShell de AzureRM.Compute de hello.</span><span class="sxs-lookup"><span data-stu-id="c1810-144">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="c1810-145">Exécutez hello après la commande tooinstall il.</span><span class="sxs-lookup"><span data-stu-id="c1810-145">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="c1810-146">Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c1810-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="c1810-147">Définissez des variables.</span><span class="sxs-lookup"><span data-stu-id="c1810-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="c1810-148">Vérifiez que hello que machine virtuelle a été libérée.</span><span class="sxs-lookup"><span data-stu-id="c1810-148">Make sure hello VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="c1810-149">Définir le statut de hello de machine virtuelle de hello trop**généralisé**.</span><span class="sxs-lookup"><span data-stu-id="c1810-149">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="c1810-150">Obtenir un ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="c1810-150">Get hello virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="c1810-151">Créer la configuration de l’image hello.</span><span class="sxs-lookup"><span data-stu-id="c1810-151">Create hello image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="c1810-152">Créer l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="c1810-152">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="c1810-153">Créer une image managée d’un disque dur virtuel à l’aide de Powershell</span><span class="sxs-lookup"><span data-stu-id="c1810-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="c1810-154">Créez une image managée à l’aide de votre disque dur virtuel généralisé de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="c1810-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="c1810-155">Tout d’abord, définissez les paramètres communs hello :</span><span class="sxs-lookup"><span data-stu-id="c1810-155">First, set hello common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="c1810-156">Hello Step\deallocate machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c1810-156">Step\deallocate hello VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="c1810-157">Marquer hello machine virtuelle comme généralisé.</span><span class="sxs-lookup"><span data-stu-id="c1810-157">Mark hello VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="c1810-158">Créer l’image de hello à l’aide de votre disque dur virtuel du système d’exploitation généralisé.</span><span class="sxs-lookup"><span data-stu-id="c1810-158">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="c1810-159">Créer une image managée à partir d’une capture instantanée à l’aide de Powershell</span><span class="sxs-lookup"><span data-stu-id="c1810-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="c1810-160">Vous pouvez également créer une image managée à partir d’un instantané de disque dur virtuel à partir d’une machine virtuelle généralisée de hello.</span><span class="sxs-lookup"><span data-stu-id="c1810-160">You can also create a managed image from a snapshot of hello VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="c1810-161">Définissez des variables.</span><span class="sxs-lookup"><span data-stu-id="c1810-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="c1810-162">Obtenir un instantané de hello.</span><span class="sxs-lookup"><span data-stu-id="c1810-162">Get hello snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="c1810-163">Créer la configuration de l’image hello.</span><span class="sxs-lookup"><span data-stu-id="c1810-163">Create hello image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="c1810-164">Créer l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="c1810-164">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="c1810-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c1810-165">Next steps</span></span>
- <span data-ttu-id="c1810-166">Vous pouvez à présent [créer une machine virtuelle à partir de l’image managée de hello généralisé](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c1810-166">Now you can [create a VM from hello generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>    

