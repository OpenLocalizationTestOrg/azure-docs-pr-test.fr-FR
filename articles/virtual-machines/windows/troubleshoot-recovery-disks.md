---
title: "aaaUse une résolution des problèmes de la machine virtuelle avec Azure PowerShell Windows | Documents Microsoft"
description: "Découvrez comment tootroubleshoot machine virtuelle Windows problèmes dans Azure en vous connectant à la restauration tooa disque hello du système d’exploitation machine virtuelle à l’aide d’Azure PowerShell"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a><span data-ttu-id="b6c3a-103">Résoudre les problèmes d’une machine virtuelle Windows en attachant la restauration tooa disque hello du système d’exploitation machine virtuelle à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6c3a-103">Troubleshoot a Windows VM by attaching hello OS disk tooa recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="b6c3a-104">Si votre machine virtuelle de Windows (VM) dans Azure rencontre une erreur de démarrage ou de disque, vous devrez peut-être tooperform étapes de dépannage sur le disque dur virtuel hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="b6c3a-105">Un exemple courant est une mise à jour de l’application qui a échoué empêche hello machine virtuelle en mesure de tooboot avec succès.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-105">A common example would be a failed application update that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="b6c3a-106">Cet article détails comment toouse Azure PowerShell tooconnect votre toofix de machine virtuelle Windows tooanother disque dur virtuel toutes les erreurs, puis la recréer votre machine virtuelle d’origine.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-106">This article details how toouse Azure PowerShell tooconnect your virtual hard disk tooanother Windows VM toofix any errors, then re-create your original VM.</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="b6c3a-107">Vue d’ensemble du processus de récupération</span><span class="sxs-lookup"><span data-stu-id="b6c3a-107">Recovery process overview</span></span>
<span data-ttu-id="b6c3a-108">Hello, résolution des problèmes de processus est la suivante :</span><span class="sxs-lookup"><span data-stu-id="b6c3a-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="b6c3a-109">Supprimer hello VM fait de rencontrer des problèmes, en conservant les disques durs virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="b6c3a-110">Attacher et monter un disque dur virtuel de hello tooanother machine virtuelle Windows à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-110">Attach and mount hello virtual hard disk tooanother Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="b6c3a-111">Se connecter toohello résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="b6c3a-112">Modifier des fichiers ou d’exécuter des outils toofix problèmes sur les disque dur virtuel d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="b6c3a-113">Démontez et détacher le disque dur virtuel de hello de hello, résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="b6c3a-114">Créer une machine virtuelle à l’aide de hello d’origine disque dur.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-114">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="b6c3a-115">Assurez-vous que vous avez [hello la dernière version d’Azure PowerShell](/powershell/azure/overview) installé et enregistré dans tooyour abonnement :</span><span class="sxs-lookup"><span data-stu-id="b6c3a-115">Make sure that you have [hello latest Azure PowerShell](/powershell/azure/overview) installed and logged in tooyour subscription:</span></span>

```powershell
Login-AzureRMAccount
```

<span data-ttu-id="b6c3a-116">Bonjour les exemples suivants, remplacez les noms de paramètres par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-116">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="b6c3a-117">Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `myVM`.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="b6c3a-118">Identifier les problèmes de démarrage</span><span class="sxs-lookup"><span data-stu-id="b6c3a-118">Determine boot issues</span></span>
<span data-ttu-id="b6c3a-119">Vous pouvez afficher une capture d’écran de votre machine virtuelle dans Azure toohelp résoudre les problèmes de démarrage.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-119">You can view a screenshot of your VM in Azure toohelp troubleshoot boot issues.</span></span> <span data-ttu-id="b6c3a-120">Cette capture d’écran peut aider à identifier la cause d’une machine virtuelle échoue tooboot.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-120">This screenshot can help identify why a VM fails tooboot.</span></span> <span data-ttu-id="b6c3a-121">Hello exemple suivant obtient hello capture d’écran de hello VM Windows nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b6c3a-121">hello following example gets hello screenshot from hello Windows VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="b6c3a-122">Passez en revue les toodetermine de capture d’écran hello pourquoi hello VM échoue tooboot.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-122">Review hello screenshot toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="b6c3a-123">Notez les messages d’erreur ou les codes d’erreur spécifiques fournis.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-123">Note any specific error messages or error codes provided.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="b6c3a-124">Afficher les détails du disque dur virtuel existant</span><span class="sxs-lookup"><span data-stu-id="b6c3a-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="b6c3a-125">Avant de pouvoir joindre votre tooanother de disque dur virtuel machine virtuelle, vous devez nom de hello tooidentify de hello les disque dur virtuel (VHD).</span><span class="sxs-lookup"><span data-stu-id="b6c3a-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span>

