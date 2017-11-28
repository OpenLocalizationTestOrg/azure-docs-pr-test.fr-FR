---
title: "aaaUse a Linux résolution des problèmes de la machine virtuelle dans hello portail Azure | Documents Microsoft"
description: "Découvrez comment les problèmes d’ordinateur virtuel Linux tootroubleshoot par connexion hello du système d’exploitation disque tooa récupération machine virtuelle à l’aide de hello portail Azure"
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
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: 794daa06d7436215af84a61ab9088524254c47df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a><span data-ttu-id="2082a-103">Dépanner une VM Linux en attachant l’ordinateur virtuel de récupération tooa de disque hello du système d’exploitation à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="2082a-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure portal</span></span>
<span data-ttu-id="2082a-104">Si votre machine virtuelle de Linux (VM) rencontre une erreur de démarrage ou de disque, vous devrez peut-être tooperform étapes de dépannage sur le disque dur virtuel hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="2082a-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="2082a-105">Un exemple courant est une entrée non valide dans `/etc/fstab` qui empêche de hello machine virtuelle en mesure de tooboot avec succès.</span><span class="sxs-lookup"><span data-stu-id="2082a-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="2082a-106">Cet article explique comment toouse hello tooconnect portail Azure votre virtuel dur disque tooanother Linux VM toofix toutes les erreurs, puis recréer votre machine virtuelle d’origine.</span><span class="sxs-lookup"><span data-stu-id="2082a-106">This article details how toouse hello Azure portal tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="2082a-107">Vue d’ensemble du processus de récupération</span><span class="sxs-lookup"><span data-stu-id="2082a-107">Recovery process overview</span></span>
<span data-ttu-id="2082a-108">Hello, résolution des problèmes de processus est la suivante :</span><span class="sxs-lookup"><span data-stu-id="2082a-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="2082a-109">Supprimer hello VM fait de rencontrer des problèmes, en conservant les disques durs virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="2082a-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="2082a-110">Attacher et monter tooanother de disque dur virtuel hello Linux VM à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="2082a-110">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="2082a-111">Se connecter toohello résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2082a-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="2082a-112">Modifier des fichiers ou d’exécuter des outils toofix problèmes sur les disque dur virtuel d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="2082a-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="2082a-113">Démontez et détacher le disque dur virtuel de hello de hello, résolution des problèmes de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2082a-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="2082a-114">Créer une machine virtuelle à l’aide de hello d’origine disque dur.</span><span class="sxs-lookup"><span data-stu-id="2082a-114">Create a VM using hello original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="2082a-115">Identifier les problèmes de démarrage</span><span class="sxs-lookup"><span data-stu-id="2082a-115">Determine boot issues</span></span>
<span data-ttu-id="2082a-116">Examinez les diagnostics de démarrage hello et toodetermine de capture d’écran de machine virtuelle pourquoi votre machine virtuelle n’est pas en mesure de tooboot correctement.</span><span class="sxs-lookup"><span data-stu-id="2082a-116">Examine hello boot diagnostics and VM screenshot toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="2082a-117">Comme exemple courant, citons une entrée non valide dans `/etc/fstab`, ou le disque dur virtuel en cours de suppression ou de déplacement.</span><span class="sxs-lookup"><span data-stu-id="2082a-117">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="2082a-118">Sélectionnez votre machine virtuelle dans le portail de hello et faites défiler vers le bas toohello **prise en charge + dépannage** section.</span><span class="sxs-lookup"><span data-stu-id="2082a-118">Select your VM in hello portal and then scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="2082a-119">Cliquez sur **diagnostics de démarrage** messages de la console tooview hello diffusées en continu depuis votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2082a-119">Click **Boot diagnostics** tooview hello console messages streamed from your VM.</span></span> <span data-ttu-id="2082a-120">Révision hello journaux de la console toosee si vous pouvez déterminer pourquoi hello VM rencontre un problème.</span><span class="sxs-lookup"><span data-stu-id="2082a-120">Review hello console logs toosee if you can determine why hello VM is encountering an issue.</span></span> <span data-ttu-id="2082a-121">Hello suivant montre qu'une machine virtuelle est bloqué en mode de maintenance qui nécessite une intervention manuelle :</span><span class="sxs-lookup"><span data-stu-id="2082a-121">hello following example shows a VM stuck in maintenance mode that requires manual interaction:</span></span>

