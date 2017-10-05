---
title: "Configurer LVM sur une machine virtuelle exécutant Linux | Microsoft Docs"
description: "Apprenez à configurer LVM sur Linux dans Azure."
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
ms.openlocfilehash: 7926627aaa3f0da935131f491d927ab5cb4b35c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="e957a-103">Configurer LVM sur une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="e957a-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="e957a-104">Ce document vous explique comment configurer le gestionnaire de volume logique (LVM) sur votre machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="e957a-104">This document will discuss how to configure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="e957a-105">Bien qu’il soit possible de configurer LVM sur tout disque connecté à la machine virtuelle, par défaut la plupart des images cloud n’auront pas LVM configuré sur le disque du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="e957a-105">While it is feasible to configure LVM on any disk attached to the virtual machine, by default most cloud images will not have LVM configured on the OS disk.</span></span> <span data-ttu-id="e957a-106">Cela vise à éviter les problèmes liés aux groupes de volumes en double si le disque du système d’exploitation est joint à une autre machine virtuelle de la distribution et du même type, par exemple lors d’un scénario de récupération.</span><span class="sxs-lookup"><span data-stu-id="e957a-106">This is to prevent problems with duplicate volume groups if the OS disk is ever attached to another VM of the same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="e957a-107">Par conséquent, il est recommandé de n’utiliser LVM que sur les disques de données.</span><span class="sxs-lookup"><span data-stu-id="e957a-107">Therefore it is recommended only to use LVM on the data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="e957a-108">Volumes logiques linéaires et agrégé par bandes</span><span class="sxs-lookup"><span data-stu-id="e957a-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="e957a-109">LVM peut être utilisé pour combiner plusieurs disques physiques en un seul volume de stockage.</span><span class="sxs-lookup"><span data-stu-id="e957a-109">LVM can be used to combine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="e957a-110">Par défaut, LVM crée généralement des volumes logiques linéaires, ce qui signifie que le stockage physique est concaténé.</span><span class="sxs-lookup"><span data-stu-id="e957a-110">By default LVM will usually create linear logical volumes, which means that the physical storage is concatenated together.</span></span> <span data-ttu-id="e957a-111">Dans ce cas les opérations de lecture/d’écriture sont généralement envoyées à un seul disque.</span><span class="sxs-lookup"><span data-stu-id="e957a-111">In this case read/write operations will typically only be sent to a single disk.</span></span> <span data-ttu-id="e957a-112">En revanche, nous pouvons également créer des volumes logiques agrégés par bandes où les lectures et écritures sont distribuées à plusieurs disques contenus dans le groupe de volumes (par exemple, similaire à RAID 0).</span><span class="sxs-lookup"><span data-stu-id="e957a-112">In contrast, we can also create striped logical volumes where reads and writes are distributed to multiple disks contained in the volume group (i.e. similar to RAID0).</span></span> <span data-ttu-id="e957a-113">Pour obtenir des performances optimales, il est recommandé d’agréger les volumes logiques afin que les lectures et écritures utilisent tous les disques de données joints.</span><span class="sxs-lookup"><span data-stu-id="e957a-113">For performance reasons it is likely you will want to stripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="e957a-114">Ce document décrit comment combiner plusieurs disques de données dans un seul groupe de volumes, puis créer un volume logique agrégé par bandes.</span><span class="sxs-lookup"><span data-stu-id="e957a-114">This document will describe how to combine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="e957a-115">Les étapes ci-dessous sont généralisées de manière à fonctionner avec la plupart des distributions.</span><span class="sxs-lookup"><span data-stu-id="e957a-115">The steps below are somewhat generalized to work with most distributions.</span></span> <span data-ttu-id="e957a-116">Dans la plupart des cas les utilitaires et les workflows de gestion LVM sur Azure ne sont pas fondamentalement différents des autres environnements.</span><span class="sxs-lookup"><span data-stu-id="e957a-116">In most cases the utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="e957a-117">Comme d’habitude, veuillez également consulter votre fournisseur Linux pour obtenir la documentation et les meilleures pratiques pour utiliser LVM avec votre distribution spécifique.</span><span class="sxs-lookup"><span data-stu-id="e957a-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="e957a-118">Disques de données attachés</span><span class="sxs-lookup"><span data-stu-id="e957a-118">Attaching data disks</span></span>
<span data-ttu-id="e957a-119">Il est généralement recommandé de commencer avec au moins deux disques de données pour utiliser LVM.</span><span class="sxs-lookup"><span data-stu-id="e957a-119">One will usually want to start with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="e957a-120">En fonction de vos besoins d’E/S, vous pouvez choisir d’attacher des disques qui sont stockés dans notre stockage Standard, avec un maximum de 500 opérations d’E/S par disque ou dans notre stockage Premium avec un maximum de 5 000 opérations d’E/S par disque.</span><span class="sxs-lookup"><span data-stu-id="e957a-120">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span></span> <span data-ttu-id="e957a-121">Cet article n’aborde pas en détail la marche à suivre pour approvisionner et attacher des disques de données sur une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="e957a-121">This article will not go into detail on how to provision and attach data disks to a Linux virtual machine.</span></span> <span data-ttu-id="e957a-122">Consultez l’article Microsoft Azure [Attacher un disque](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour obtenir des instructions détaillées sur la marche à suivre pour attacher un disque de données vide à une machine virtuelle Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e957a-122">Please see the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span></span>

## <a name="install-the-lvm-utilities"></a><span data-ttu-id="e957a-123">Installer les utilitaires LVM</span><span class="sxs-lookup"><span data-stu-id="e957a-123">Install the LVM utilities</span></span>
* <span data-ttu-id="e957a-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="e957a-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="e957a-125">**RHEL, CentOS & Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="e957a-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="e957a-126">**SLES 12 et openSUSE**</span><span class="sxs-lookup"><span data-stu-id="e957a-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="e957a-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="e957a-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="e957a-128">Sur SLES11, vous devez également modifier `/etc/sysconfig/lvm` et définir `LVM_ACTIVATED_ON_DISCOVERED` sur « activer » :</span><span class="sxs-lookup"><span data-stu-id="e957a-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` to "enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="e957a-129">Configurer LVM</span><span class="sxs-lookup"><span data-stu-id="e957a-129">Configure LVM</span></span>
<span data-ttu-id="e957a-130">Dans ce guide, nous supposons que vous avez connecté trois disques de données, nommés `/dev/sdc`, `/dev/sdd` et `/dev/sde`.</span><span class="sxs-lookup"><span data-stu-id="e957a-130">In this guide we will assume you have attached three data disks, which we'll refer to as `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="e957a-131">Notez que les chemins peuvent être différents dans votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e957a-131">Note that these may not always be the same path names in your VM.</span></span> <span data-ttu-id="e957a-132">Vous pouvez exécuter ’`sudo fdisk -l`’ ou une commande semblable pour répertorier vos disques disponibles.</span><span class="sxs-lookup"><span data-stu-id="e957a-132">You can run '`sudo fdisk -l`' or similar command to list your available disks.</span></span>

1. <span data-ttu-id="e957a-133">Préparer les volumes physiques :</span><span class="sxs-lookup"><span data-stu-id="e957a-133">Prepare the physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="e957a-134">Créez un groupe de volumes.</span><span class="sxs-lookup"><span data-stu-id="e957a-134">Create a volume group.</span></span> <span data-ttu-id="e957a-135">Dans cet exemple, nous appelons le groupe de volumes `data-vg01` :</span><span class="sxs-lookup"><span data-stu-id="e957a-135">In this example we are calling the volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="e957a-136">Créez le ou les volumes logiques.</span><span class="sxs-lookup"><span data-stu-id="e957a-136">Create the logical volume(s).</span></span> <span data-ttu-id="e957a-137">La commande ci-dessous crée un volume logique appelé `data-lv01` pour couvrir le groupe de volumes entier. Notez qu’il est également possible de créer plusieurs volumes logiques dans le groupe de volumes.</span><span class="sxs-lookup"><span data-stu-id="e957a-137">The command below we will create a single logical volume called `data-lv01` to span the entire volume group, but note that it is also feasible to create multiple logical volumes in the volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="e957a-138">Formater le volume logique</span><span class="sxs-lookup"><span data-stu-id="e957a-138">Format the logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="e957a-139">Avec SLES 11, utilisez `-t ext3` plutôt qu’ext4.</span><span class="sxs-lookup"><span data-stu-id="e957a-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="e957a-140">SLES 11 prend uniquement en charge l’accès en lecture seule aux systèmes de fichiers ext4.</span><span class="sxs-lookup"><span data-stu-id="e957a-140">SLES11 only supports read-only access to ext4 filesystems.</span></span>

## <a name="add-the-new-file-system-to-etcfstab"></a><span data-ttu-id="e957a-141">Ajout du nouveau système de fichiers à /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="e957a-141">Add the new file system to /etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e957a-142">si vous ne modifiez pas correctement le fichier `/etc/fstab`, il se peut que le système ne puisse plus démarrer.</span><span class="sxs-lookup"><span data-stu-id="e957a-142">Improperly editing the `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="e957a-143">En cas de doute, reportez-vous à la documentation de la distribution pour obtenir des informations sur la modification adéquate de ce fichier.</span><span class="sxs-lookup"><span data-stu-id="e957a-143">If unsure, please refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="e957a-144">Il est par ailleurs vivement recommandé de créer une sauvegarde du fichier `/etc/fstab` avant de le modifier.</span><span class="sxs-lookup"><span data-stu-id="e957a-144">It is also recommended that a backup of the `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="e957a-145">Créez le point de montage désiré pour le nouveau système de fichiers. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e957a-145">Create the desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="e957a-146">Trouver le chemin du volume logique</span><span class="sxs-lookup"><span data-stu-id="e957a-146">Locate the logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="e957a-147">Ouvrez `/etc/fstab` dans un éditeur de texte, puis ajoutez une entrée pour le nouveau système de fichiers, par exemple :</span><span class="sxs-lookup"><span data-stu-id="e957a-147">Open `/etc/fstab` in a text editor and add an entry for the new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="e957a-148">Ensuite, enregistrez et fermez `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="e957a-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="e957a-149">Vérifiez si l'entrée `/etc/fstab` est correcte :</span><span class="sxs-lookup"><span data-stu-id="e957a-149">Test that the `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="e957a-150">Si cette commande génère un message d’erreur, vérifiez que la syntaxe utilisée dans le fichier `/etc/fstab` est correcte.</span><span class="sxs-lookup"><span data-stu-id="e957a-150">If this command results in an error message please check the syntax in the `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="e957a-151">Ensuite, exécutez la commande `mount` pour vérifier que le système de fichiers est monté :</span><span class="sxs-lookup"><span data-stu-id="e957a-151">Next run the `mount` command to ensure the file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="e957a-152">(Facultatif) Paramètres de démarrage fiables dans `/etc/fstab`</span><span class="sxs-lookup"><span data-stu-id="e957a-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="e957a-153">De nombreuses distributions comprennent les paramètres de montage `nobootwait` ou `nofail` pouvant être ajoutés au fichier `/etc/fstab`.</span><span class="sxs-lookup"><span data-stu-id="e957a-153">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the `/etc/fstab` file.</span></span> <span data-ttu-id="e957a-154">Ces paramètres autorisent les échecs lors du montage d'un système de fichiers donné et permettent au système Linux de continuer à démarrer même s'il n'a pas été en mesure de monter le système de fichiers RAID.</span><span class="sxs-lookup"><span data-stu-id="e957a-154">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span></span> <span data-ttu-id="e957a-155">Pour plus d'informations sur ces paramètres, reportez-vous à la documentation de votre distribution.</span><span class="sxs-lookup"><span data-stu-id="e957a-155">Please refer to your distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="e957a-156">Exemple (Ubuntu) :</span><span class="sxs-lookup"><span data-stu-id="e957a-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="e957a-157">Prise en charge de TRIM/UNMAP</span><span class="sxs-lookup"><span data-stu-id="e957a-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="e957a-158">Certains noyaux Linux prennent en charge les opérations TRIM/UNMAP pour ignorer les blocs inutilisés sur le disque.</span><span class="sxs-lookup"><span data-stu-id="e957a-158">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="e957a-159">Ces opérations sont particulièrement utiles dans un stockage standard pour informer Azure que des pages supprimées ne sont plus valides et peuvent être ignorées.</span><span class="sxs-lookup"><span data-stu-id="e957a-159">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="e957a-160">Le fait d’ignorer des pages peut vous permettre de réaliser des économies si vous créez des fichiers volumineux, puis les supprimez.</span><span class="sxs-lookup"><span data-stu-id="e957a-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="e957a-161">Il existe deux façons d’activer la prise en charge de TRIM sur votre machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="e957a-161">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="e957a-162">Comme d’habitude, consultez votre distribution pour connaître l’approche recommandée :</span><span class="sxs-lookup"><span data-stu-id="e957a-162">As usual, consult your distribution for the recommended approach:</span></span>

- <span data-ttu-id="e957a-163">Utilisez l’option de montage `discard` dans `/etc/fstab`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="e957a-163">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="e957a-164">Dans certains cas, l’option `discard` peut avoir un impact sur la performance.</span><span class="sxs-lookup"><span data-stu-id="e957a-164">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="e957a-165">Vous pouvez également exécuter la commande `fstrim` manuellement à partir de la ligne de commande ou l’ajouter à votre crontab pour l’exécuter régulièrement :</span><span class="sxs-lookup"><span data-stu-id="e957a-165">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>

    <span data-ttu-id="e957a-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="e957a-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="e957a-167">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="e957a-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
