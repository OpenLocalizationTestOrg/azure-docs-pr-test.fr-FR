---
title: "aaaConfigure Gestionnaire de volume logique sur une machine virtuelle exécutant Linux | Documents Microsoft"
description: "Découvrez comment tooconfigure Gestionnaire de volume logique sur Linux dans Azure."
services: virtual-machines-linux
documentationcenter: na
author: szarkos
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: 7f533725-1484-479d-9472-6b3098d0aecc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 8daf792d87c6bb3d91a2eddcd01cfab34fd28cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="206ef-103">Configurer LVM sur une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="206ef-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="206ef-104">Ce document vous explique comment tooconfigure logique Volume Manager (Gestionnaire de volume logique) dans votre machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="206ef-104">This document will discuss how tooconfigure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="206ef-105">Bien qu’il soit possible tooconfigure que gestionnaire de volume logique sur n’importe quel disque attaché toohello virtual machine, par défaut cloud la plupart des images n’aura pas Gestionnaire de volume logique configuré sur hello disque de système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="206ef-105">While it is feasible tooconfigure LVM on any disk attached toohello virtual machine, by default most cloud images will not have LVM configured on hello OS disk.</span></span> <span data-ttu-id="206ef-106">Il s’agit des problèmes de tooprevent avec les groupes de volumes en double si hello disque de système d’exploitation est déjà attaché tooanother VM de hello distribution même type et, par exemple, lors d’un scénario de récupération.</span><span class="sxs-lookup"><span data-stu-id="206ef-106">This is tooprevent problems with duplicate volume groups if hello OS disk is ever attached tooanother VM of hello same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="206ef-107">Par conséquent, il est recommandé uniquement toouse Gestionnaire de volume logique sur des disques de données hello.</span><span class="sxs-lookup"><span data-stu-id="206ef-107">Therefore it is recommended only toouse LVM on hello data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="206ef-108">Volumes logiques linéaires et agrégé par bandes</span><span class="sxs-lookup"><span data-stu-id="206ef-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="206ef-109">Gestionnaire de volume logique peut être utilisé toocombine un nombre de disques physiques dans un seul volume de stockage.</span><span class="sxs-lookup"><span data-stu-id="206ef-109">LVM can be used toocombine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="206ef-110">Par défaut Gestionnaire de volume logique crée généralement des volumes logiques linéaires, ce qui signifie que le stockage physique de hello concaténé ensemble.</span><span class="sxs-lookup"><span data-stu-id="206ef-110">By default LVM will usually create linear logical volumes, which means that hello physical storage is concatenated together.</span></span> <span data-ttu-id="206ef-111">Dans ce cas les opérations de lecture/écriture seront généralement uniquement envoyées tooa seul disque.</span><span class="sxs-lookup"><span data-stu-id="206ef-111">In this case read/write operations will typically only be sent tooa single disk.</span></span> <span data-ttu-id="206ef-112">En revanche, nous pouvons également créer des volumes agrégés par bandes de logiques où les lectures et écritures sont les disques toomultiple distribuée contenues dans le groupe de volumes hello (c'est-à-dire similaire tooRAID0).</span><span class="sxs-lookup"><span data-stu-id="206ef-112">In contrast, we can also create striped logical volumes where reads and writes are distributed toomultiple disks contained in hello volume group (i.e. similar tooRAID0).</span></span> <span data-ttu-id="206ef-113">Pour des performances optimales, qu'il est probable que vous pouvez toostripe vos volumes logiques afin que les lectures et écritures utilisent tous vos disques de données attaché.</span><span class="sxs-lookup"><span data-stu-id="206ef-113">For performance reasons it is likely you will want toostripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="206ef-114">Ce document sera décrivent comment toocombine les données de plusieurs disques dans un seul groupe de volumes, puis créez un volume logique.</span><span class="sxs-lookup"><span data-stu-id="206ef-114">This document will describe how toocombine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="206ef-115">les étapes de Hello ci-dessous sont quelque peu généralisée toowork avec la plupart des distributions.</span><span class="sxs-lookup"><span data-stu-id="206ef-115">hello steps below are somewhat generalized toowork with most distributions.</span></span> <span data-ttu-id="206ef-116">Dans la plupart des hello de cas les utilitaires et les flux de travail pour la gestion du Gestionnaire de volume logique sur Azure n’est pas fondamentalement différentes des autres environnements.</span><span class="sxs-lookup"><span data-stu-id="206ef-116">In most cases hello utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="206ef-117">Comme d’habitude, veuillez également consulter votre fournisseur Linux pour obtenir la documentation et les meilleures pratiques pour utiliser LVM avec votre distribution spécifique.</span><span class="sxs-lookup"><span data-stu-id="206ef-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="206ef-118">Disques de données attachés</span><span class="sxs-lookup"><span data-stu-id="206ef-118">Attaching data disks</span></span>
<span data-ttu-id="206ef-119">Un est souhaitable généralement toostart avec deux ou plusieurs disques de données vide lors de l’utilisation du Gestionnaire de volume logique.</span><span class="sxs-lookup"><span data-stu-id="206ef-119">One will usually want toostart with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="206ef-120">Selon vos besoins d’e/s, vous pouvez choisir les disques tooattach qui sont stockées dans notre stockage Standard, avec des e/s de too500/ps par le stockage sur disque ou notre Premium avec des e/s de too5000/ps par disque.</span><span class="sxs-lookup"><span data-stu-id="206ef-120">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="206ef-121">Cet article ne sera pas entrer dans les détails sur la façon de tooprovision et attacher une machine virtuelle Linux données disques tooa.</span><span class="sxs-lookup"><span data-stu-id="206ef-121">This article will not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span> <span data-ttu-id="206ef-122">Consultez l’article de Microsoft Azure hello [attacher un disque](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour obtenir des instructions détaillées sur tooattach un vide de données de disque virtuels tooa Linux sur Azure.</span><span class="sxs-lookup"><span data-stu-id="206ef-122">Please see hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-lvm-utilities"></a><span data-ttu-id="206ef-123">Installez les utilitaires du Gestionnaire de volume logique hello</span><span class="sxs-lookup"><span data-stu-id="206ef-123">Install hello LVM utilities</span></span>
* <span data-ttu-id="206ef-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="206ef-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="206ef-125">**RHEL, CentOS &amp; Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="206ef-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="206ef-126">**SLES 12 et openSUSE**</span><span class="sxs-lookup"><span data-stu-id="206ef-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="206ef-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="206ef-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="206ef-128">Sur SLES11 vous devez également modifier `/etc/sysconfig/lvm` et définissez `LVM_ACTIVATED_ON_DISCOVERED` trop « activer » :</span><span class="sxs-lookup"><span data-stu-id="206ef-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` too"enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="206ef-129">Configurer LVM</span><span class="sxs-lookup"><span data-stu-id="206ef-129">Configure LVM</span></span>
<span data-ttu-id="206ef-130">Dans ce guide, nous supposerons vous avez attaché les trois disques de données, ce qui nous l’appellerons tooas `/dev/sdc`, `/dev/sdd` et `/dev/sde`.</span><span class="sxs-lookup"><span data-stu-id="206ef-130">In this guide we will assume you have attached three data disks, which we'll refer tooas `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="206ef-131">Notez qu’il ne peuvent pas toujours être hello mêmes noms de chemin d’accès dans votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="206ef-131">Note that these may not always be hello same path names in your VM.</span></span> <span data-ttu-id="206ef-132">Vous pouvez exécuter '`sudo fdisk -l`' ou toolist de commande similaires vos disques disponibles.</span><span class="sxs-lookup"><span data-stu-id="206ef-132">You can run '`sudo fdisk -l`' or similar command toolist your available disks.</span></span>

1. <span data-ttu-id="206ef-133">Préparer les volumes physiques hello :</span><span class="sxs-lookup"><span data-stu-id="206ef-133">Prepare hello physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="206ef-134">Créez un groupe de volumes.</span><span class="sxs-lookup"><span data-stu-id="206ef-134">Create a volume group.</span></span> <span data-ttu-id="206ef-135">Dans cet exemple, nous appelons un groupe de volumes hello `data-vg01`:</span><span class="sxs-lookup"><span data-stu-id="206ef-135">In this example we are calling hello volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="206ef-136">Créer ou les volumes logiques hello.</span><span class="sxs-lookup"><span data-stu-id="206ef-136">Create hello logical volume(s).</span></span> <span data-ttu-id="206ef-137">Hello commande ci-dessous, nous crée un volume logique appelé `data-lv01` toospan hello ensemble groupe de volumes, mais il est également possible toocreate plusieurs volumes logiques dans un groupe de volumes hello.</span><span class="sxs-lookup"><span data-stu-id="206ef-137">hello command below we will create a single logical volume called `data-lv01` toospan hello entire volume group, but note that it is also feasible toocreate multiple logical volumes in hello volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="206ef-138">Format du volume logique hello</span><span class="sxs-lookup"><span data-stu-id="206ef-138">Format hello logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="206ef-139">Avec SLES 11, utilisez `-t ext3` plutôt qu’ext4.</span><span class="sxs-lookup"><span data-stu-id="206ef-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="206ef-140">SLES11 prend uniquement en charge les systèmes de fichiers tooext4 accès en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="206ef-140">SLES11 only supports read-only access tooext4 filesystems.</span></span>

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="206ef-141">Ajouter hello nouveau fichier système trop/etc/fstab</span><span class="sxs-lookup"><span data-stu-id="206ef-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="206ef-142">Mal modification hello `/etc/fstab` fichier peut entraîner un système non démarrable.</span><span class="sxs-lookup"><span data-stu-id="206ef-142">Improperly editing hello `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="206ef-143">En cas de doute, consultez la documentation de la distribution toohello pour plus d’informations sur la façon dont tooproperly modifier ce fichier.</span><span class="sxs-lookup"><span data-stu-id="206ef-143">If unsure, please refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="206ef-144">Il est également recommandé d’une sauvegarde de hello `/etc/fstab` fichier est créé avant la modification.</span><span class="sxs-lookup"><span data-stu-id="206ef-144">It is also recommended that a backup of hello `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="206ef-145">Créez le point de montage hello souhaité pour votre nouveau système de fichiers, par exemple :</span><span class="sxs-lookup"><span data-stu-id="206ef-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="206ef-146">Recherchez le chemin d’accès du volume logique hello</span><span class="sxs-lookup"><span data-stu-id="206ef-146">Locate hello logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="206ef-147">Ouvrez `/etc/fstab` dans un éditeur de texte et ajoutez une entrée pour le nouveau système de fichiers hello, par exemple :</span><span class="sxs-lookup"><span data-stu-id="206ef-147">Open `/etc/fstab` in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="206ef-148">Ensuite, enregistrez et fermez `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="206ef-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="206ef-149">Tester ce hello `/etc/fstab` entrée est correcte :</span><span class="sxs-lookup"><span data-stu-id="206ef-149">Test that hello `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="206ef-150">Si cette commande renvoie un message d’erreur de syntaxe hello dans hello Vérifiez `/etc/fstab` fichier.</span><span class="sxs-lookup"><span data-stu-id="206ef-150">If this command results in an error message please check hello syntax in hello `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="206ef-151">Prochaine exécution hello `mount` système de fichiers de commandes tooensure hello est monté :</span><span class="sxs-lookup"><span data-stu-id="206ef-151">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="206ef-152">(Facultatif) Paramètres de démarrage fiables dans `/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="206ef-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="206ef-153">Nombre de distributions inclure soit hello `nobootwait` ou `nofail` monter des paramètres qui peuvent être ajoutées toohello `/etc/fstab` fichier.</span><span class="sxs-lookup"><span data-stu-id="206ef-153">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello `/etc/fstab` file.</span></span> <span data-ttu-id="206ef-154">Ces paramètres permettent échecs lors du montage d’un système de fichiers particulier et autoriser hello Linux système toocontinue tooboot même s’il est impossible de tooproperly montage hello RAID.</span><span class="sxs-lookup"><span data-stu-id="206ef-154">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="206ef-155">Veuillez consultez la documentation de la distribution tooyour pour plus d’informations sur ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="206ef-155">Please refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="206ef-156">Exemple (Ubuntu) :</span><span class="sxs-lookup"><span data-stu-id="206ef-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="206ef-157">Prise en charge de TRIM/UNMAP</span><span class="sxs-lookup"><span data-stu-id="206ef-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="206ef-158">Certains noyaux Linux prend en charge TRIM/annuler le mappage operations toodiscard les blocs inutilisés sur le disque de hello.</span><span class="sxs-lookup"><span data-stu-id="206ef-158">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="206ef-159">Ces opérations sont principalement dans tooinform standard de stockage Azure qui pages supprimées ne sont plus valides et peuvent être ignorées.</span><span class="sxs-lookup"><span data-stu-id="206ef-159">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="206ef-160">Le fait d’ignorer des pages peut vous permettre de réaliser des économies si vous créez des fichiers volumineux, puis les supprimez.</span><span class="sxs-lookup"><span data-stu-id="206ef-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="206ef-161">Il existe deux façons tooenable TRIM prend en charge dans votre VM Linux.</span><span class="sxs-lookup"><span data-stu-id="206ef-161">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="206ef-162">Comme d’habitude, consultez votre distribution pour hello approche recommandée :</span><span class="sxs-lookup"><span data-stu-id="206ef-162">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="206ef-163">Hello d’utilisation `discard` monter option dans `/etc/fstab`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="206ef-163">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="206ef-164">Dans certains hello cas `discard` option peut avoir des conséquences sur les performances.</span><span class="sxs-lookup"><span data-stu-id="206ef-164">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="206ef-165">Vous pouvez également exécuter hello `fstrim` commande manuellement à partir de la ligne de commande hello ou ajoutez-le tooyour crontab toorun régulièrement :</span><span class="sxs-lookup"><span data-stu-id="206ef-165">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="206ef-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="206ef-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="206ef-167">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="206ef-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