![Affichage des journaux de console des diagnostics de démarrage de la machine virtuelle](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

<span data-ttu-id="2082a-123">Vous pouvez également cliquer sur **capture d’écran de** haut hello de hello démarrage diagnostics journal toodownload une capture de capture d’écran de la machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="2082a-123">You can also click **Screenshot** across hello top of hello boot diagnostics log toodownload a capture of hello VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="2082a-124">Afficher les détails du disque dur virtuel existant</span><span class="sxs-lookup"><span data-stu-id="2082a-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="2082a-125">Avant de pouvoir joindre votre tooanother de disque dur virtuel machine virtuelle, vous devez nom de hello tooidentify de hello les disque dur virtuel (VHD).</span><span class="sxs-lookup"><span data-stu-id="2082a-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="2082a-126">Sélectionnez votre groupe de ressources à partir du portail de hello, puis sélectionnez votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2082a-126">Select your resource group from hello portal, then select your storage account.</span></span> <span data-ttu-id="2082a-127">Cliquez sur **BLOB**, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="2082a-127">Click **Blobs**, as in hello following example:</span></span>

![Sélectionner les blobs de stockage](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="2082a-129">En général, vous avez un conteneur nommé **vhds** qui stocke vos disques durs virtuels.</span><span class="sxs-lookup"><span data-stu-id="2082a-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="2082a-130">Sélectionnez le conteneur de hello tooview une liste de disques durs virtuels.</span><span class="sxs-lookup"><span data-stu-id="2082a-130">Select hello container tooview a list of virtual hard disks.</span></span> <span data-ttu-id="2082a-131">Nom de hello Remarque de votre disque dur virtuel (hello préfixe est généralement hello nom de votre machine virtuelle) :</span><span class="sxs-lookup"><span data-stu-id="2082a-131">Note hello name of your VHD (hello prefix is usually hello name of your VM):</span></span>

![Identifier le disque dur virtuel dans un conteneur de stockage](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="2082a-133">Sélectionnez votre disque dur virtuel existant à partir de la liste de hello et copier l’URL de hello pour une utilisation dans hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2082a-133">Select your existing virtual hard disk from hello list and copy hello URL for use in hello following steps:</span></span>

![Copier l’URL du disque dur virtuel existant](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="2082a-135">Supprimer une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="2082a-135">Delete existing VM</span></span>
<span data-ttu-id="2082a-136">Les disques durs virtuels et les machines virtuelles sont deux ressources distinctes dans Azure.</span><span class="sxs-lookup"><span data-stu-id="2082a-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="2082a-137">Un disque dur virtuel consiste à stocker des hello système d’exploitation, des applications et des configurations.</span><span class="sxs-lookup"><span data-stu-id="2082a-137">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="2082a-138">Hello machine virtuelle proprement dite est simplement des métadonnées qui définit la taille de hello ou l’emplacement et fait référence à des ressources, tel qu’un disque dur virtuel ou d’une carte réseau virtuelle (NIC).</span><span class="sxs-lookup"><span data-stu-id="2082a-138">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="2082a-139">Chaque disque dur virtuel a un bail attribué lorsqu’il est attaché tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2082a-139">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="2082a-140">Bien que les disques de données peuvent être attachées et détachées même pendant l’exécution de la machine virtuelle de hello, les disques du système d’exploitation hello ne peut pas être détachée tant que hello ressource d’ordinateur virtuel est supprimé.</span><span class="sxs-lookup"><span data-stu-id="2082a-140">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="2082a-141">bail de Hello continue disque hello du système d’exploitation de tooassociate avec une machine virtuelle, même lorsque l’ordinateur virtuel est dans un état arrêté et est libéré.</span><span class="sxs-lookup"><span data-stu-id="2082a-141">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="2082a-142">Hello première étape toorecover votre machine virtuelle est la ressource d’ordinateur virtuel hello toodelete lui-même.</span><span class="sxs-lookup"><span data-stu-id="2082a-142">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="2082a-143">Suppression hello VM laisse hello des disques durs virtuels dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2082a-143">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="2082a-144">Après hello que machine virtuelle est supprimée, vous attachez hello disque dur virtuel tooanother VM tootroubleshoot et résolvez les erreurs de hello.</span><span class="sxs-lookup"><span data-stu-id="2082a-144">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="2082a-145">Sélectionnez votre machine virtuelle dans le portail de hello, puis cliquez sur **supprimer**:</span><span class="sxs-lookup"><span data-stu-id="2082a-145">Select your VM in hello portal, then click **Delete**:</span></span>

![Capture d’écran de diagnostics de démarrage de machine virtuelle présentant une erreur de démarrage](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="2082a-147">Attendez la fin hello VM suppression avant de joindre tooanother de disque dur virtuel hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2082a-147">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="2082a-148">bail Hello sur le disque dur virtuel hello qui associe hello machine virtuelle doit toobe publié avant de pouvoir joindre tooanother de disque dur virtuel hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2082a-148">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="2082a-149">Attacher tooanother de disque dur virtuel existant machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="2082a-149">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="2082a-150">Pour hello en suivant quelques étapes, vous utilisez un autre ordinateur virtuel à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="2082a-150">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="2082a-151">Vous attachez hello toothis de disque dur virtuel existant toobrowse en mesure de machine virtuelle toobe de résolution des problèmes et que vous modifiez le contenu du disque hello.</span><span class="sxs-lookup"><span data-stu-id="2082a-151">You attach hello existing virtual hard disk toothis troubleshooting VM toobe able toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="2082a-152">Ce processus vous permet de toocorrect toutes les erreurs de configuration ou examiner des applications supplémentaires ou de système de fichiers journaux, par exemple.</span><span class="sxs-lookup"><span data-stu-id="2082a-152">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="2082a-153">Choisissez ou créez une autre machine virtuelle toouse, à des fins de dépannage.</span><span class="sxs-lookup"><span data-stu-id="2082a-153">Choose or create another VM toouse for troubleshooting purposes.</span></span>

1. <span data-ttu-id="2082a-154">Sélectionnez votre groupe de ressources à partir du portail de hello, puis sélectionnez votre machine virtuelle de résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="2082a-154">Select your resource group from hello portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="2082a-155">Sélectionnez **Disques**, puis cliquez sur **Attacher existant** :</span><span class="sxs-lookup"><span data-stu-id="2082a-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Attacher un disque existant dans le portail de hello](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="2082a-157">tooselect votre disque dur virtuel existant, cliquez sur **fichier de disque dur virtuel**:</span><span class="sxs-lookup"><span data-stu-id="2082a-157">tooselect your existing virtual hard disk, click **VHD File**:</span></span>

    ![Rechercher le disque dur virtuel existant](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="2082a-159">Sélectionnez votre compte de stockage et votre conteneur, puis cliquez sur votre disque dur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="2082a-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="2082a-160">Cliquez sur hello **sélectionnez** bouton tooconfirm votre choix :</span><span class="sxs-lookup"><span data-stu-id="2082a-160">Click hello **Select** button tooconfirm your choice:</span></span>

    ![Sélectionner votre disque dur virtuel existant](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="2082a-162">Cliquez sur votre disque dur virtuel sélectionné maintenant, **OK** tooattach hello disque dur virtuel existant :</span><span class="sxs-lookup"><span data-stu-id="2082a-162">With your VHD now selected, click **OK** tooattach hello existing virtual hard disk:</span></span>

    ![Confirmer l’attachement du disque dur virtuel existant](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="2082a-164">Après quelques secondes, hello **disques** répertorie pour votre machine virtuelle votre disque dur virtuel existant connecté en tant qu’un disque de données :</span><span class="sxs-lookup"><span data-stu-id="2082a-164">After a few seconds, hello **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Disque dur virtuel existant attaché en tant que disque de données](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="2082a-166">Monter le disque de données attaché hello</span><span class="sxs-lookup"><span data-stu-id="2082a-166">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="2082a-167">Hello exemples suivants décrivent les étapes hello requis sur un VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="2082a-167">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="2082a-168">Si vous utilisez un autre distributeur Linux, telles que Red Hat Enterprise Linux ou SUSE, hello emplacements des fichiers journaux et `mount` commandes peuvent être légèrement différentes.</span><span class="sxs-lookup"><span data-stu-id="2082a-168">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="2082a-169">Consultez la documentation du toohello pour votre distribution spécifique pour les modifications appropriées de hello dans les commandes.</span><span class="sxs-lookup"><span data-stu-id="2082a-169">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="2082a-170">SSH tooyour de résolution des problèmes de la machine virtuelle en utilisant les informations d’identification appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="2082a-170">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="2082a-171">Si ce disque est hello première données disque attaché tooyour résolution des problèmes de la machine virtuelle, il est probablement connecté trop`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="2082a-171">If this disk is hello first data disk attached tooyour troubleshooting VM, it is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="2082a-172">Utilisez `dmseg` toolist les disques attachés :</span><span class="sxs-lookup"><span data-stu-id="2082a-172">Use `dmseg` toolist attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```
    <span data-ttu-id="2082a-173">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="2082a-173">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="2082a-174">Bonjour précédent exemple, disque de hello du système d’exploitation est à `/dev/sda` et le disque temporaire hello fournie pour chaque ordinateur virtuel est à `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="2082a-174">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="2082a-175">Si vous possédiez plusieurs disques de données, ils doivent se trouver au niveau de `/dev/sdd`, `/dev/sde`, etc.</span><span class="sxs-lookup"><span data-stu-id="2082a-175">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="2082a-176">Créer un répertoire toomount votre disque dur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="2082a-176">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="2082a-177">Hello exemple suivant crée un répertoire nommé `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="2082a-177">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="2082a-178">Si vous avez plusieurs partitions sur votre disque dur virtuel existant, montez la partition de hello requis.</span><span class="sxs-lookup"><span data-stu-id="2082a-178">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="2082a-179">exemple Hello monte première partition principale hello à `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="2082a-179">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="2082a-180">Il est recommandé toomount des disques de données sur des machines virtuelles à l’aide d’Azure hello identificateur unique universel (UUID) du disque dur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="2082a-180">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="2082a-181">Pour ce scénario de dépannage court, le disque dur virtuel hello montage à l’aide de hello UUID n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2082a-181">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="2082a-182">Toutefois, en fonctionnement normal, Édition `/etc/fstab` à l’aide du nom de périphérique plutôt que UUID peut entraîner des disques durs virtuels toomount hello tooboot toofail de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2082a-182">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="2082a-183">Résoudre des problèmes sur le disque dur virtuel d’origine</span><span class="sxs-lookup"><span data-stu-id="2082a-183">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="2082a-184">Avec hello disque dur virtuel existant monté, vous pouvez désormais effectuer une maintenance et dépannage en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="2082a-184">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="2082a-185">Une fois que vous avez corrige les problèmes de hello, poursuivez hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="2082a-185">Once you have addressed hello issues, continue with hello following steps.</span></span>

## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="2082a-186">Démonter et dissocier le disque dur virtuel d’origine</span><span class="sxs-lookup"><span data-stu-id="2082a-186">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="2082a-187">Une fois les erreurs résolues, détachez hello disque dur virtuel existant à partir de votre machine virtuelle de résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="2082a-187">Once your errors are resolved, detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="2082a-188">Vous ne pouvez pas utiliser votre disque dur virtuel avec n’importe quel autre machine virtuelle jusqu'à ce que le bail hello attachement toohello de disque dur virtuel hello résolution des problèmes de la machine virtuelle est libéré.</span><span class="sxs-lookup"><span data-stu-id="2082a-188">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="2082a-189">À partir de hello tooyour de session SSH résolution des problèmes d’ordinateur virtuel, démontez le disque dur virtuel existant hello.</span><span class="sxs-lookup"><span data-stu-id="2082a-189">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="2082a-190">Modifiez d’abord en dehors du répertoire parent de hello pour votre point de montage :</span><span class="sxs-lookup"><span data-stu-id="2082a-190">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="2082a-191">Démonter le disque dur virtuel existant hello maintenant.</span><span class="sxs-lookup"><span data-stu-id="2082a-191">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="2082a-192">exemple Hello démonte périphérique hello sur `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="2082a-192">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="2082a-193">Maintenant détacher le disque dur virtuel de hello à partir de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="2082a-193">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="2082a-194">Sélectionnez votre machine virtuelle dans le portail de hello et cliquez sur **disques**.</span><span class="sxs-lookup"><span data-stu-id="2082a-194">Select your VM in hello portal and click **Disks**.</span></span> <span data-ttu-id="2082a-195">Sélectionnez votre disque dur virtuel existant, puis cliquez **Dissocier** :</span><span class="sxs-lookup"><span data-stu-id="2082a-195">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Dissocier le disque dur virtuel existant](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="2082a-197">Attendez que hello machine virtuelle a été correctement détaché disque de données hello avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="2082a-197">Wait until hello VM has successfully detached hello data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="2082a-198">Créer une machine virtuelle à partir du disque dur d’origine</span><span class="sxs-lookup"><span data-stu-id="2082a-198">Create VM from original hard disk</span></span>
<span data-ttu-id="2082a-199">utilisation d’une machine virtuelle à partir de votre disque dur virtuel d’origine, toocreate [ce modèle Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="2082a-199">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="2082a-200">modèle de Hello déploie une machine virtuelle dans un réseau virtuel existant, à l’aide de hello URL de disque dur virtuel à partir de hello commande précédemment.</span><span class="sxs-lookup"><span data-stu-id="2082a-200">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="2082a-201">Cliquez sur hello **déployer tooAzure** bouton comme suit :</span><span class="sxs-lookup"><span data-stu-id="2082a-201">Click hello **Deploy tooAzure** button as follows:</span></span>

![Déployer la machine virtuelle du modèle à partir de GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="2082a-203">modèle de Hello chargée hello portail Azure pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="2082a-203">hello template is loaded into hello Azure portal for deployment.</span></span> <span data-ttu-id="2082a-204">Entrez les noms de hello pour votre nouvelle machine virtuelle et les ressources Azure existantes et collez hello URL tooyour disque dur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="2082a-204">Enter hello names for your new VM and existing Azure resources, and paste hello URL tooyour existing virtual hard disk.</span></span> <span data-ttu-id="2082a-205">déploiement de hello toobegin, cliquez sur **achat**:</span><span class="sxs-lookup"><span data-stu-id="2082a-205">toobegin hello deployment, click **Purchase**:</span></span>

![Déployer une machine virtuelle à partir d’un modèle](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="2082a-207">Réactiver les diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="2082a-207">Re-enable boot diagnostics</span></span>
<span data-ttu-id="2082a-208">Lorsque vous créez votre machine virtuelle à partir du disque dur virtuel existant hello, les diagnostics de démarrage ne peut pas être automatiquement activés.</span><span class="sxs-lookup"><span data-stu-id="2082a-208">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="2082a-209">toocheck hello état des diagnostics de démarrage et l’activer si nécessaire, sélectionnez votre machine virtuelle dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="2082a-209">toocheck hello status of boot diagnostics and turn on if needed, select your VM in hello portal.</span></span> <span data-ttu-id="2082a-210">Sous **Surveillance**, cliquez sur **Paramètres de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="2082a-210">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="2082a-211">Vérifiez l’état de hello est **sur**, et hello coche ensuite trop**diagnostics de démarrage** est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="2082a-211">Ensure hello status is **On**, and hello check mark next too**Boot diagnostics** is selected.</span></span> <span data-ttu-id="2082a-212">Si vous apportez des modifications, cliquez sur **Enregistrer** :</span><span class="sxs-lookup"><span data-stu-id="2082a-212">If you make any changes, click **Save**:</span></span>

![Mettre à jour les paramètres des diagnostics de démarrage](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="2082a-214">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2082a-214">Next steps</span></span>
<span data-ttu-id="2082a-215">Si vous rencontrez des problèmes de connexion tooyour machine virtuelle, consultez [tooan dépanner SSH connexions Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2082a-215">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2082a-216">Pour résoudre les problèmes liés à l’accès aux applications exécutées sur votre machine virtuelle, consultez la section [Résoudre les problèmes de connectivité des applications sur une machine virtuelle Linux Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2082a-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="2082a-217">Pour plus d’informations sur l’utilisation de Resource Manager, consultez la page [Présentation d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2082a-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
