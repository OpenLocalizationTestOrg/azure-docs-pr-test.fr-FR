---
title: "Configuration logicielle de RAID sur une machine virtuelle exécutant Linux | Microsoft Docs"
description: "Apprenez à utiliser mdadm pour configurer RAID sur Linux dans Azure."
services: virtual-machines-linux
documentationcenter: na
author: rickstercdn
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: f3cb2786-bda6-4d2c-9aaf-2db80f490feb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: rclaus
ms.openlocfilehash: 12f540a700fbf85e579e8aadc9f6def039299ff7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="ce266-103">Configuration d’un RAID logiciel sur Linux</span><span class="sxs-lookup"><span data-stu-id="ce266-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="ce266-104">L'utilisation d'un RAID logiciel pour les machines virtuelles Linux sur Azure est un scénario fréquent afin de regrouper plusieurs disques de données attachés sous la forme d'un périphérique RAID unique.</span><span class="sxs-lookup"><span data-stu-id="ce266-104">It's a common scenario to use software RAID on Linux virtual machines in Azure to present multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="ce266-105">En règle générale, ce scénario permet d'optimiser les performances et d'améliorer le débit par rapport à l'utilisation d'un disque unique.</span><span class="sxs-lookup"><span data-stu-id="ce266-105">Typically this can be used to improve performance and allow for improved throughput compared to using just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="ce266-106">Disques de données attachés</span><span class="sxs-lookup"><span data-stu-id="ce266-106">Attaching data disks</span></span>
<span data-ttu-id="ce266-107">Au moins deux disques de données sont nécessaires pour configurer un périphérique RAID.</span><span class="sxs-lookup"><span data-stu-id="ce266-107">Two or more empty data disks are needed to configure a RAID device.</span></span>  <span data-ttu-id="ce266-108">La raison principale pour la création d’un appareil RAID est d’améliorer les performances de vos E/S de disque.</span><span class="sxs-lookup"><span data-stu-id="ce266-108">The primary reason for creating a RAID device is to improve performance of your disk IO.</span></span>  <span data-ttu-id="ce266-109">En fonction de vos besoins d’E/S, vous pouvez choisir d’attacher des disques qui sont stockés dans notre stockage Standard, avec un maximum de 500 opérations d’E/S par disque ou dans notre stockage Premium avec un maximum de 5 000 opérations d’E/S par disque.</span><span class="sxs-lookup"><span data-stu-id="ce266-109">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span></span> <span data-ttu-id="ce266-110">Cet article n’aborde pas en détail la marche à suivre pour approvisionner et attacher des disques de données sur une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="ce266-110">This article does not go into detail on how to provision and attach data disks to a Linux virtual machine.</span></span>  <span data-ttu-id="ce266-111">Consultez l’article Microsoft Azure [Attacher un disque](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour obtenir des instructions détaillées sur la marche à suivre pour attacher un disque de données vide à une machine virtuelle Linux dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ce266-111">See the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span></span>

## <a name="install-the-mdadm-utility"></a><span data-ttu-id="ce266-112">Installation de l'utilitaire mdadm</span><span class="sxs-lookup"><span data-stu-id="ce266-112">Install the mdadm utility</span></span>
* <span data-ttu-id="ce266-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="ce266-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="ce266-114">**CentOS et Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="ce266-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="ce266-115">**SLES et openSUSE**</span><span class="sxs-lookup"><span data-stu-id="ce266-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-the-disk-partitions"></a><span data-ttu-id="ce266-116">Création des partitions de disque</span><span class="sxs-lookup"><span data-stu-id="ce266-116">Create the disk partitions</span></span>
<span data-ttu-id="ce266-117">Dans cet exemple, nous créons une partition de disque unique sur /dev/sdc.</span><span class="sxs-lookup"><span data-stu-id="ce266-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="ce266-118">La nouvelle partition de disque sera appelée /dev/sdc1.</span><span class="sxs-lookup"><span data-stu-id="ce266-118">The new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="ce266-119">Démarrez `fdisk` pour lancer la création des partitions</span><span class="sxs-lookup"><span data-stu-id="ce266-119">Start `fdisk` to begin creating partitions</span></span>

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide to write them.
    After that, of course, the previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off the mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. <span data-ttu-id="ce266-120">Appuyez sur « n » à l’invite de commandes pour créer un  **n** partition de la nouvelle :</span><span class="sxs-lookup"><span data-stu-id="ce266-120">Press 'n' at the prompt to create a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="ce266-121">Ensuite, appuyez sur « p » à l'invite pour créer une partition **p**rincipale :</span><span class="sxs-lookup"><span data-stu-id="ce266-121">Next, press 'p' to create a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="ce266-122">Appuyez sur « 1 » pour sélectionner la partition numéro 1 :</span><span class="sxs-lookup"><span data-stu-id="ce266-122">Press '1' to select partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="ce266-123">Sélectionnez le point de départ de la nouvelle partition ou appuyez sur `<enter>` pour accepter le paramètre par défaut et placer la partition au début de l’espace libre sur le disque :</span><span class="sxs-lookup"><span data-stu-id="ce266-123">Select the starting point of the new partition, or press `<enter>` to accept the default to place the partition at the beginning of the free space on the drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="ce266-124">Sélectionnez la taille de la partition. Par exemple, tapez « +10G » pour créer une partition de 10 Go.</span><span class="sxs-lookup"><span data-stu-id="ce266-124">Select the size of the partition, for example type '+10G' to create a 10 gigabyte partition.</span></span> <span data-ttu-id="ce266-125">Vous pouvez aussi appuyer sur `<enter>` pour créer une seule partition pour l’intégralité du disque :</span><span class="sxs-lookup"><span data-stu-id="ce266-125">Or, press `<enter>` create a single partition that spans the entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="ce266-126">Ensuite, remplacez l'ID et le **t**ype de partition de l'ID par défaut « 83 » (Linux) par l'ID « fd » (raid auto Linux) :</span><span class="sxs-lookup"><span data-stu-id="ce266-126">Next, change the ID and **t**ype of the partition from the default ID '83' (Linux) to ID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L to list codes): fd
    ```

8. <span data-ttu-id="ce266-127">Enfin, écrivez la table de partition sur le disque et quittez fdisk :</span><span class="sxs-lookup"><span data-stu-id="ce266-127">Finally, write the partition table to the drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    The partition table has been altered!
    ```

