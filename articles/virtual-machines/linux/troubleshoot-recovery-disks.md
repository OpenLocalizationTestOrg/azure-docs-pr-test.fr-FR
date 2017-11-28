---
title: "aaaUse une résolution des problèmes de la machine virtuelle avec hello Azure CLI 2.0 de Linux | Documents Microsoft"
description: "Découvrez comment tootroubleshoot Linux VM émet par connexion hello du système d’exploitation disque tooa récupération machine virtuelle à l’aide de hello Azure CLI 2.0"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a><span data-ttu-id="e25ac-103">Dépanner une VM Linux en attachant hello du système d’exploitation disque tooa ordinateur virtuel de récupération avec hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e25ac-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM with hello Azure CLI 2.0</span></span>
<span data-ttu-id="e25ac-104">Si votre machine virtuelle de Linux (VM) rencontre une erreur de démarrage ou de disque, vous devrez peut-être tooperform étapes de dépannage sur le disque dur virtuel hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="e25ac-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="e25ac-105">Un exemple courant est une entrée non valide dans `/etc/fstab` qui empêche de hello machine virtuelle en mesure de tooboot avec succès.</span><span class="sxs-lookup"><span data-stu-id="e25ac-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="e25ac-106">Cet article explique comment toouse hello Azure CLI 2.0 tooconnect votre virtuel dur disque tooanother Linux VM toofix toutes les erreurs, puis recréer votre machine virtuelle d’origine.</span><span class="sxs-lookup"><span data-stu-id="e25ac-106">This article details how toouse hello Azure CLI 2.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span> <span data-ttu-id="e25ac-107">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e25ac-107">You can also perform these steps with hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="e25ac-108">Vue d’ensemble du processus de récupération</span><span class="sxs-lookup"><span data-stu-id="e25ac-108">Recovery process overview</span></span>
<span data-ttu-id="e25ac-109">Hello, résolution des problèmes de processus est la suivante :</span><span class="sxs-lookup"><span data-stu-id="e25ac-109">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="e25ac-110">Supprimer hello VM fait de rencontrer des problèmes, en conservant les disques durs virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="e25ac-110">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="e25ac-111">Attacher et monter tooanother de disque dur virtuel hello Linux VM à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="e25ac-111">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="e25ac-112">Se connecter toohello résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e25ac-112">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="e25ac-113">Modifier des fichiers ou d’exécuter des outils toofix problèmes sur les disque dur virtuel d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="e25ac-113">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="e25ac-114">Démontez et détacher le disque dur virtuel de hello de hello, résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e25ac-114">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="e25ac-115">Créer une machine virtuelle à l’aide de hello d’origine disque dur.</span><span class="sxs-lookup"><span data-stu-id="e25ac-115">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="e25ac-116">tooperform ces étapes de dépannage vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e25ac-116">tooperform these troubleshooting steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="e25ac-117">Bonjour les exemples suivants, remplacez les noms de paramètres par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="e25ac-117">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="e25ac-118">Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `myVM`.</span><span class="sxs-lookup"><span data-stu-id="e25ac-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="e25ac-119">Identifier les problèmes de démarrage</span><span class="sxs-lookup"><span data-stu-id="e25ac-119">Determine boot issues</span></span>
<span data-ttu-id="e25ac-120">Examinez toodetermine de sortie série hello pourquoi votre machine virtuelle n’est pas en mesure de tooboot correctement.</span><span class="sxs-lookup"><span data-stu-id="e25ac-120">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="e25ac-121">Un exemple courant est une entrée non valide dans `/etc/fstab`, ou hello sous-jacent de disque dur virtuel est supprimé ou déplacé.</span><span class="sxs-lookup"><span data-stu-id="e25ac-121">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="e25ac-122">Obtenir les journaux de démarrage hello avec [az vm diagnostics de démarrage get-démarrage-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span><span class="sxs-lookup"><span data-stu-id="e25ac-122">Get hello boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="e25ac-123">Hello exemple suivant obtient hello série sortie à partir de hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e25ac-123">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="e25ac-124">Passez en revue les toodetermine de sortie série hello pourquoi hello VM échoue tooboot.</span><span class="sxs-lookup"><span data-stu-id="e25ac-124">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="e25ac-125">Si aucune indication n’offre pas de sortie de série hello, vous devrez peut-être tooreview les fichiers de journaux dans `/var/log` une fois que vous avez hello virtuel disque dur connecté tooa résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e25ac-125">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="e25ac-126">Afficher les détails du disque dur virtuel existant</span><span class="sxs-lookup"><span data-stu-id="e25ac-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="e25ac-127">Avant de pouvoir joindre votre disque dur virtuel (VHD) de tooanother machine virtuelle, vous devez tooidentify hello URI de disque de système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="e25ac-127">Before you can attach your virtual hard disk (VHD) tooanother VM, you need tooidentify hello URI of hello OS disk.</span></span> 

<span data-ttu-id="e25ac-128">Pour afficher des informations sur votre machine virtuelle, utilisez la commande [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="e25ac-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="e25ac-129">Hello d’utilisation `--query` le disque du système d’exploitation de toohello URI indicateur tooextract hello.</span><span class="sxs-lookup"><span data-stu-id="e25ac-129">Use hello `--query` flag tooextract hello URI toohello OS disk.</span></span> <span data-ttu-id="e25ac-130">exemple Hello Obtient des informations de disque pour hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e25ac-130">hello following example gets disk information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="e25ac-131">Hello URI est trop similaire**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span><span class="sxs-lookup"><span data-stu-id="e25ac-131">hello URI is similar too**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="e25ac-132">Supprimer une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="e25ac-132">Delete existing VM</span></span>
<span data-ttu-id="e25ac-133">Les disques durs virtuels et les machines virtuelles sont deux ressources distinctes dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e25ac-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="e25ac-134">Un disque dur virtuel consiste à stocker des hello système d’exploitation, des applications et des configurations.</span><span class="sxs-lookup"><span data-stu-id="e25ac-134">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="e25ac-135">Hello machine virtuelle proprement dite est simplement des métadonnées qui définit la taille de hello ou l’emplacement et fait référence à des ressources, tel qu’un disque dur virtuel ou d’une carte réseau virtuelle (NIC).</span><span class="sxs-lookup"><span data-stu-id="e25ac-135">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="e25ac-136">Chaque disque dur virtuel a un bail attribué lorsqu’il est attaché tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e25ac-136">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="e25ac-137">Bien que les disques de données peuvent être attachées et détachées même pendant l’exécution de la machine virtuelle de hello, les disques du système d’exploitation hello ne peut pas être détachée tant que hello ressource d’ordinateur virtuel est supprimé.</span><span class="sxs-lookup"><span data-stu-id="e25ac-137">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="e25ac-138">bail de Hello continue disque hello du système d’exploitation de tooassociate avec une machine virtuelle, même lorsque l’ordinateur virtuel est dans un état arrêté et est libéré.</span><span class="sxs-lookup"><span data-stu-id="e25ac-138">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="e25ac-139">Hello première étape toorecover votre machine virtuelle est la ressource d’ordinateur virtuel hello toodelete lui-même.</span><span class="sxs-lookup"><span data-stu-id="e25ac-139">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="e25ac-140">Suppression hello VM laisse hello des disques durs virtuels dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e25ac-140">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="e25ac-141">Après hello que machine virtuelle est supprimée, vous attachez hello disque dur virtuel tooanother VM tootroubleshoot et résolvez les erreurs de hello.</span><span class="sxs-lookup"><span data-stu-id="e25ac-141">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="e25ac-142">Supprimer hello machine virtuelle avec [az vm supprimer](/cli/azure/vm#delete).</span><span class="sxs-lookup"><span data-stu-id="e25ac-142">Delete hello VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="e25ac-143">Hello suivant supprime de l’exemple hello ordinateur virtuel nommé `myVM` du groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e25ac-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="e25ac-144">Attendez la fin hello VM suppression avant de joindre tooanother de disque dur virtuel hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e25ac-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="e25ac-145">bail Hello sur le disque dur virtuel hello qui associe hello machine virtuelle doit toobe publié avant de pouvoir joindre tooanother de disque dur virtuel hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e25ac-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="e25ac-146">Attacher tooanother de disque dur virtuel existant machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e25ac-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="e25ac-147">Pour hello en suivant quelques étapes, vous utilisez un autre ordinateur virtuel à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="e25ac-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="e25ac-148">Vous attachez hello toothis de disque dur virtuel existant dépannage toobrowse de machine virtuelle et que vous modifiez le contenu du disque hello.</span><span class="sxs-lookup"><span data-stu-id="e25ac-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="e25ac-149">Ce processus vous permet de toocorrect toutes les erreurs de configuration ou examiner des applications supplémentaires ou de système de fichiers journaux, par exemple.</span><span class="sxs-lookup"><span data-stu-id="e25ac-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="e25ac-150">Choisissez ou créez une autre machine virtuelle toouse, à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="e25ac-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="e25ac-151">Attacher hello disque dur virtuel existant avec [az non managée-disque de machine virtuelle attacher](/cli/azure/vm/unmanaged-disk#attach).</span><span class="sxs-lookup"><span data-stu-id="e25ac-151">Attach hello existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="e25ac-152">Lorsque vous attachez le disque dur virtuel existant hello, spécifiez le disque de toohello hello URI obtenu Bonjour précédent `az vm show` commande.</span><span class="sxs-lookup"><span data-stu-id="e25ac-152">When you attach hello existing virtual hard disk, specify hello URI toohello disk obtained in hello preceding `az vm show` command.</span></span> <span data-ttu-id="e25ac-153">exemple Hello attache un toohello disque dur virtuel existant, résolution des problèmes d’ordinateur virtuel nommé `myVMRecovery` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e25ac-153">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="e25ac-154">Monter le disque de données attaché hello</span><span class="sxs-lookup"><span data-stu-id="e25ac-154">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="e25ac-155">Hello exemples suivants décrivent les étapes hello requis sur un VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e25ac-155">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="e25ac-156">Si vous utilisez un autre distributeur Linux, telles que Red Hat Enterprise Linux ou SUSE, hello emplacements des fichiers journaux et `mount` commandes peuvent être légèrement différentes.</span><span class="sxs-lookup"><span data-stu-id="e25ac-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="e25ac-157">Consultez la documentation du toohello pour votre distribution spécifique pour les modifications appropriées de hello dans les commandes.</span><span class="sxs-lookup"><span data-stu-id="e25ac-157">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="e25ac-158">SSH tooyour de résolution des problèmes de la machine virtuelle en utilisant les informations d’identification appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="e25ac-158">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="e25ac-159">Si ce disque est hello première données disque attaché tooyour résolution des problèmes de la machine virtuelle, hello disque est probablement connecté trop`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="e25ac-159">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="e25ac-160">Utilisez `dmseg` tooview les disques attachés :</span><span class="sxs-lookup"><span data-stu-id="e25ac-160">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="e25ac-161">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="e25ac-161">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="e25ac-162">Bonjour précédent exemple, disque de hello du système d’exploitation est à `/dev/sda` et le disque temporaire hello fournie pour chaque ordinateur virtuel est à `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="e25ac-162">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="e25ac-163">Si vous possédiez plusieurs disques de données, ils doivent se trouver au niveau de `/dev/sdd`, `/dev/sde`, etc.</span><span class="sxs-lookup"><span data-stu-id="e25ac-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="e25ac-164">Créer un répertoire toomount votre disque dur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="e25ac-164">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="e25ac-165">Hello exemple suivant crée un répertoire nommé `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="e25ac-165">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="e25ac-166">Si vous avez plusieurs partitions sur votre disque dur virtuel existant, montez la partition de hello requis.</span><span class="sxs-lookup"><span data-stu-id="e25ac-166">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="e25ac-167">exemple Hello monte première partition principale hello à `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="e25ac-167">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="e25ac-168">Il est recommandé toomount des disques de données sur des machines virtuelles à l’aide d’Azure hello identificateur unique universel (UUID) du disque dur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="e25ac-168">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="e25ac-169">Pour ce scénario de dépannage court, le disque dur virtuel hello montage à l’aide de hello UUID n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e25ac-169">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="e25ac-170">Toutefois, en fonctionnement normal, Édition `/etc/fstab` à l’aide du nom de périphérique plutôt que UUID peut entraîner des disques durs virtuels toomount hello tooboot toofail de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e25ac-170">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="e25ac-171">Résoudre des problèmes sur le disque dur virtuel d’origine</span><span class="sxs-lookup"><span data-stu-id="e25ac-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="e25ac-172">Avec hello disque dur virtuel existant monté, vous pouvez désormais effectuer une maintenance et dépannage en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="e25ac-172">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="e25ac-173">Une fois que vous avez corrige les problèmes de hello, poursuivez hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="e25ac-173">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="e25ac-174">Démonter et dissocier le disque dur virtuel d’origine</span><span class="sxs-lookup"><span data-stu-id="e25ac-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="e25ac-175">Une fois les erreurs résolues, vous démontez et détachez un disque dur virtuel existant hello à partir de votre machine virtuelle de résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="e25ac-175">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="e25ac-176">Vous ne pouvez pas utiliser votre disque dur virtuel avec n’importe quel autre machine virtuelle jusqu'à ce que le bail hello attachement toohello de disque dur virtuel hello résolution des problèmes de la machine virtuelle est libéré.</span><span class="sxs-lookup"><span data-stu-id="e25ac-176">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="e25ac-177">À partir de hello tooyour de session SSH résolution des problèmes d’ordinateur virtuel, démontez le disque dur virtuel existant hello.</span><span class="sxs-lookup"><span data-stu-id="e25ac-177">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="e25ac-178">Modifiez d’abord en dehors du répertoire parent de hello pour votre point de montage :</span><span class="sxs-lookup"><span data-stu-id="e25ac-178">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="e25ac-179">Démonter le disque dur virtuel existant hello maintenant.</span><span class="sxs-lookup"><span data-stu-id="e25ac-179">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="e25ac-180">exemple Hello démonte périphérique hello sur `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="e25ac-180">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="e25ac-181">Maintenant détacher le disque dur virtuel de hello à partir de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="e25ac-181">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="e25ac-182">Quittez hello SSH session tooyour résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e25ac-182">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="e25ac-183">Hello de liste jointe tooyour de disques de données résolution des problèmes de la machine virtuelle avec [liste de disque non managée de machine virtuelle az](/cli/azure/vm/unmanaged-disk#list).</span><span class="sxs-lookup"><span data-stu-id="e25ac-183">List hello attached data disks tooyour troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="e25ac-184">listes hello disques de données d’exemple Hello attaché toohello ordinateur virtuel nommé `myVMRecovery` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e25ac-184">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="e25ac-185">Notez le nom hello pour votre disque dur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="e25ac-185">Note hello name for your existing virtual hard disk.</span></span> <span data-ttu-id="e25ac-186">Par exemple, le nom hello d’un disque avec hello URI de **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** est **myVHD**.</span><span class="sxs-lookup"><span data-stu-id="e25ac-186">For example, hello name of a disk with hello URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="e25ac-187">Détacher le disque de données hello à partir de votre machine virtuelle [az non managée-disque de machine virtuelle détacher](/cli/azure/vm/unmanaged-disk#detach).</span><span class="sxs-lookup"><span data-stu-id="e25ac-187">Detach hello data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="e25ac-188">exemple Hello détache disque hello nommé `myVHD` de hello ordinateur virtuel nommé `myVMRecovery` Bonjour `myResourceGroup` groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="e25ac-188">hello following example detaches hello disk named `myVHD` from hello VM named `myVMRecovery` in hello `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="e25ac-189">Créer une machine virtuelle à partir du disque dur d’origine</span><span class="sxs-lookup"><span data-stu-id="e25ac-189">Create VM from original hard disk</span></span>
<span data-ttu-id="e25ac-190">utilisation d’une machine virtuelle à partir de votre disque dur virtuel d’origine, toocreate [ce modèle Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="e25ac-190">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="e25ac-191">modèle JSON réel Hello est à hello lien :</span><span class="sxs-lookup"><span data-stu-id="e25ac-191">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="e25ac-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="e25ac-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="e25ac-193">modèle Hello déploie une machine virtuelle à l’aide de hello URI VHD à partir de hello commande précédemment.</span><span class="sxs-lookup"><span data-stu-id="e25ac-193">hello template deploys a VM using hello VHD URI from hello earlier command.</span></span> <span data-ttu-id="e25ac-194">Déployer le modèle hello avec [créer de déploiement de groupe az](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="e25ac-194">Deploy hello template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="e25ac-195">Fournir hello URI tooyour disque dur virtuel d’origine, puis spécifiez les type hello du système d’exploitation, la taille de machine virtuelle et nom d’ordinateur virtuel comme suit :</span><span class="sxs-lookup"><span data-stu-id="e25ac-195">Provide hello URI tooyour original VHD and then specify hello OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="e25ac-196">Réactiver les diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="e25ac-196">Re-enable boot diagnostics</span></span>
<span data-ttu-id="e25ac-197">Lorsque vous créez votre machine virtuelle à partir du disque dur virtuel existant hello, les diagnostics de démarrage ne peut pas être automatiquement activés.</span><span class="sxs-lookup"><span data-stu-id="e25ac-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="e25ac-198">Activez les diagnostics de démarrage avec la commande [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="e25ac-198">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="e25ac-199">Hello exemple suivant permet d’extension de diagnostic hello sur hello ordinateur virtuel nommé `myDeployedVM` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="e25ac-199">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="e25ac-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e25ac-200">Next steps</span></span>
<span data-ttu-id="e25ac-201">Si vous rencontrez des problèmes de connexion tooyour machine virtuelle, consultez [tooan dépanner SSH connexions Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e25ac-201">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e25ac-202">Pour résoudre les problèmes liés à l’accès aux applications exécutées sur votre machine virtuelle, consultez la section [Résoudre les problèmes de connectivité des applications sur une machine virtuelle Linux Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e25ac-202">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
