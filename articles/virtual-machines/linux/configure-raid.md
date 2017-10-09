---
title: "aaaConfigure les volumes RAID logiciels sur un ordinateur virtuel exécutant Linux | Documents Microsoft"
description: "Découvrez comment toouse mdadm tooconfigure RAID sur Linux dans Azure."
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
ms.openlocfilehash: f06e2679d953faf88ffee9991226cdb3cc1cbdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="b6d64-103">Configuration d’un RAID logiciel sur Linux</span><span class="sxs-lookup"><span data-stu-id="b6d64-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="b6d64-104">Il est un commun scénario toouse les volumes RAID logiciels sur les ordinateurs virtuels Linux dans Azure toopresent données jointes plusieurs disques comme un périphérique RAID unique.</span><span class="sxs-lookup"><span data-stu-id="b6d64-104">It's a common scenario toouse software RAID on Linux virtual machines in Azure toopresent multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="b6d64-105">Cela vous pouvez généralement les performances tooimprove utilisé et autoriser pour améliorée débit comparées toousing un seul disque.</span><span class="sxs-lookup"><span data-stu-id="b6d64-105">Typically this can be used tooimprove performance and allow for improved throughput compared toousing just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="b6d64-106">Disques de données attachés</span><span class="sxs-lookup"><span data-stu-id="b6d64-106">Attaching data disks</span></span>
<span data-ttu-id="b6d64-107">Deux ou plusieurs disques de données vides sont nécessaire tooconfigure un périphérique RAID.</span><span class="sxs-lookup"><span data-stu-id="b6d64-107">Two or more empty data disks are needed tooconfigure a RAID device.</span></span>  <span data-ttu-id="b6d64-108">Hello principal motif de création d’un périphérique RAID est tooimprove les performances de votre disque e/s.</span><span class="sxs-lookup"><span data-stu-id="b6d64-108">hello primary reason for creating a RAID device is tooimprove performance of your disk IO.</span></span>  <span data-ttu-id="b6d64-109">Selon vos besoins d’e/s, vous pouvez choisir les disques tooattach qui sont stockées dans notre stockage Standard, avec des e/s de too500/ps par le stockage sur disque ou notre Premium avec des e/s de too5000/ps par disque.</span><span class="sxs-lookup"><span data-stu-id="b6d64-109">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="b6d64-110">Cet article n’aborde pas de détails sur la façon de tooprovision et attacher une machine virtuelle Linux données disques tooa.</span><span class="sxs-lookup"><span data-stu-id="b6d64-110">This article does not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span>  <span data-ttu-id="b6d64-111">Consultez l’article de Microsoft Azure hello [attacher un disque](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour obtenir des instructions détaillées sur tooattach un vide de données de disque virtuels tooa Linux sur Azure.</span><span class="sxs-lookup"><span data-stu-id="b6d64-111">See hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-mdadm-utility"></a><span data-ttu-id="b6d64-112">Installer l’utilitaire de mdadm hello</span><span class="sxs-lookup"><span data-stu-id="b6d64-112">Install hello mdadm utility</span></span>
* <span data-ttu-id="b6d64-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="b6d64-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="b6d64-114">**CentOS et Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="b6d64-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="b6d64-115">**SLES et openSUSE**</span><span class="sxs-lookup"><span data-stu-id="b6d64-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a><span data-ttu-id="b6d64-116">Créer des partitions de disque hello</span><span class="sxs-lookup"><span data-stu-id="b6d64-116">Create hello disk partitions</span></span>
<span data-ttu-id="b6d64-117">Dans cet exemple, nous créons une partition de disque unique sur /dev/sdc.</span><span class="sxs-lookup"><span data-stu-id="b6d64-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="b6d64-118">nouvelle partition de disque Hello sera appelée /dev/sdc1.</span><span class="sxs-lookup"><span data-stu-id="b6d64-118">hello new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="b6d64-119">Démarrer `fdisk` toobegin création de partitions</span><span class="sxs-lookup"><span data-stu-id="b6d64-119">Start `fdisk` toobegin creating partitions</span></span>

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide toowrite them.
    After that, of course, hello previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off hello mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. <span data-ttu-id="b6d64-120">Appuyez sur « n » à toocreate d’invite de commandes hello un  **n** partition de la nouvelle :</span><span class="sxs-lookup"><span data-stu-id="b6d64-120">Press 'n' at hello prompt toocreate a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="b6d64-121">Ensuite, appuyez sur « p » toocreate un **p**rincipal partition :</span><span class="sxs-lookup"><span data-stu-id="b6d64-121">Next, press 'p' toocreate a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="b6d64-122">Appuyez sur le numéro de partition '1' tooselect 1 :</span><span class="sxs-lookup"><span data-stu-id="b6d64-122">Press '1' tooselect partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="b6d64-123">Sélectionnez hello point de départ de la partition hello, ou appuyez sur `<enter>` partition tooaccept hello par défaut tooplace hello au début de hello d’espace disque de hello hello :</span><span class="sxs-lookup"><span data-stu-id="b6d64-123">Select hello starting point of hello new partition, or press `<enter>` tooaccept hello default tooplace hello partition at hello beginning of hello free space on hello drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="b6d64-124">Sélectionnez la taille de partition hello, par exemple le type '+10G' toocreate une partition de 10 gigaoctets hello.</span><span class="sxs-lookup"><span data-stu-id="b6d64-124">Select hello size of hello partition, for example type '+10G' toocreate a 10 gigabyte partition.</span></span> <span data-ttu-id="b6d64-125">Ou bien, appuyez sur `<enter>` créer une seule partition qui couvre l’intégralité du lecteur hello :</span><span class="sxs-lookup"><span data-stu-id="b6d64-125">Or, press `<enter>` create a single partition that spans hello entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="b6d64-126">Ensuite, modifiez les ID hello et **t**ype de partition hello à partir de la valeur par défaut hello ID '83' (Linux) tooID 'fd' (Linux raid auto) :</span><span class="sxs-lookup"><span data-stu-id="b6d64-126">Next, change hello ID and **t**ype of hello partition from hello default ID '83' (Linux) tooID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. <span data-ttu-id="b6d64-127">Enfin, écrire le lecteur de toohello de table de partition hello et quitter fdisk :</span><span class="sxs-lookup"><span data-stu-id="b6d64-127">Finally, write hello partition table toohello drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a><span data-ttu-id="b6d64-128">Création de disques RAID hello</span><span class="sxs-lookup"><span data-stu-id="b6d64-128">Create hello RAID array</span></span>
1. <span data-ttu-id="b6d64-129">Hello suivant va de l’exemple « bandes » (RAID de niveau 0) trois partitions situées sur trois disques de données distinct (sdc1, sdd1, sde1).</span><span class="sxs-lookup"><span data-stu-id="b6d64-129">hello following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="b6d64-130">Après l’exécution de cette commande, un nouveau périphérique RAID dénommé **/dev/md127** est créé.</span><span class="sxs-lookup"><span data-stu-id="b6d64-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="b6d64-131">Notez également que si ces données disques nous précédemment partie d’un autre tableau RAID obsolète il peut être nécessaire de tooadd hello `--force` paramètre toohello `mdadm` commande :</span><span class="sxs-lookup"><span data-stu-id="b6d64-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary tooadd hello `--force` parameter toohello `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="b6d64-132">Créer un système de fichiers hello sur un périphérique RAID nouvelle hello</span><span class="sxs-lookup"><span data-stu-id="b6d64-132">Create hello file system on hello new RAID device</span></span>
   
    <span data-ttu-id="b6d64-133">a.</span><span class="sxs-lookup"><span data-stu-id="b6d64-133">a.</span></span> <span data-ttu-id="b6d64-134">**CentOS, Oracle Linux, SLES 12, openSUSE et Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="b6d64-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="b6d64-135">b.</span><span class="sxs-lookup"><span data-stu-id="b6d64-135">b.</span></span> <span data-ttu-id="b6d64-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="b6d64-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="b6d64-137">c.</span><span class="sxs-lookup"><span data-stu-id="b6d64-137">c.</span></span> <span data-ttu-id="b6d64-138">**SLES 11** : activez boot.md et créez mdadm.conf</span><span class="sxs-lookup"><span data-stu-id="b6d64-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="b6d64-139">Un redémarrage peut être nécessaire après avoir apporté ces modifications sur des systèmes SUSE.</span><span class="sxs-lookup"><span data-stu-id="b6d64-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="b6d64-140">Cette étape n’est *pas* requise pour SLES 12.</span><span class="sxs-lookup"><span data-stu-id="b6d64-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="b6d64-141">Ajouter hello nouveau fichier système trop/etc/fstab</span><span class="sxs-lookup"><span data-stu-id="b6d64-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b6d64-142">Modification incorrecte de fichier/etc/fstab de hello peut entraîner un système non démarrable.</span><span class="sxs-lookup"><span data-stu-id="b6d64-142">Improperly editing hello /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="b6d64-143">En cas de doute, consultez la documentation de la distribution toohello pour plus d’informations sur la façon dont tooproperly modifier ce fichier.</span><span class="sxs-lookup"><span data-stu-id="b6d64-143">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="b6d64-144">Il est également recommandé qu’une sauvegarde de fichier/etc/fstab de hello est créée avant la modification.</span><span class="sxs-lookup"><span data-stu-id="b6d64-144">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="b6d64-145">Créez le point de montage hello souhaité pour votre nouveau système de fichiers, par exemple :</span><span class="sxs-lookup"><span data-stu-id="b6d64-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="b6d64-146">Lorsque vous modifiez/etc/fstab, hello **UUID** doit être utilisé tooreference hello système plutôt que hello appareil nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="b6d64-146">When editing /etc/fstab, hello **UUID** should be used tooreference hello file system rather than hello device name.</span></span>  <span data-ttu-id="b6d64-147">Hello d’utilisation `blkid` hello de toodetermine utilitaire UUID hello nouveau système de fichiers :</span><span class="sxs-lookup"><span data-stu-id="b6d64-147">Use hello `blkid` utility toodetermine hello UUID for hello new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="b6d64-148">Ouvrez/etc/fstab dans un éditeur de texte et ajoutez une entrée pour le nouveau système de fichiers hello, par exemple :</span><span class="sxs-lookup"><span data-stu-id="b6d64-148">Open /etc/fstab in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="b6d64-149">Ou sur **SLES 11** :</span><span class="sxs-lookup"><span data-stu-id="b6d64-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="b6d64-150">Ensuite, enregistrez et fermez /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="b6d64-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="b6d64-151">Tester que hello/etc/fstab entrée est correcte :</span><span class="sxs-lookup"><span data-stu-id="b6d64-151">Test that hello /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="b6d64-152">Si cette commande renvoie un message d’erreur, vérifiez la syntaxe hello dans le fichier/etc/fstab de hello.</span><span class="sxs-lookup"><span data-stu-id="b6d64-152">If this command results in an error message, please check hello syntax in hello /etc/fstab file.</span></span>
   
    <span data-ttu-id="b6d64-153">Prochaine exécution hello `mount` système de fichiers de commandes tooensure hello est monté :</span><span class="sxs-lookup"><span data-stu-id="b6d64-153">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="b6d64-154">(Facultatif) Paramètres de démarrage fiables</span><span class="sxs-lookup"><span data-stu-id="b6d64-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="b6d64-155">**Configuration fstab**</span><span class="sxs-lookup"><span data-stu-id="b6d64-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="b6d64-156">Nombre de distributions inclure soit hello `nobootwait` ou `nofail` monter des paramètres qui peuvent être ajoutés à un fichier fstab toohello/etc /.</span><span class="sxs-lookup"><span data-stu-id="b6d64-156">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello /etc/fstab file.</span></span> <span data-ttu-id="b6d64-157">Ces paramètres permettent échecs lors du montage d’un système de fichiers particulier et autoriser hello Linux système toocontinue tooboot même s’il est impossible de tooproperly montage hello RAID.</span><span class="sxs-lookup"><span data-stu-id="b6d64-157">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="b6d64-158">Pour plus d’informations sur ces paramètres, consultez la documentation de la distribution tooyour.</span><span class="sxs-lookup"><span data-stu-id="b6d64-158">Refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="b6d64-159">Exemple (Ubuntu) :</span><span class="sxs-lookup"><span data-stu-id="b6d64-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="b6d64-160">**Paramètres de démarrage Linux**</span><span class="sxs-lookup"><span data-stu-id="b6d64-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="b6d64-161">Dans toohello ajout au-dessus de paramètres, hello au paramètre de noyau «`bootdegraded=true`» peut autoriser hello système tooboot même si hello RAID est perçu comme endommagé ou détérioré, par exemple, si un lecteur de données est supprimé par inadvertance de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="b6d64-161">In addition toohello above parameters, hello kernel parameter "`bootdegraded=true`" can allow hello system tooboot even if hello RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from hello virtual machine.</span></span> <span data-ttu-id="b6d64-162">Par défaut, cette situation peut également rendre impossible le démarrage du système.</span><span class="sxs-lookup"><span data-stu-id="b6d64-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="b6d64-163">Consultez la documentation de la distribution tooyour sur comment tooproperly modifier les paramètres de noyau.</span><span class="sxs-lookup"><span data-stu-id="b6d64-163">Please refer tooyour distribution's documentation on how tooproperly edit kernel parameters.</span></span> <span data-ttu-id="b6d64-164">Par exemple, dans de nombreuses distributions (CentOS, Oracle Linux SLES et 11), ces paramètres peuvent être ajoutés manuellement toohello «`/boot/grub/menu.lst`« fichier.</span><span class="sxs-lookup"><span data-stu-id="b6d64-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually toohello "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="b6d64-165">Sur Ubuntu ce paramètre peut être ajouté à toohello `GRUB_CMDLINE_LINUX_DEFAULT` variable sur « / etc/par défaut/grub ».</span><span class="sxs-lookup"><span data-stu-id="b6d64-165">On Ubuntu this parameter can be added toohello `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="b6d64-166">Prise en charge de TRIM/UNMAP</span><span class="sxs-lookup"><span data-stu-id="b6d64-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="b6d64-167">Certains noyaux Linux prend en charge TRIM/annuler le mappage operations toodiscard les blocs inutilisés sur le disque de hello.</span><span class="sxs-lookup"><span data-stu-id="b6d64-167">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="b6d64-168">Ces opérations sont principalement dans tooinform standard de stockage Azure qui pages supprimées ne sont plus valides et peuvent être ignorées.</span><span class="sxs-lookup"><span data-stu-id="b6d64-168">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="b6d64-169">Le fait d’ignorer des pages peut vous permettre de réaliser des économies si vous créez des fichiers volumineux, puis les supprimez.</span><span class="sxs-lookup"><span data-stu-id="b6d64-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="b6d64-170">RAID ne peut pas émettre des commandes de rejet si la taille de segment de hello pour le tableau de hello a la valeur accessible sans que la valeur par défaut de hello (512 Ko).</span><span class="sxs-lookup"><span data-stu-id="b6d64-170">RAID may not issue discard commands if hello chunk size for hello array is set tooless than hello default (512KB).</span></span> <span data-ttu-id="b6d64-171">C’est parce que hello annuler le mappage granularité sur hello hôte est également de 512 Ko.</span><span class="sxs-lookup"><span data-stu-id="b6d64-171">This is because hello unmap granularity on hello Host is also 512KB.</span></span> <span data-ttu-id="b6d64-172">Si vous avez modifié le taille de segment du tableau hello par le biais de mdadm `--chunk=` paramètre, puis les demandes/annuler le mappage de découpage peuvent être ignoré par le noyau de hello.</span><span class="sxs-lookup"><span data-stu-id="b6d64-172">If you modified hello array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by hello kernel.</span></span>

<span data-ttu-id="b6d64-173">Il existe deux façons tooenable TRIM prend en charge dans votre VM Linux.</span><span class="sxs-lookup"><span data-stu-id="b6d64-173">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="b6d64-174">Comme d’habitude, consultez votre distribution pour hello approche recommandée :</span><span class="sxs-lookup"><span data-stu-id="b6d64-174">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="b6d64-175">Hello d’utilisation `discard` monter option dans `/etc/fstab`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="b6d64-175">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="b6d64-176">Dans certains hello cas `discard` option peut avoir des conséquences sur les performances.</span><span class="sxs-lookup"><span data-stu-id="b6d64-176">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="b6d64-177">Vous pouvez également exécuter hello `fstrim` commande manuellement à partir de la ligne de commande hello ou ajoutez-le tooyour crontab toorun régulièrement :</span><span class="sxs-lookup"><span data-stu-id="b6d64-177">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="b6d64-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="b6d64-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="b6d64-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="b6d64-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