## <a name="create-the-raid-array"></a><span data-ttu-id="ce266-128">Création du contrôleur RAID</span><span class="sxs-lookup"><span data-stu-id="ce266-128">Create the RAID array</span></span>
1. <span data-ttu-id="ce266-129">L’exemple suivant permet de créer un volume agrégé par bandes (RAID 0) de trois partitions sur trois disques de données distincts (sdc1, sdd1, sde1).</span><span class="sxs-lookup"><span data-stu-id="ce266-129">The following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="ce266-130">Après l’exécution de cette commande, un nouveau périphérique RAID dénommé **/dev/md127** est créé.</span><span class="sxs-lookup"><span data-stu-id="ce266-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="ce266-131">Notez que si les disques de données précédemment utilisés font partie d’un autre contrôleur RAID qui n’existe plus, il peut s'avérer nécessaire d’ajouter le paramètre `--force` à la commande `mdadm`.</span><span class="sxs-lookup"><span data-stu-id="ce266-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary to add the `--force` parameter to the `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="ce266-132">Créez le système de fichiers sur le nouveau périphérique RAID.</span><span class="sxs-lookup"><span data-stu-id="ce266-132">Create the file system on the new RAID device</span></span>
   
    <span data-ttu-id="ce266-133">a.</span><span class="sxs-lookup"><span data-stu-id="ce266-133">a.</span></span> <span data-ttu-id="ce266-134">**CentOS, Oracle Linux, SLES 12, openSUSE et Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="ce266-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="ce266-135">b.</span><span class="sxs-lookup"><span data-stu-id="ce266-135">b.</span></span> <span data-ttu-id="ce266-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="ce266-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="ce266-137">c.</span><span class="sxs-lookup"><span data-stu-id="ce266-137">c.</span></span> <span data-ttu-id="ce266-138">**SLES 11** : activez boot.md et créez mdadm.conf</span><span class="sxs-lookup"><span data-stu-id="ce266-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="ce266-139">Un redémarrage peut être nécessaire après avoir apporté ces modifications sur des systèmes SUSE.</span><span class="sxs-lookup"><span data-stu-id="ce266-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="ce266-140">Cette étape n’est *pas* requise pour SLES 12.</span><span class="sxs-lookup"><span data-stu-id="ce266-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-the-new-file-system-to-etcfstab"></a><span data-ttu-id="ce266-141">Ajout du nouveau système de fichiers à /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="ce266-141">Add the new file system to /etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ce266-142">si vous ne modifiez pas correctement le fichier /etc/fstab, il se peut que le système ne puisse plus démarrer.</span><span class="sxs-lookup"><span data-stu-id="ce266-142">Improperly editing the /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="ce266-143">En cas de doute, reportez-vous à la documentation de la distribution pour obtenir des informations sur la modification adéquate de ce fichier.</span><span class="sxs-lookup"><span data-stu-id="ce266-143">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="ce266-144">Il est par ailleurs vivement recommandé de créer une sauvegarde du fichier /etc/fstab avant de le modifier.</span><span class="sxs-lookup"><span data-stu-id="ce266-144">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="ce266-145">Créez le point de montage désiré pour le nouveau système de fichiers. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ce266-145">Create the desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="ce266-146">Lors de la modification du fichier /etc/fstab, l' **identificateur unique universel** doit être utilisé pour faire référence au système de fichiers plutôt qu'au nom de périphérique.</span><span class="sxs-lookup"><span data-stu-id="ce266-146">When editing /etc/fstab, the **UUID** should be used to reference the file system rather than the device name.</span></span>  <span data-ttu-id="ce266-147">Servez-vous de l'utilitaire `blkid` pour déterminer l'identificateur unique universel (UUID) du nouveau système de fichiers :</span><span class="sxs-lookup"><span data-stu-id="ce266-147">Use the `blkid` utility to determine the UUID for the new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="ce266-148">Ouvrez /etc/fstab dans un éditeur de texte, puis ajoutez une entrée pour le nouveau système de fichiers, par exemple :</span><span class="sxs-lookup"><span data-stu-id="ce266-148">Open /etc/fstab in a text editor and add an entry for the new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="ce266-149">Ou sur **SLES 11** :</span><span class="sxs-lookup"><span data-stu-id="ce266-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="ce266-150">Ensuite, enregistrez et fermez /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="ce266-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="ce266-151">Vérifiez si l'entrée /etc/fstab est correcte :</span><span class="sxs-lookup"><span data-stu-id="ce266-151">Test that the /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="ce266-152">Si cette commande génère un message d’erreur, vérifiez que la syntaxe utilisée dans le fichier /etc/fstab est correcte.</span><span class="sxs-lookup"><span data-stu-id="ce266-152">If this command results in an error message, please check the syntax in the /etc/fstab file.</span></span>
   
    <span data-ttu-id="ce266-153">Ensuite, exécutez la commande `mount` pour vérifier que le système de fichiers est monté :</span><span class="sxs-lookup"><span data-stu-id="ce266-153">Next run the `mount` command to ensure the file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="ce266-154">(Facultatif) Paramètres de démarrage fiables</span><span class="sxs-lookup"><span data-stu-id="ce266-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="ce266-155">**Configuration fstab**</span><span class="sxs-lookup"><span data-stu-id="ce266-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="ce266-156">De nombreuses distributions comprennent les paramètres de montage `nobootwait` ou `nofail` pouvant être ajoutés au fichier /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="ce266-156">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the /etc/fstab file.</span></span> <span data-ttu-id="ce266-157">Ces paramètres autorisent les échecs lors du montage d'un système de fichiers donné et permettent au système Linux de continuer à démarrer même s'il n'a pas été en mesure de monter le système de fichiers RAID.</span><span class="sxs-lookup"><span data-stu-id="ce266-157">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span></span> <span data-ttu-id="ce266-158">Pour plus d’informations sur ces paramètres, reportez-vous à la documentation de votre distribution.</span><span class="sxs-lookup"><span data-stu-id="ce266-158">Refer to your distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="ce266-159">Exemple (Ubuntu) :</span><span class="sxs-lookup"><span data-stu-id="ce266-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="ce266-160">**Paramètres de démarrage Linux**</span><span class="sxs-lookup"><span data-stu-id="ce266-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="ce266-161">En plus des paramètres ci-dessus, le paramètre de noyau «`bootdegraded=true`» peut permettre au système de démarrer, même si le RAID est identifié comme endommagé ou détérioré, par exemple si un disque de données est supprimé par inadvertance de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ce266-161">In addition to the above parameters, the kernel parameter "`bootdegraded=true`" can allow the system to boot even if the RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from the virtual machine.</span></span> <span data-ttu-id="ce266-162">Par défaut, cette situation peut également rendre impossible le démarrage du système.</span><span class="sxs-lookup"><span data-stu-id="ce266-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="ce266-163">Pour plus d'informations sur la modification adéquate des paramètres de noyau, reportez-vous à la documentation de votre distribution.</span><span class="sxs-lookup"><span data-stu-id="ce266-163">Please refer to your distribution's documentation on how to properly edit kernel parameters.</span></span> <span data-ttu-id="ce266-164">Par exemple, dans de nombreuses distributions (CentOS, Oracle Linux, SLES 11), ces paramètres peuvent être ajoutés manuellement au fichier «`/boot/grub/menu.lst`».</span><span class="sxs-lookup"><span data-stu-id="ce266-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually to the "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="ce266-165">Sur Ubuntu, ce paramètre peut être ajouté à la variable `GRUB_CMDLINE_LINUX_DEFAULT` dans « /etc/default/grub ».</span><span class="sxs-lookup"><span data-stu-id="ce266-165">On Ubuntu this parameter can be added to the `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="ce266-166">Prise en charge de TRIM/UNMAP</span><span class="sxs-lookup"><span data-stu-id="ce266-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="ce266-167">Certains noyaux Linux prennent en charge les opérations TRIM/UNMAP pour ignorer les blocs inutilisés sur le disque.</span><span class="sxs-lookup"><span data-stu-id="ce266-167">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="ce266-168">Ces opérations sont particulièrement utiles dans un stockage standard pour informer Azure que des pages supprimées ne sont plus valides et peuvent être ignorées.</span><span class="sxs-lookup"><span data-stu-id="ce266-168">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="ce266-169">Le fait d’ignorer des pages peut vous permettre de réaliser des économies si vous créez des fichiers volumineux, puis les supprimez.</span><span class="sxs-lookup"><span data-stu-id="ce266-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="ce266-170">RAID ne peut pas émettre de commandes Ignorer si la taille de segment de tableau est inférieure à la valeur par défaut (512 Ko).</span><span class="sxs-lookup"><span data-stu-id="ce266-170">RAID may not issue discard commands if the chunk size for the array is set to less than the default (512KB).</span></span> <span data-ttu-id="ce266-171">La raison en est que la granularité d’annulation de mappage sur l’ordinateur hôte est également de 512 Ko.</span><span class="sxs-lookup"><span data-stu-id="ce266-171">This is because the unmap granularity on the Host is also 512KB.</span></span> <span data-ttu-id="ce266-172">Si vous avez modifié la taille de segment du tableau par l’intermédiaire du paramètre `--chunk=` de mdadm, les demandes TRIM ou d’annulation de mappage peuvent être ignorées par le noyau.</span><span class="sxs-lookup"><span data-stu-id="ce266-172">If you modified the array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by the kernel.</span></span>

<span data-ttu-id="ce266-173">Il existe deux façons d’activer la prise en charge de TRIM sur votre machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="ce266-173">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="ce266-174">Comme d’habitude, consultez votre distribution pour connaître l’approche recommandée :</span><span class="sxs-lookup"><span data-stu-id="ce266-174">As usual, consult your distribution for the recommended approach:</span></span>

- <span data-ttu-id="ce266-175">Utilisez l’option de montage `discard` dans `/etc/fstab`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="ce266-175">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="ce266-176">Dans certains cas, l’option `discard` peut avoir un impact sur la performance.</span><span class="sxs-lookup"><span data-stu-id="ce266-176">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="ce266-177">Vous pouvez également exécuter la commande `fstrim` manuellement à partir de la ligne de commande ou l’ajouter à votre crontab pour l’exécuter régulièrement :</span><span class="sxs-lookup"><span data-stu-id="ce266-177">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>

    <span data-ttu-id="ce266-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="ce266-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="ce266-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="ce266-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
