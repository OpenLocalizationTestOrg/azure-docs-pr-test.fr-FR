---
title: "Utiliser une machine virtuelle de dépannage Linux avec Azure CLI 1.0 | Microsoft Docs"
description: "Découvrez comment résoudre les problèmes de machines virtuelles Linux en connectant le disque du système d’exploitation à une machine virtuelle de récupération à l’aide d’Azure CLI 1.0."
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: d817358211f123c96d899c5cff88cc47aeb5c9c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-cli-10"></a><span data-ttu-id="6c311-103">Résoudre les problèmes d’une machine virtuelle Linux en connectant le disque du système d’exploitation à une machine virtuelle de récupération à l’aide d’Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6c311-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="6c311-104">Si votre machine virtuelle Linux rencontre une erreur de démarrage ou de disque, il vous faudra éventuellement appliquer la procédure de dépannage directement sur le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="6c311-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="6c311-105">Comme exemple courant, citons une entrée non valide dans `/etc/fstab` qui empêche le bon démarrage de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6c311-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="6c311-106">Cet article vous explique comment utiliser l’interface Azure CLI 1.0 pour connecter votre disque dur virtuel à une autre machine virtuelle Linux pour corriger les éventuelles erreurs, puis pour régénérer votre machine virtuelle d’origine.</span><span class="sxs-lookup"><span data-stu-id="6c311-106">This article details how to use the Azure CLI 1.0 to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="6c311-107">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="6c311-107">CLI versions to complete the task</span></span>
<span data-ttu-id="6c311-108">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="6c311-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="6c311-109">[Azure CLI 1.0](#recovery-process-overview) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="6c311-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="6c311-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) : notre interface de ligne de commande nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6c311-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="6c311-111">Vue d’ensemble du processus de récupération</span><span class="sxs-lookup"><span data-stu-id="6c311-111">Recovery process overview</span></span>
<span data-ttu-id="6c311-112">Le processus de résolution de problème se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="6c311-112">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="6c311-113">Supprimez les machines virtuelles présentant des erreurs, en conservant les disques durs virtuels.</span><span class="sxs-lookup"><span data-stu-id="6c311-113">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="6c311-114">Fixez et montez le disque dur virtuel sur une autre machine virtuelle Linux, à des fins de résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="6c311-114">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="6c311-115">Connectez-vous à la machine virtuelle de dépannage.</span><span class="sxs-lookup"><span data-stu-id="6c311-115">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="6c311-116">Modifiez les fichiers ou exécutez des outils afin de corriger les problèmes sur le disque dur virtuel d’origine.</span><span class="sxs-lookup"><span data-stu-id="6c311-116">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="6c311-117">Démontez le disque dur virtuel d’origine et dissociez-le de la machine virtuelle de dépannage.</span><span class="sxs-lookup"><span data-stu-id="6c311-117">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="6c311-118">Créez une machine virtuelle à l’aide du disque dur virtuel d’origine.</span><span class="sxs-lookup"><span data-stu-id="6c311-118">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="6c311-119">Veillez à ce que la [dernière version d’Azure CLI 1.0](../../cli-install-nodejs.md) soit installée et connectée et assurez-vous qu’elle utilise le mode Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="6c311-119">Make sure that you have [the latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="6c311-120">Dans les exemples suivants, remplacez les noms de paramètres avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="6c311-120">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="6c311-121">Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `myVM`.</span><span class="sxs-lookup"><span data-stu-id="6c311-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="6c311-122">Identifier les problèmes de démarrage</span><span class="sxs-lookup"><span data-stu-id="6c311-122">Determine boot issues</span></span>
<span data-ttu-id="6c311-123">Examinez la sortie en série afin d’identifier la raison pour laquelle votre machine virtuelle ne démarre pas correctement.</span><span class="sxs-lookup"><span data-stu-id="6c311-123">Examine the serial output to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="6c311-124">Comme exemple courant, citons une entrée non valide dans `/etc/fstab`, ou le disque dur virtuel en cours de suppression ou de déplacement.</span><span class="sxs-lookup"><span data-stu-id="6c311-124">A common example is an invalid entry in `/etc/fstab`, or the underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="6c311-125">L’exemple suivant récupère la sortie en série de la machine virtuelle nommée `myVM` dans le groupe de ressources nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="6c311-125">The following example gets the serial output from the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="6c311-126">Examinez la sortie en série afin d’identifier la raison pour laquelle le démarrage de la machine virtuelle est mis en échec.</span><span class="sxs-lookup"><span data-stu-id="6c311-126">Review the serial output to determine why the VM is failing to boot.</span></span> <span data-ttu-id="6c311-127">Si la sortie en série ne fournit aucune indication, il vous faudra éventuellement passer en revue les fichiers journaux de `/var/log` une fois que le disque dur virtuel est connecté à une machine virtuelle de dépannage.</span><span class="sxs-lookup"><span data-stu-id="6c311-127">If the serial output isn't providing any indication, you may need to review log files in `/var/log` once you have the virtual hard disk connected to a troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="6c311-128">Afficher les détails du disque dur virtuel existant</span><span class="sxs-lookup"><span data-stu-id="6c311-128">View existing virtual hard disk details</span></span>
<span data-ttu-id="6c311-129">Avant de pouvoir associer votre disque dur virtuel à une autre machine virtuelle, vous devez identifier le nom du disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="6c311-129">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="6c311-130">L’exemple suivant récupère des informations pour la machine virtuelle nommée `myVM` dans le groupe de ressources nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="6c311-130">The following example gets information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="6c311-131">Recherchez `Vhd URI` dans la sortie de la commande précédente.</span><span class="sxs-lookup"><span data-stu-id="6c311-131">Look for `Vhd URI` in the output from the preceding command.</span></span> <span data-ttu-id="6c311-132">La sortie tronquée de l’exemple suivant représente l’élément `Vhd URI` sur la dernière ligne :</span><span class="sxs-lookup"><span data-stu-id="6c311-132">The following truncated example output shows the `Vhd URI` on the last line:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "myVM"
+ Looking up the NIC "myNic"
+ Looking up the public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a><span data-ttu-id="6c311-133">Supprimer une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="6c311-133">Delete existing VM</span></span>
<span data-ttu-id="6c311-134">Les disques durs virtuels et les machines virtuelles sont deux ressources distinctes dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6c311-134">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="6c311-135">Le disque dur virtuel est l’emplacement de stockage du système d’exploitation, des applications et des configurations.</span><span class="sxs-lookup"><span data-stu-id="6c311-135">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="6c311-136">La machine virtuelle correspond à des métadonnées définissant la taille ou l’emplacement ; elle référence des ressources comme un disque dur virtuel ou une carte d’interface réseau virtuelle (NIC).</span><span class="sxs-lookup"><span data-stu-id="6c311-136">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="6c311-137">Chaque disque dur virtuel associé à une machine virtuelle se voit attribuer un bail.</span><span class="sxs-lookup"><span data-stu-id="6c311-137">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="6c311-138">Bien que l’association et la dissociation des disques de données puisse s’effectuer pendant l’exécution de la machine virtuelle, le disque du système d’exploitation ne peut pas être dissocié, sauf si la ressource de machine virtuelle est supprimée.</span><span class="sxs-lookup"><span data-stu-id="6c311-138">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="6c311-139">Le bail continue à associer le disque du système d’exploitation à une machine virtuelle, même lorsque cette machine virtuelle se trouve dans un état d’arrêt ou de libération.</span><span class="sxs-lookup"><span data-stu-id="6c311-139">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="6c311-140">La première étape de la récupération de votre machine virtuelle consiste à supprimer la ressource de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6c311-140">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="6c311-141">En supprimant la machine virtuelle, vous ne vous séparez pas des disques durs virtuels de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6c311-141">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="6c311-142">Une fois la machine virtuelle supprimée, vous associez le disque dur virtuel à une autre machine virtuelle afin de réparer et de corriger les erreurs.</span><span class="sxs-lookup"><span data-stu-id="6c311-142">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="6c311-143">L’exemple suivant supprime la machine virtuelle nommée `myVM` du groupe de ressource nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="6c311-143">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="6c311-144">Attendez la suppression définitive de la machine virtuelle avant d’associer le disque dur virtuel à une autre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6c311-144">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="6c311-145">Le bail du disque dur virtuel, qui l’associe à la machine virtuelle, doit être libéré avant l’association du disque dur virtuel à une autre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6c311-145">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="6c311-146">Associer un disque dur virtuel existant à une autre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6c311-146">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="6c311-147">Pour les prochaines étapes, vous utilisez une autre machine virtuelle à des fins de résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="6c311-147">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="6c311-148">Vous associez le disque dur virtuel existant à cette machine virtuelle de dépannage et modifiez le contenu du disque.</span><span class="sxs-lookup"><span data-stu-id="6c311-148">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="6c311-149">Ce processus vous permet de corriger les éventuelles erreurs de configuration ou d’examiner des fichiers journaux supplémentaires de système ou d’application, par exemple.</span><span class="sxs-lookup"><span data-stu-id="6c311-149">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="6c311-150">Sélectionnez ou créez une autre machine virtuelle à des fins de résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="6c311-150">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="6c311-151">Lorsque vous associez le disque dur virtuel existant, spécifiez l’URL du disque obtenu dans la commande `azure vm show` précédente.</span><span class="sxs-lookup"><span data-stu-id="6c311-151">When you attach the existing virtual hard disk, specify the URL to the disk obtained in the preceding `azure vm show` command.</span></span> <span data-ttu-id="6c311-152">L’exemple suivant associe un disque dur virtuel existant à la machine virtuelle de dépannage nommée `myVMRecovery` dans le groupe de ressources nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="6c311-152">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="6c311-153">Monter le disque de données associé</span><span class="sxs-lookup"><span data-stu-id="6c311-153">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="6c311-154">Les exemples suivants décrivent les étapes requises sur une machine virtuelle Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="6c311-154">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="6c311-155">Si vous utilisez une distribution Linux différente, comme Red Hat Enterprise Linux ou SUSE, les emplacements de fichiers journaux et les commandes `mount` peuvent varier.</span><span class="sxs-lookup"><span data-stu-id="6c311-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="6c311-156">Pour connaître les modifications appropriées dans les commandes, reportez-vous à la documentation de votre distribution spécifique.</span><span class="sxs-lookup"><span data-stu-id="6c311-156">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="6c311-157">Exécutez une commande SSH sur votre machine virtuelle de dépannage à l’aide des informations d’identification appropriées.</span><span class="sxs-lookup"><span data-stu-id="6c311-157">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="6c311-158">Si ce disque est le premier disque de données associé à votre machine virtuelle de dépannage, il est probablement connecté à `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="6c311-158">If this disk is the first data disk attached to your troubleshooting VM, the disk is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="6c311-159">Pour afficher les disques associés, utilisez `dmseg` :</span><span class="sxs-lookup"><span data-stu-id="6c311-159">Use `dmseg` to view attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="6c311-160">Le résultat ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6c311-160">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="6c311-161">Dans l’exemple précédent, le disque du système d’exploitation se trouve au niveau de `/dev/sda`, et le disque temporaire fourni pour chaque machine virtuelle se trouve au niveau de `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="6c311-161">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="6c311-162">Si vous possédiez plusieurs disques de données, ils doivent se trouver au niveau de `/dev/sdd`, `/dev/sde`, etc.</span><span class="sxs-lookup"><span data-stu-id="6c311-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="6c311-163">Créez un répertoire pour monter votre disque dur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="6c311-163">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="6c311-164">L’exemple suivant crée un répertoire nommé `troubleshootingdisk` :</span><span class="sxs-lookup"><span data-stu-id="6c311-164">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="6c311-165">Si votre disque dur virtuel existant présente plusieurs partitions, montez la partition requise.</span><span class="sxs-lookup"><span data-stu-id="6c311-165">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="6c311-166">L’exemple suivant monte la première partition primaire au niveau de `/dev/sdc1` :</span><span class="sxs-lookup"><span data-stu-id="6c311-166">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="6c311-167">Nous vous recommandons de monter les disques de données sur les machines virtuelles à l’aide de l’identifiant unique universel (UUID) du disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="6c311-167">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="6c311-168">Pour ce scénario court de résolution des problèmes, il n’est pas nécessaire de monter le disque dur virtuel à l’aide de l’UUID.</span><span class="sxs-lookup"><span data-stu-id="6c311-168">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="6c311-169">Toutefois, dans des conditions normales, la modification de `/etc/fstab` pour monter les disques durs virtuels avec le nom d’appareil en lieu et place de l’UUID peut entraîner la mise en échec du démarrage de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6c311-169">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="6c311-170">Résoudre des problèmes sur le disque dur virtuel d’origine</span><span class="sxs-lookup"><span data-stu-id="6c311-170">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="6c311-171">Avec le disque dur virtuel existant monté, vous pouvez désormais exécuter les procédures de maintenance et de dépannage requises.</span><span class="sxs-lookup"><span data-stu-id="6c311-171">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="6c311-172">Une fois que vous avez résolu les problèmes, passez aux étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="6c311-172">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="6c311-173">Démonter et dissocier le disque dur virtuel d’origine</span><span class="sxs-lookup"><span data-stu-id="6c311-173">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="6c311-174">Une fois les erreurs résolues, vous démontez et dissociez le disque dur virtuel existant de votre machine virtuelle de dépannage.</span><span class="sxs-lookup"><span data-stu-id="6c311-174">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="6c311-175">Vous ne pouvez pas utiliser votre disque dur virtuel avec une autre machine virtuelle avant la publication du bail associant le disque dur virtuel à la machine virtuelle de dépannage.</span><span class="sxs-lookup"><span data-stu-id="6c311-175">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="6c311-176">À partir de la session SSH vers votre machine virtuelle de dépannage, démontez le disque dur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="6c311-176">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="6c311-177">Commencez par modifier votre point de montage dans le répertoire parent :</span><span class="sxs-lookup"><span data-stu-id="6c311-177">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="6c311-178">Montez alors le disque dur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="6c311-178">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="6c311-179">L’exemple suivant démonte l’appareil au niveau de `/dev/sdc1` :</span><span class="sxs-lookup"><span data-stu-id="6c311-179">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="6c311-180">Dissociez le disque dur virtuel de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6c311-180">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="6c311-181">Quittez la session SSH vers votre machine virtuelle de dépannage.</span><span class="sxs-lookup"><span data-stu-id="6c311-181">Exit the SSH session to your troubleshooting VM.</span></span> <span data-ttu-id="6c311-182">Dans l’interface de ligne de commande Azure, commencez par répertorier les disques de données associés à votre machine virtuelle de dépannage.</span><span class="sxs-lookup"><span data-stu-id="6c311-182">In the Azure CLI, first list the attached data disks to your troubleshooting VM.</span></span> <span data-ttu-id="6c311-183">L’exemple suivant répertorie les disques de données associés à la machine virtuelle nommée `myVMRecovery` dans le groupe de ressources nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="6c311-183">The following example lists the data disks attached to the VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    <span data-ttu-id="6c311-184">Notez la valeur `Lun` associée à votre disque dur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="6c311-184">Note the `Lun` value for your existing virtual hard disk.</span></span> <span data-ttu-id="6c311-185">L’exemple de sortie de commande suivant représente le disque virtuel existant associé au niveau LUN 0 :</span><span class="sxs-lookup"><span data-stu-id="6c311-185">The following example command output shows the existing virtual disk attached at LUN 0:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Looking up the VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    <span data-ttu-id="6c311-186">Dissociez le disque de données de la machine virtuelle à l’aide de la valeur `Lun` applicable :</span><span class="sxs-lookup"><span data-stu-id="6c311-186">Detach the data disk from your VM using the applicable `Lun` value:</span></span>

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="6c311-187">Créer une machine virtuelle à partir du disque dur d’origine</span><span class="sxs-lookup"><span data-stu-id="6c311-187">Create VM from original hard disk</span></span>
<span data-ttu-id="6c311-188">Pour créer une machine virtuelle à partir de votre disque dur d’origine, utilisez [ce modèle Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="6c311-188">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="6c311-189">Le véritable modèle JSON se trouve sur le lien suivant :</span><span class="sxs-lookup"><span data-stu-id="6c311-189">The actual JSON template is at the following link:</span></span>

- <span data-ttu-id="6c311-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="6c311-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="6c311-191">Le modèle déploie une machine virtuelle dans un réseau virtuel existant, à l’aide de l’URL de disque dur virtuel de la commande précédente.</span><span class="sxs-lookup"><span data-stu-id="6c311-191">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="6c311-192">L’exemple suivant déploie le modèle du groupe de ressources nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="6c311-192">The following example deploys the template to the resource group named `myResourceGroup`:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

<span data-ttu-id="6c311-193">Répondez aux invites pour le modèle, relatives notamment au nom de machine virtuelle (`myDeployedVM` l’exemple suivant), au type de système d’exploitation (`Linux`) et à la taille de machine virtuelle (`Standard_DS1_v2`).</span><span class="sxs-lookup"><span data-stu-id="6c311-193">Answer the prompts for the template such as VM name (`myDeployedVM` the following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span></span> <span data-ttu-id="6c311-194">L’élément `osDiskVhdUri` est celui utilisé lors de l’association du disque dur virtuel existant à la machine virtuelle de dépannage.</span><span class="sxs-lookup"><span data-stu-id="6c311-194">The `osDiskVhdUri` is the same as previously used when attaching the existing virtual hard disk to the troubleshooting VM.</span></span> <span data-ttu-id="6c311-195">Voici un exemple de sortie de commande et d’invite :</span><span class="sxs-lookup"><span data-stu-id="6c311-195">An example of the command output and prompts is as follows:</span></span>

```azurecli
info:    Executing command group deployment create
info:    Supply values for the following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment to complete
+
```


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="6c311-196">Réactiver les diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="6c311-196">Re-enable boot diagnostics</span></span>

<span data-ttu-id="6c311-197">Lorsque vous créez votre machine virtuelle à partir du disque dur virtuel existant, les diagnostics de démarrage peuvent ne pas être automatiquement activés.</span><span class="sxs-lookup"><span data-stu-id="6c311-197">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="6c311-198">L’exemple suivant active l’extension de diagnostic sur la machine virtuelle nommée `myDeployedVM`, dans le groupe de ressources nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="6c311-198">The following example enables the diagnostic extension on the VM named `myDeployedVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="6c311-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6c311-199">Next steps</span></span>
<span data-ttu-id="6c311-200">Si vous rencontrez des problèmes pour vous connecter à votre machine virtuelle, consultez la rubrique [Dépannage d’une connexion SSH à une machine virtuelle Linux Azure défaillante, qui génère une erreur ou qui est refusée](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6c311-200">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="6c311-201">Pour résoudre les problèmes liés à l’accès aux applications exécutées sur votre machine virtuelle, consultez la section [Résoudre les problèmes de connectivité des applications sur une machine virtuelle Linux Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6c311-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>