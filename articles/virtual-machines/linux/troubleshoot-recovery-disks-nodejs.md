---
title: "aaaUse une résolution des problèmes de la machine virtuelle avec hello Azure CLI 1.0 de Linux | Documents Microsoft"
description: "Découvrez comment tootroubleshoot Linux VM émet par connexion hello du système d’exploitation disque tooa récupération machine virtuelle à l’aide de hello Azure CLI 1.0"
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
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a><span data-ttu-id="e074c-103">Dépanner une VM Linux en attachant l’ordinateur virtuel de récupération tooa de disque hello du système d’exploitation à l’aide de hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e074c-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="e074c-104">Si votre machine virtuelle de Linux (VM) rencontre une erreur de démarrage ou de disque, vous devrez peut-être tooperform étapes de dépannage sur le disque dur virtuel hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="e074c-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="e074c-105">Un exemple courant est une entrée non valide dans `/etc/fstab` qui empêche de hello machine virtuelle en mesure de tooboot avec succès.</span><span class="sxs-lookup"><span data-stu-id="e074c-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="e074c-106">Cet article explique comment toouse hello Azure CLI 1.0 tooconnect votre virtuel dur disque tooanother Linux VM toofix toutes les erreurs, puis recréer votre machine virtuelle d’origine.</span><span class="sxs-lookup"><span data-stu-id="e074c-106">This article details how toouse hello Azure CLI 1.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e074c-107">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="e074c-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="e074c-108">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="e074c-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="e074c-109">[Azure CLI 1.0](#recovery-process-overview) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="e074c-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e074c-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="e074c-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="e074c-111">Vue d’ensemble du processus de récupération</span><span class="sxs-lookup"><span data-stu-id="e074c-111">Recovery process overview</span></span>
<span data-ttu-id="e074c-112">Hello, résolution des problèmes de processus est la suivante :</span><span class="sxs-lookup"><span data-stu-id="e074c-112">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="e074c-113">Supprimer hello VM fait de rencontrer des problèmes, en conservant les disques durs virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="e074c-113">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="e074c-114">Attacher et monter tooanother de disque dur virtuel hello Linux VM à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="e074c-114">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="e074c-115">Se connecter toohello résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e074c-115">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="e074c-116">Modifier des fichiers ou d’exécuter des outils toofix problèmes sur les disque dur virtuel d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="e074c-116">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="e074c-117">Démontez et détacher le disque dur virtuel de hello de hello, résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e074c-117">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="e074c-118">Créer une machine virtuelle à l’aide de hello d’origine disque dur.</span><span class="sxs-lookup"><span data-stu-id="e074c-118">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="e074c-119">Assurez-vous que vous avez [hello dernière Azure CLI 1.0](../../cli-install-nodejs.md) installé et connecté à l’aide du mode de gestionnaire de ressources :</span><span class="sxs-lookup"><span data-stu-id="e074c-119">Make sure that you have [hello latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e074c-120">Bonjour les exemples suivants, remplacez les noms de paramètres par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="e074c-120">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="e074c-121">Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `myVM`.</span><span class="sxs-lookup"><span data-stu-id="e074c-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="e074c-122">Identifier les problèmes de démarrage</span><span class="sxs-lookup"><span data-stu-id="e074c-122">Determine boot issues</span></span>
<span data-ttu-id="e074c-123">Examinez toodetermine de sortie série hello pourquoi votre machine virtuelle n’est pas en mesure de tooboot correctement.</span><span class="sxs-lookup"><span data-stu-id="e074c-123">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="e074c-124">Un exemple courant est une entrée non valide dans `/etc/fstab`, ou hello sous-jacent de disque dur virtuel est supprimé ou déplacé.</span><span class="sxs-lookup"><span data-stu-id="e074c-124">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="e074c-125">Hello exemple suivant obtient hello série sortie à partir de hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e074c-125">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="e074c-126">Passez en revue les toodetermine de sortie série hello pourquoi hello VM échoue tooboot.</span><span class="sxs-lookup"><span data-stu-id="e074c-126">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="e074c-127">Si aucune indication n’offre pas de sortie de série hello, vous devrez peut-être tooreview les fichiers de journaux dans `/var/log` une fois que vous avez hello virtuel disque dur connecté tooa résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e074c-127">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="e074c-128">Afficher les détails du disque dur virtuel existant</span><span class="sxs-lookup"><span data-stu-id="e074c-128">View existing virtual hard disk details</span></span>
<span data-ttu-id="e074c-129">Avant de pouvoir joindre votre tooanother de disque dur virtuel machine virtuelle, vous devez nom de hello tooidentify de hello les disque dur virtuel (VHD).</span><span class="sxs-lookup"><span data-stu-id="e074c-129">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="e074c-130">Hello exemple suivant obtient les informations pour hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e074c-130">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="e074c-131">Recherchez `Vhd URI` dans sortie hello hello précédant la commande.</span><span class="sxs-lookup"><span data-stu-id="e074c-131">Look for `Vhd URI` in hello output from hello preceding command.</span></span> <span data-ttu-id="e074c-132">Hello tronquée exemple de sortie suivant affiche hello `Vhd URI` sur la dernière ligne de hello :</span><span class="sxs-lookup"><span data-stu-id="e074c-132">hello following truncated example output shows hello `Vhd URI` on hello last line:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
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


## <a name="delete-existing-vm"></a><span data-ttu-id="e074c-133">Supprimer une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="e074c-133">Delete existing VM</span></span>
<span data-ttu-id="e074c-134">Les disques durs virtuels et les machines virtuelles sont deux ressources distinctes dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e074c-134">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="e074c-135">Un disque dur virtuel consiste à stocker des hello système d’exploitation, des applications et des configurations.</span><span class="sxs-lookup"><span data-stu-id="e074c-135">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="e074c-136">Hello machine virtuelle proprement dite est simplement des métadonnées qui définit la taille de hello ou l’emplacement et fait référence à des ressources, tel qu’un disque dur virtuel ou d’une carte réseau virtuelle (NIC).</span><span class="sxs-lookup"><span data-stu-id="e074c-136">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="e074c-137">Chaque disque dur virtuel a un bail attribué lorsqu’il est attaché tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e074c-137">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="e074c-138">Bien que les disques de données peuvent être attachées et détachées même pendant l’exécution de la machine virtuelle de hello, les disques du système d’exploitation hello ne peut pas être détachée tant que hello ressource d’ordinateur virtuel est supprimé.</span><span class="sxs-lookup"><span data-stu-id="e074c-138">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="e074c-139">bail de Hello continue disque hello du système d’exploitation de tooassociate avec une machine virtuelle, même lorsque l’ordinateur virtuel est dans un état arrêté et est libéré.</span><span class="sxs-lookup"><span data-stu-id="e074c-139">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="e074c-140">Hello première étape toorecover votre machine virtuelle est la ressource d’ordinateur virtuel hello toodelete lui-même.</span><span class="sxs-lookup"><span data-stu-id="e074c-140">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="e074c-141">Suppression hello VM laisse hello des disques durs virtuels dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e074c-141">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="e074c-142">Après hello que machine virtuelle est supprimée, vous attachez hello disque dur virtuel tooanother VM tootroubleshoot et résolvez les erreurs de hello.</span><span class="sxs-lookup"><span data-stu-id="e074c-142">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="e074c-143">Hello suivant supprime de l’exemple hello ordinateur virtuel nommé `myVM` du groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e074c-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="e074c-144">Attendez la fin hello VM suppression avant de joindre tooanother de disque dur virtuel hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e074c-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="e074c-145">bail Hello sur le disque dur virtuel hello qui associe hello machine virtuelle doit toobe publié avant de pouvoir joindre tooanother de disque dur virtuel hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e074c-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="e074c-146">Attacher tooanother de disque dur virtuel existant machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e074c-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="e074c-147">Pour hello en suivant quelques étapes, vous utilisez un autre ordinateur virtuel à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="e074c-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="e074c-148">Vous attachez hello toothis de disque dur virtuel existant dépannage toobrowse de machine virtuelle et que vous modifiez le contenu du disque hello.</span><span class="sxs-lookup"><span data-stu-id="e074c-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="e074c-149">Ce processus vous permet de toocorrect toutes les erreurs de configuration ou examiner des applications supplémentaires ou de système de fichiers journaux, par exemple.</span><span class="sxs-lookup"><span data-stu-id="e074c-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="e074c-150">Choisissez ou créez une autre machine virtuelle toouse, à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="e074c-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="e074c-151">Lorsque vous attachez le disque dur virtuel existant hello, spécifier le disque de toohello URL hello obtenu Bonjour précédent `azure vm show` commande.</span><span class="sxs-lookup"><span data-stu-id="e074c-151">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `azure vm show` command.</span></span> <span data-ttu-id="e074c-152">exemple Hello attache un toohello disque dur virtuel existant, résolution des problèmes d’ordinateur virtuel nommé `myVMRecovery` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e074c-152">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="e074c-153">Monter le disque de données attaché hello</span><span class="sxs-lookup"><span data-stu-id="e074c-153">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="e074c-154">Hello exemples suivants décrivent les étapes hello requis sur un VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e074c-154">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="e074c-155">Si vous utilisez un autre distributeur Linux, telles que Red Hat Enterprise Linux ou SUSE, hello emplacements des fichiers journaux et `mount` commandes peuvent être légèrement différentes.</span><span class="sxs-lookup"><span data-stu-id="e074c-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="e074c-156">Consultez la documentation du toohello pour votre distribution spécifique pour les modifications appropriées de hello dans les commandes.</span><span class="sxs-lookup"><span data-stu-id="e074c-156">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="e074c-157">SSH tooyour de résolution des problèmes de la machine virtuelle en utilisant les informations d’identification appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="e074c-157">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="e074c-158">Si ce disque est hello première données disque attaché tooyour résolution des problèmes de la machine virtuelle, hello disque est probablement connecté trop`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="e074c-158">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="e074c-159">Utilisez `dmseg` tooview les disques attachés :</span><span class="sxs-lookup"><span data-stu-id="e074c-159">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="e074c-160">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="e074c-160">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="e074c-161">Bonjour précédent exemple, disque de hello du système d’exploitation est à `/dev/sda` et le disque temporaire hello fournie pour chaque ordinateur virtuel est à `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="e074c-161">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="e074c-162">Si vous possédiez plusieurs disques de données, ils doivent se trouver au niveau de `/dev/sdd`, `/dev/sde`, etc.</span><span class="sxs-lookup"><span data-stu-id="e074c-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="e074c-163">Créer un répertoire toomount votre disque dur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="e074c-163">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="e074c-164">Hello exemple suivant crée un répertoire nommé `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="e074c-164">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="e074c-165">Si vous avez plusieurs partitions sur votre disque dur virtuel existant, montez la partition de hello requis.</span><span class="sxs-lookup"><span data-stu-id="e074c-165">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="e074c-166">exemple Hello monte première partition principale hello à `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="e074c-166">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="e074c-167">Il est recommandé toomount des disques de données sur des machines virtuelles à l’aide d’Azure hello identificateur unique universel (UUID) du disque dur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="e074c-167">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="e074c-168">Pour ce scénario de dépannage court, le disque dur virtuel hello montage à l’aide de hello UUID n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e074c-168">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="e074c-169">Toutefois, en fonctionnement normal, Édition `/etc/fstab` à l’aide du nom de périphérique plutôt que UUID peut entraîner des disques durs virtuels toomount hello tooboot toofail de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e074c-169">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="e074c-170">Résoudre des problèmes sur le disque dur virtuel d’origine</span><span class="sxs-lookup"><span data-stu-id="e074c-170">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="e074c-171">Avec hello disque dur virtuel existant monté, vous pouvez désormais effectuer une maintenance et dépannage en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="e074c-171">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="e074c-172">Une fois que vous avez corrige les problèmes de hello, poursuivez hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="e074c-172">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="e074c-173">Démonter et dissocier le disque dur virtuel d’origine</span><span class="sxs-lookup"><span data-stu-id="e074c-173">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="e074c-174">Une fois les erreurs résolues, vous démontez et détachez un disque dur virtuel existant hello à partir de votre machine virtuelle de résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="e074c-174">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="e074c-175">Vous ne pouvez pas utiliser votre disque dur virtuel avec n’importe quel autre machine virtuelle jusqu'à ce que le bail hello attachement toohello de disque dur virtuel hello résolution des problèmes de la machine virtuelle est libéré.</span><span class="sxs-lookup"><span data-stu-id="e074c-175">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="e074c-176">À partir de hello tooyour de session SSH résolution des problèmes d’ordinateur virtuel, démontez le disque dur virtuel existant hello.</span><span class="sxs-lookup"><span data-stu-id="e074c-176">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="e074c-177">Modifiez d’abord en dehors du répertoire parent de hello pour votre point de montage :</span><span class="sxs-lookup"><span data-stu-id="e074c-177">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="e074c-178">Démonter le disque dur virtuel existant hello maintenant.</span><span class="sxs-lookup"><span data-stu-id="e074c-178">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="e074c-179">exemple Hello démonte périphérique hello sur `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="e074c-179">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="e074c-180">Maintenant détacher le disque dur virtuel de hello à partir de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="e074c-180">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="e074c-181">Quittez hello SSH session tooyour résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e074c-181">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="e074c-182">Bonjour CLI d’Azure, première hello de liste jointe tooyour de disques de données résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e074c-182">In hello Azure CLI, first list hello attached data disks tooyour troubleshooting VM.</span></span> <span data-ttu-id="e074c-183">listes hello disques de données d’exemple Hello attaché toohello ordinateur virtuel nommé `myVMRecovery` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e074c-183">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    <span data-ttu-id="e074c-184">Hello de note `Lun` valeur de votre disque dur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="e074c-184">Note hello `Lun` value for your existing virtual hard disk.</span></span> <span data-ttu-id="e074c-185">Hello exemple de sortie de commande suivant montre le disque virtuel existant par la hello est attaché à LUN 0 :</span><span class="sxs-lookup"><span data-stu-id="e074c-185">hello following example command output shows hello existing virtual disk attached at LUN 0:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    <span data-ttu-id="e074c-186">Détacher le disque de données hello à partir de votre machine virtuelle à l’aide de hello applicable `Lun` valeur :</span><span class="sxs-lookup"><span data-stu-id="e074c-186">Detach hello data disk from your VM using hello applicable `Lun` value:</span></span>

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="e074c-187">Créer une machine virtuelle à partir du disque dur d’origine</span><span class="sxs-lookup"><span data-stu-id="e074c-187">Create VM from original hard disk</span></span>
<span data-ttu-id="e074c-188">utilisation d’une machine virtuelle à partir de votre disque dur virtuel d’origine, toocreate [ce modèle Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="e074c-188">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="e074c-189">modèle JSON réel Hello est à hello lien :</span><span class="sxs-lookup"><span data-stu-id="e074c-189">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="e074c-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="e074c-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="e074c-191">modèle de Hello déploie une machine virtuelle dans un réseau virtuel existant, à l’aide de hello URL de disque dur virtuel à partir de hello commande précédemment.</span><span class="sxs-lookup"><span data-stu-id="e074c-191">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="e074c-192">exemple Hello déploie groupe de ressources hello modèle toohello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e074c-192">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

<span data-ttu-id="e074c-193">Hello de réponse demande modèle hello comme nom d’ordinateur virtuel (`myDeployedVM` hello selon exemple), type de système d’exploitation (`Linux`) et la taille de machine virtuelle (`Standard_DS1_v2`).</span><span class="sxs-lookup"><span data-stu-id="e074c-193">Answer hello prompts for hello template such as VM name (`myDeployedVM` hello following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span></span> <span data-ttu-id="e074c-194">Hello `osDiskVhdUri` est hello même que celui précédemment utilisé lors de l’attachement toohello disque dur virtuel existant de hello, résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e074c-194">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span> <span data-ttu-id="e074c-195">Un exemple de sortie de la commande hello et la demande est la suivante :</span><span class="sxs-lookup"><span data-stu-id="e074c-195">An example of hello command output and prompts is as follows:</span></span>

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
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
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="e074c-196">Réactiver les diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="e074c-196">Re-enable boot diagnostics</span></span>

<span data-ttu-id="e074c-197">Lorsque vous créez votre machine virtuelle à partir du disque dur virtuel existant hello, les diagnostics de démarrage ne peut pas être automatiquement activés.</span><span class="sxs-lookup"><span data-stu-id="e074c-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="e074c-198">Hello exemple suivant permet d’extension de diagnostic hello sur hello ordinateur virtuel nommé `myDeployedVM` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e074c-198">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="e074c-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e074c-199">Next steps</span></span>
<span data-ttu-id="e074c-200">Si vous rencontrez des problèmes de connexion tooyour machine virtuelle, consultez [tooan dépanner SSH connexions Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e074c-200">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e074c-201">Pour résoudre les problèmes liés à l’accès aux applications exécutées sur votre machine virtuelle, consultez la section [Résoudre les problèmes de connectivité des applications sur une machine virtuelle Linux Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e074c-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