<span data-ttu-id="b6c3a-126">Hello exemple suivant obtient les informations pour hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b6c3a-126">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="b6c3a-127">Recherchez `Vhd URI` dans hello `StorageProfile` section à partir de la sortie de hello Hello précédant la commande.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-127">Look for `Vhd URI` within hello `StorageProfile` section from hello output of hello preceding command.</span></span> <span data-ttu-id="b6c3a-128">Hello tronquée exemple de sortie suivant affiche hello `Vhd URI` vers fin hello hello du bloc de code :</span><span class="sxs-lookup"><span data-stu-id="b6c3a-128">hello following truncated example output shows hello `Vhd URI` towards hello end of hello code block:</span></span>

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a><span data-ttu-id="b6c3a-129">Supprimer une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="b6c3a-129">Delete existing VM</span></span>
<span data-ttu-id="b6c3a-130">Les disques durs virtuels et les machines virtuelles sont deux ressources distinctes dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-130">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="b6c3a-131">Un disque dur virtuel consiste à stocker des hello système d’exploitation, des applications et des configurations.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-131">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="b6c3a-132">Hello machine virtuelle proprement dite est simplement des métadonnées qui définit la taille de hello ou l’emplacement et fait référence à des ressources, tel qu’un disque dur virtuel ou d’une carte réseau virtuelle (NIC).</span><span class="sxs-lookup"><span data-stu-id="b6c3a-132">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="b6c3a-133">Chaque disque dur virtuel a un bail attribué lorsqu’il est attaché tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-133">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="b6c3a-134">Bien que les disques de données peuvent être attachées et détachées même pendant l’exécution de la machine virtuelle de hello, les disques du système d’exploitation hello ne peut pas être détachée tant que hello ressource d’ordinateur virtuel est supprimé.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-134">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="b6c3a-135">bail de Hello continue disque hello du système d’exploitation de tooassociate avec une machine virtuelle, même lorsque l’ordinateur virtuel est dans un état arrêté et est libéré.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-135">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="b6c3a-136">Hello première étape toorecover votre machine virtuelle est la ressource d’ordinateur virtuel hello toodelete lui-même.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-136">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="b6c3a-137">Suppression hello VM laisse hello des disques durs virtuels dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-137">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="b6c3a-138">Après hello que machine virtuelle est supprimée, vous attachez hello disque dur virtuel tooanother VM tootroubleshoot et résolvez les erreurs de hello.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-138">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="b6c3a-139">Hello suivant supprime de l’exemple hello ordinateur virtuel nommé `myVM` du groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b6c3a-139">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="b6c3a-140">Attendez la fin hello VM suppression avant de joindre tooanother de disque dur virtuel hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-140">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="b6c3a-141">bail Hello sur le disque dur virtuel hello qui associe hello machine virtuelle doit toobe publié avant de pouvoir joindre tooanother de disque dur virtuel hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-141">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="b6c3a-142">Attacher tooanother de disque dur virtuel existant machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b6c3a-142">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="b6c3a-143">Pour hello en suivant quelques étapes, vous utilisez un autre ordinateur virtuel à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-143">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="b6c3a-144">Vous attachez hello toothis de disque dur virtuel existant dépannage toobrowse de machine virtuelle et que vous modifiez le contenu du disque hello.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-144">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="b6c3a-145">Ce processus vous permet de toocorrect toutes les erreurs de configuration ou examiner des applications supplémentaires ou de système de fichiers journaux, par exemple.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-145">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="b6c3a-146">Choisissez ou créez une autre machine virtuelle toouse, à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-146">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="b6c3a-147">Lorsque vous attachez le disque dur virtuel existant hello, spécifier le disque de toohello URL hello obtenu Bonjour précédent `Get-AzureRmVM` commande.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-147">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `Get-AzureRmVM` command.</span></span> <span data-ttu-id="b6c3a-148">exemple Hello attache un toohello disque dur virtuel existant, résolution des problèmes d’ordinateur virtuel nommé `myVMRecovery` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b6c3a-148">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> <span data-ttu-id="b6c3a-149">Ajout d’un disque nécessite de taille de hello toospecify du disque de hello.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-149">Adding a disk requires you toospecify hello size of hello disk.</span></span> <span data-ttu-id="b6c3a-150">Comme nous attacher un disque existant, hello `-DiskSizeInGB` est spécifié en tant que `$null`.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-150">As we attach an existing disk, hello `-DiskSizeInGB` is specified as `$null`.</span></span> <span data-ttu-id="b6c3a-151">Cette valeur permet de disque de données hello est correctement attaché, et sans hello devez toodetermine hello taille réelle du disque de données.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-151">This value ensures hello data disk is correctly attached, and without hello need toodetermine hello true size of data disk.</span></span>


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="b6c3a-152">Monter le disque de données attaché hello</span><span class="sxs-lookup"><span data-stu-id="b6c3a-152">Mount hello attached data disk</span></span>

