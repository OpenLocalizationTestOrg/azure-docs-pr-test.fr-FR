---
title: "Créer une image managée dans Azure | Microsoft Docs"
description: "Créer une image managée d’une machine virtuelle ou d’un disque dur virtuel généralisé(e) dans Azure. Les images peuvent être utilisées pour créer différentes machines virtuelles utilisant des disques gérés."
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
ms.openlocfilehash: f64b81489ab426b50ec89af369e1581ac71848be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="f72e1-104">Créer une image managée d’une machine virtuelle généralisée dans Azure</span><span class="sxs-lookup"><span data-stu-id="f72e1-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="f72e1-105">Une ressource d’image managée peut être créée à partir d’une machine virtuelle généralisée stockée comme un disque géré ou non géré dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f72e1-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="f72e1-106">L’image peut ensuite être utilisée pour créer plusieurs machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="f72e1-106">The image can then be used to create multiple VMs.</span></span> 


## <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="f72e1-107">Généraliser la machine virtuelle Windows à l’aide de Sysprep</span><span class="sxs-lookup"><span data-stu-id="f72e1-107">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="f72e1-108">Sysprep supprime toutes les informations personnelles de votre compte, entre autres, et prépare la machine de façon à pouvoir l’utiliser comme image.</span><span class="sxs-lookup"><span data-stu-id="f72e1-108">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="f72e1-109">Pour plus d’informations sur Sysprep, voir [Introduction à l’utilisation de Sysprep](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="f72e1-109">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="f72e1-110">Vérifiez que les rôles serveur exécutés sur la machine sont pris en charge par Sysprep.</span><span class="sxs-lookup"><span data-stu-id="f72e1-110">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="f72e1-111">Pour plus d’informations, consultez [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="f72e1-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f72e1-112">Si vous exécutez Sysprep avant de charger votre disque dur virtuel vers Azure pour la première fois, vérifiez que vous avez [préparé votre machine virtuelle](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avant d’exécuter Sysprep.</span><span class="sxs-lookup"><span data-stu-id="f72e1-112">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="f72e1-113">Connectez-vous à la machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="f72e1-113">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="f72e1-114">Ouvrez la fenêtre d’invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f72e1-114">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="f72e1-115">Remplacez le répertoire par **%windir%\system32\sysprep**, puis exécutez `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="f72e1-115">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="f72e1-116">Dans la boîte de dialogue **Outil de préparation du système**, sélectionnez **Entrer en mode OOBE (Out-of-Box Experience)** et vérifiez que la case **Généraliser** est cochée.</span><span class="sxs-lookup"><span data-stu-id="f72e1-116">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="f72e1-117">Dans **Options d’arrêt**, sélectionnez **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="f72e1-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="f72e1-118">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f72e1-118">Click **OK**.</span></span>
   
    ![Démarrer Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="f72e1-120">Une fois l’opération Sysprep terminée, elle arrête la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f72e1-120">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="f72e1-121">Ne redémarrez pas la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f72e1-121">Do not restart the VM.</span></span>


## <a name="create-a-managed-image-in-the-portal"></a><span data-ttu-id="f72e1-122">Créer une image managée dans le portail</span><span class="sxs-lookup"><span data-stu-id="f72e1-122">Create a managed image in the portal</span></span> 

1. <span data-ttu-id="f72e1-123">Ouvrez le [portail](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f72e1-123">Open the [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f72e1-124">Cliquez sur le signe (+) pour créer une ressource.</span><span class="sxs-lookup"><span data-stu-id="f72e1-124">Click the plus sign to create a new resource.</span></span>
3. <span data-ttu-id="f72e1-125">Dans le filtre de recherche, tapez **Image**.</span><span class="sxs-lookup"><span data-stu-id="f72e1-125">In the filter search, type **Image**.</span></span>
4. <span data-ttu-id="f72e1-126">Sélectionnez **Image** dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="f72e1-126">Select **Image** from the results.</span></span>
5. <span data-ttu-id="f72e1-127">Dans le panneau **Image**, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f72e1-127">In the **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="f72e1-128">Dans **Nom**, entrez le nom de l’image.</span><span class="sxs-lookup"><span data-stu-id="f72e1-128">In **Name**, type a name for the image.</span></span>
7. <span data-ttu-id="f72e1-129">Si vous avez plusieurs abonnements, sélectionnez le bon dans la liste déroulante **Abonnement**.</span><span class="sxs-lookup"><span data-stu-id="f72e1-129">If you have more than one subscription, select the correct one from the **Subscription** drop-down.</span></span>
7. <span data-ttu-id="f72e1-130">Dans **Groupe de ressources**, sélectionnez **Créer** et tapez un nom, ou sélectionnez **À partir d’un groupe existant** et choisissez un groupe de ressources à utiliser dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="f72e1-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group to use from the drop-down list.</span></span>
8. <span data-ttu-id="f72e1-131">Dans **Emplacement**, choisissez l’emplacement de votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f72e1-131">In **Location**, choose the location of your resource group.</span></span>
9. <span data-ttu-id="f72e1-132">Dans **Type de système d’exploitation**, sélectionnez le type de système d’exploitation, soit Windows, soit Linux.</span><span class="sxs-lookup"><span data-stu-id="f72e1-132">In **OS type** select the type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="f72e1-133">Dans **Stockage Blob**, cliquez sur **Parcourir** pour rechercher le disque dur virtuel dans votre stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="f72e1-133">In **Storage blob**, click **Browse** to look for the VHD in your Azure storage.</span></span>
12. <span data-ttu-id="f72e1-134">Dans **Type de compte**, choisissez Standard_LRS ou Premium_LRS.</span><span class="sxs-lookup"><span data-stu-id="f72e1-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="f72e1-135">Le type Standard utilise des disques durs et Premium, des disques SSD.</span><span class="sxs-lookup"><span data-stu-id="f72e1-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="f72e1-136">Les deux utilisent le stockage localement redondant.</span><span class="sxs-lookup"><span data-stu-id="f72e1-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="f72e1-137">Dans **Mise en cache du disque**, sélectionnez l’option de mise en cache de disque appropriée.</span><span class="sxs-lookup"><span data-stu-id="f72e1-137">In **Disk caching** select the appropriate disk caching option.</span></span> <span data-ttu-id="f72e1-138">Options possibles : **Aucune**, **Lecture seule** et **Lecture/écriture**.</span><span class="sxs-lookup"><span data-stu-id="f72e1-138">The options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="f72e1-139">Facultatif : vous pouvez également ajouter un disque de données existant à l’image en cliquant sur **+ Ajouter des données**.</span><span class="sxs-lookup"><span data-stu-id="f72e1-139">Optional: You can also add an existing data disk to the image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="f72e1-140">Une fois les sélections terminées, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f72e1-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="f72e1-141">Une fois que l’image est créée, elle s’affiche en tant que ressource **Image** dans la liste des ressources du groupe de ressources que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="f72e1-141">After the image is created, you will see it as an **Image** resource in the list of resources in the resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="f72e1-142">Créer une image managée d’une machine virtuelle à l’aide de Powershell</span><span class="sxs-lookup"><span data-stu-id="f72e1-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="f72e1-143">La création d’une image directement à partir de la machine virtuelle permet de s’assurer qu’elle comprend tous les disques associés à la machine virtuelle, y compris le disque du système d’exploitation et tous les disques de données.</span><span class="sxs-lookup"><span data-stu-id="f72e1-143">Creating an image directly from the VM ensures that the image includes all of the disks associated with the VM, including the OS Disk and any data disks.</span></span>


<span data-ttu-id="f72e1-144">Avant de commencer, assurez-vous que vous disposez de la dernière version du module PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="f72e1-144">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="f72e1-145">Exécutez la commande suivante pour l’installer.</span><span class="sxs-lookup"><span data-stu-id="f72e1-145">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="f72e1-146">Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f72e1-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="f72e1-147">Définissez des variables.</span><span class="sxs-lookup"><span data-stu-id="f72e1-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="f72e1-148">Assurez-vous que la machine virtuelle a été libérée.</span><span class="sxs-lookup"><span data-stu-id="f72e1-148">Make sure the VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="f72e1-149">Définissez l’état de la machine virtuelle sur **Généralisé**.</span><span class="sxs-lookup"><span data-stu-id="f72e1-149">Set the status of the virtual machine to **Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="f72e1-150">Accédez à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f72e1-150">Get the virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="f72e1-151">Créez la configuration de l’image.</span><span class="sxs-lookup"><span data-stu-id="f72e1-151">Create the image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="f72e1-152">Créez l’image.</span><span class="sxs-lookup"><span data-stu-id="f72e1-152">Create the image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="f72e1-153">Créer une image managée d’un disque dur virtuel à l’aide de Powershell</span><span class="sxs-lookup"><span data-stu-id="f72e1-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="f72e1-154">Créez une image managée à l’aide de votre disque dur virtuel généralisé de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="f72e1-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="f72e1-155">Tout d’abord, définissez les paramètres communs :</span><span class="sxs-lookup"><span data-stu-id="f72e1-155">First, set the common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="f72e1-156">Arrêtez/libérez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f72e1-156">Step\deallocate the VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="f72e1-157">Indiquez que la machine virtuelle est généralisée.</span><span class="sxs-lookup"><span data-stu-id="f72e1-157">Mark the VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="f72e1-158">Créez l’image à l’aide de votre disque dur virtuel généralisé de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="f72e1-158">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="f72e1-159">Créer une image managée à partir d’une capture instantanée à l’aide de Powershell</span><span class="sxs-lookup"><span data-stu-id="f72e1-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="f72e1-160">Vous pouvez également créer une image managée à partir d’une capture instantanée du VHD d’une machine virtuelle généralisée.</span><span class="sxs-lookup"><span data-stu-id="f72e1-160">You can also create a managed image from a snapshot of the VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="f72e1-161">Définissez des variables.</span><span class="sxs-lookup"><span data-stu-id="f72e1-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="f72e1-162">Accédez à la capture instantanée.</span><span class="sxs-lookup"><span data-stu-id="f72e1-162">Get the snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="f72e1-163">Créez la configuration de l’image.</span><span class="sxs-lookup"><span data-stu-id="f72e1-163">Create the image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="f72e1-164">Créez l’image.</span><span class="sxs-lookup"><span data-stu-id="f72e1-164">Create the image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="f72e1-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f72e1-165">Next steps</span></span>
- <span data-ttu-id="f72e1-166">Vous pouvez à présent [créer une machine virtuelle à partir de l’image managée généralisée](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f72e1-166">Now you can [create a VM from the generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>  