1. <span data-ttu-id="b6c3a-153">RDP tooyour de résolution des problèmes de la machine virtuelle en utilisant les informations d’identification appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-153">RDP tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="b6c3a-154">fichier de connexion RDP hello pour hello ordinateur virtuel nommé télécharge Hello exemple suivant `myVMRecovery` dans le groupe de ressources hello nommé `myResourceGroup`et le télécharge trop`C:\Users\ops\Documents`»</span><span class="sxs-lookup"><span data-stu-id="b6c3a-154">hello following example downloads hello RDP connection file for hello VM named `myVMRecovery` in hello resource group named `myResourceGroup`, and downloads it too`C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="b6c3a-155">disque de données Hello est automatiquement détecté et attaché.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-155">hello data disk is automatically detected and attached.</span></span> <span data-ttu-id="b6c3a-156">Affichez la liste hello de lettre de lecteur de volumes attachés toodetermine hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b6c3a-156">View hello list of attached volumes toodetermine hello drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="b6c3a-157">Hello suivant l’exemple de sortie montre hello un disque dur virtuel connecté à un disque **2**.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-157">hello following example output shows hello virtual hard disk connected a disk **2**.</span></span> <span data-ttu-id="b6c3a-158">(Vous pouvez également utiliser `Get-Volume` lettre de lecteur tooview hello) :</span><span class="sxs-lookup"><span data-stu-id="b6c3a-158">(You can also use `Get-Volume` tooview hello drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="b6c3a-159">Résoudre des problèmes sur le disque dur virtuel d’origine</span><span class="sxs-lookup"><span data-stu-id="b6c3a-159">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="b6c3a-160">Avec hello disque dur virtuel existant monté, vous pouvez désormais effectuer une maintenance et dépannage en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-160">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="b6c3a-161">Une fois que vous avez corrige les problèmes de hello, poursuivez hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-161">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="b6c3a-162">Démonter et dissocier le disque dur virtuel d’origine</span><span class="sxs-lookup"><span data-stu-id="b6c3a-162">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="b6c3a-163">Une fois les erreurs résolues, vous démontez et détachez un disque dur virtuel existant hello à partir de votre machine virtuelle de résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-163">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="b6c3a-164">Vous ne pouvez pas utiliser votre disque dur virtuel avec n’importe quel autre machine virtuelle jusqu'à ce que le bail hello attachement toohello de disque dur virtuel hello résolution des problèmes de la machine virtuelle est libéré.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-164">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="b6c3a-165">À partir de votre session RDP, démontez disque de données hello sur votre ordinateur virtuel de récupération.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-165">From within your RDP session, unmount hello data disk on your recovery VM.</span></span> <span data-ttu-id="b6c3a-166">Vous devez le numéro du disque à partir de hello hello précédente `Get-Disk` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-166">You need hello disk number from hello previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="b6c3a-167">Ensuite, utilisez `Set-Disk` disque de hello tooset comme étant hors connexion :</span><span class="sxs-lookup"><span data-stu-id="b6c3a-167">Then, use `Set-Disk` tooset hello disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="b6c3a-168">Vérifiez le disque de hello est désormais défini à l’aide hors connexion `Get-Disk` à nouveau.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-168">Confirm hello disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="b6c3a-169">Hello exemple de sortie suivant affiche hello disque est désormais défini comme étant hors connexion :</span><span class="sxs-lookup"><span data-stu-id="b6c3a-169">hello following example output shows hello disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="b6c3a-170">Quittez la session Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-170">Exit your RDP session.</span></span> <span data-ttu-id="b6c3a-171">À partir de votre session Azure PowerShell, supprimez le disque dur virtuel de hello hello résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-171">From your Azure PowerShell session, remove hello virtual hard disk from hello troubleshooting VM.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="b6c3a-172">Créer une machine virtuelle à partir du disque dur d’origine</span><span class="sxs-lookup"><span data-stu-id="b6c3a-172">Create VM from original hard disk</span></span>
<span data-ttu-id="b6c3a-173">utilisation d’une machine virtuelle à partir de votre disque dur virtuel d’origine, toocreate [ce modèle Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="b6c3a-173">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="b6c3a-174">modèle JSON réel Hello est à hello lien :</span><span class="sxs-lookup"><span data-stu-id="b6c3a-174">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="b6c3a-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b6c3a-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span></span>

<span data-ttu-id="b6c3a-176">modèle de Hello déploie une machine virtuelle dans un réseau virtuel existant, à l’aide de hello URL de disque dur virtuel à partir de hello commande précédemment.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-176">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="b6c3a-177">exemple Hello déploie groupe de ressources hello modèle toohello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b6c3a-177">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

<span data-ttu-id="b6c3a-178">Hello de réponse demande modèle hello comme nom d’ordinateur virtuel, le type de système d’exploitation et taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-178">Answer hello prompts for hello template such as VM name, OS type, and VM size.</span></span> <span data-ttu-id="b6c3a-179">Hello `osDiskVhdUri` est hello même que celui précédemment utilisé lors de l’attachement toohello disque dur virtuel existant de hello, résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-179">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span>


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="b6c3a-180">Réactiver les diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="b6c3a-180">Re-enable boot diagnostics</span></span>

<span data-ttu-id="b6c3a-181">Lorsque vous créez votre machine virtuelle à partir du disque dur virtuel existant hello, les diagnostics de démarrage ne peut pas être automatiquement activés.</span><span class="sxs-lookup"><span data-stu-id="b6c3a-181">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="b6c3a-182">Hello exemple suivant permet d’extension de diagnostic hello sur hello ordinateur virtuel nommé `myVMDeployed` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b6c3a-182">hello following example enables hello diagnostic extension on hello VM named `myVMDeployed` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="b6c3a-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6c3a-183">Next steps</span></span>
<span data-ttu-id="b6c3a-184">Si vous rencontrez des problèmes de connexion tooyour machine virtuelle, consultez [tooan des connexions RDP de résoudre les problèmes Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b6c3a-184">If you are having issues connecting tooyour VM, see [Troubleshoot RDP connections tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="b6c3a-185">Pour résoudre les problèmes liés à l’accès aux applications exécutées sur votre machine virtuelle, consultez [Résoudre les problèmes de connectivité des applications sur une machine virtuelle Windows](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b6c3a-185">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="b6c3a-186">Pour plus d’informations sur l’utilisation de Resource Manager, consultez la page [Présentation d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b6c3a-186">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
