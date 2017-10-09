---
title: aaaAttach un tooa disque VM Linux dans Azure | Documents Microsoft
description: "En savoir tooattach données tooa Linux VM de disque à l’aide de déploiement classique de hello modéliser et initialiser le disque de hello par conséquent, il est prêt à être utilisé"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a><span data-ttu-id="6b84b-103">Comment tooAttach un tooa de disque de données Machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="6b84b-103">How tooAttach a Data Disk tooa Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="6b84b-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6b84b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6b84b-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="6b84b-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="6b84b-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="6b84b-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="6b84b-107">Consultez Comment trop[attacher un disque de données à l’aide du modèle de déploiement du Gestionnaire de ressources hello](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6b84b-107">See how too[attach a data disk using hello Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="6b84b-108">Vous pouvez attacher les disques vides et les disques qui contiennent des données tooyour machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="6b84b-108">You can attach both empty disks and disks that contain data tooyour Azure VMs.</span></span> <span data-ttu-id="6b84b-109">Les deux types de disques sont des fichiers .vhd conservés dans un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="6b84b-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="6b84b-110">Comme avec l’ajout d’un ordinateur Linux de tooa de disque, après avoir attaché le disque de hello vous devez tooinitialize et mettre en forme par conséquent, il est prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="6b84b-110">As with adding any disk tooa Linux machine, after you attach hello disk you need tooinitialize and format it so it's ready for use.</span></span> <span data-ttu-id="6b84b-111">Cet article explique l’attachement de disques vides et les disques contenant déjà des données tooyour machines virtuelles, ainsi que la manière dont toothen initialiser et formater un nouveau disque.</span><span class="sxs-lookup"><span data-stu-id="6b84b-111">This article details attaching both empty disks and disks already containing data tooyour VMs, as well as how toothen initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="6b84b-112">Il s’agit d’une meilleure toouse de pratique une ou plusieurs séparés toostore de disques, les données d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="6b84b-112">It's a best practice toouse one or more separate disks toostore a virtual machine's data.</span></span> <span data-ttu-id="6b84b-113">Lorsque vous créez une machine virtuelle Azure, celle-ci possède un disque de système d'exploitation et un disque temporaire.</span><span class="sxs-lookup"><span data-stu-id="6b84b-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="6b84b-114">**N’utilisez pas hello disque temporaire toostore persistants de données.**</span><span class="sxs-lookup"><span data-stu-id="6b84b-114">**Do not use hello temporary disk toostore persistent data.**</span></span> <span data-ttu-id="6b84b-115">Hello nom l’indique, il fournit un stockage temporaire uniquement.</span><span class="sxs-lookup"><span data-stu-id="6b84b-115">As hello name implies, it provides temporary storage only.</span></span> <span data-ttu-id="6b84b-116">Il n'offre aucune possibilité de redondance ou de sauvegarde, car il ne réside pas dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="6b84b-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="6b84b-117">disque temporaire de Hello est généralement gérée par hello Linux Agent Azure et automatiquement monté trop**/mnt/resource** (ou **/mnt** sur Ubuntu images).</span><span class="sxs-lookup"><span data-stu-id="6b84b-117">hello temporary disk is typically managed by hello Azure Linux Agent and automatically mounted too**/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="6b84b-118">Sur hello autre part, un disque de données peut être nommé par le noyau Linux de hello quelque chose comme `/dev/sdc`, et vous devez toopartition, mettre en forme et monter cette ressource.</span><span class="sxs-lookup"><span data-stu-id="6b84b-118">On hello other hand, a data disk might be named by hello Linux kernel something like `/dev/sdc`, and you need toopartition, format, and mount this resource.</span></span> <span data-ttu-id="6b84b-119">Consultez hello [Guide de l’utilisateur l’Agent Linux Azure] [ Agent] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="6b84b-119">See hello [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="6b84b-120">Initialisation d’un nouveau disque de données sous Linux</span><span class="sxs-lookup"><span data-stu-id="6b84b-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="6b84b-121">SSH tooyour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6b84b-121">SSH tooyour VM.</span></span> <span data-ttu-id="6b84b-122">Pour plus d’informations, consultez [comment toolog sur l’ordinateur virtuel de tooa exécutant Linux][Logon].</span><span class="sxs-lookup"><span data-stu-id="6b84b-122">For more information, see [How toolog on tooa virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="6b84b-123">Ensuite, vous devez identificateur de l’appareil toofind hello pour tooinitialize de disque de données hello.</span><span class="sxs-lookup"><span data-stu-id="6b84b-123">Next you need toofind hello device identifier for hello data disk tooinitialize.</span></span> <span data-ttu-id="6b84b-124">Il existe deux façons toodo qui :</span><span class="sxs-lookup"><span data-stu-id="6b84b-124">There are two ways toodo that:</span></span>
   
    <span data-ttu-id="6b84b-125">a) Grep pour les périphériques SCSI Bonjour ouvre une session, comme dans hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6b84b-125">a) Grep for SCSI devices in hello logs, such as in hello following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="6b84b-126">Pour les distributions Ubuntu récent, vous devrez peut-être toouse `sudo grep SCSI /var/log/syslog` car l’enregistrement trop`/var/log/messages` peuvent être désactivés par défaut.</span><span class="sxs-lookup"><span data-stu-id="6b84b-126">For recent Ubuntu distributions, you may need toouse `sudo grep SCSI /var/log/syslog` because logging too`/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="6b84b-127">Vous trouverez l’identificateur hello hello dernière du disque de données qui a été ajoutée dans les messages de type hello qui sont affichés.</span><span class="sxs-lookup"><span data-stu-id="6b84b-127">You can find hello identifier of hello last data disk that was added in hello messages that are displayed.</span></span>
   
    ![Obtenir les messages de disque hello](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="6b84b-129">OU</span><span class="sxs-lookup"><span data-stu-id="6b84b-129">OR</span></span>
   
    <span data-ttu-id="6b84b-130">b) hello d’utilisation `lsscsi` toofind de commande des id de périphérique hello. `lsscsi` peuvent être installées par soit `yum install lsscsi` (base de distributions sur Red Hat) ou `apt-get install lsscsi` (base de distributions sur Debian).</span><span class="sxs-lookup"><span data-stu-id="6b84b-130">b) Use hello `lsscsi` command toofind out hello device id. `lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="6b84b-131">Vous pouvez trouver de disque de hello recherchée par son *lun* ou **numéro d’unité logique**.</span><span class="sxs-lookup"><span data-stu-id="6b84b-131">You can find hello disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="6b84b-132">Par exemple, hello *lun* pour hello disques vous pouvant facilement visible à partir de `azure vm disk list <virtual-machine>` en tant que :</span><span class="sxs-lookup"><span data-stu-id="6b84b-132">For example, hello *lun* for hello disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="6b84b-133">sortie de Hello est similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="6b84b-133">hello output is similar toohello following:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    <span data-ttu-id="6b84b-134">Comparer ces données avec une sortie hello de `lsscsi` pour hello les mêmes exemples de machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="6b84b-134">Compare this data with hello output of `lsscsi` for hello same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="6b84b-135">dernier numéro de tuple hello dans chaque ligne Hello est hello *lun*.</span><span class="sxs-lookup"><span data-stu-id="6b84b-135">hello last number in hello tuple in each row is hello *lun*.</span></span> <span data-ttu-id="6b84b-136">Pour plus d'informations, consultez `man lsscsi` .</span><span class="sxs-lookup"><span data-stu-id="6b84b-136">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="6b84b-137">À l’invite de hello, tapez ce qui suit hello commande toocreate votre appareil :</span><span class="sxs-lookup"><span data-stu-id="6b84b-137">At hello prompt, type hello following command toocreate your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="6b84b-138">Lorsque vous y êtes invité, tapez  **n**  toocreate une partition.</span><span class="sxs-lookup"><span data-stu-id="6b84b-138">When prompted, type **n** toocreate a partition.</span></span>

    ![Créer un appareil](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="6b84b-140">Lorsque vous y êtes invité, tapez **p** partition principale pour toomake hello partition hello.</span><span class="sxs-lookup"><span data-stu-id="6b84b-140">When prompted, type **p** toomake hello partition hello primary partition.</span></span> <span data-ttu-id="6b84b-141">Type **1** toomake il hello première partition et tapez indiquez tooaccept hello valeur par défaut cylindre de hello.</span><span class="sxs-lookup"><span data-stu-id="6b84b-141">Type **1** toomake it hello first partition, and then type enter tooaccept hello default value for hello cylinder.</span></span> <span data-ttu-id="6b84b-142">Sur certains systèmes, il peut afficher les valeurs par défaut hello hello premier et hello dernier secteurs, au lieu de cylindre de hello.</span><span class="sxs-lookup"><span data-stu-id="6b84b-142">On some systems, it can show hello default values of hello first and hello last sectors, instead of hello cylinder.</span></span> <span data-ttu-id="6b84b-143">Vous pouvez choisir tooaccept ces valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="6b84b-143">You can choose tooaccept these defaults.</span></span>

    ![Créer une partition](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="6b84b-145">Type **p** toosee hello plus d’informations sur disque de hello est partitionné.</span><span class="sxs-lookup"><span data-stu-id="6b84b-145">Type **p** toosee hello details about hello disk that is being partitioned.</span></span>

    ![Répertorier les informations sur le disque](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="6b84b-147">Type **w** toowrite les paramètres de hello pour le disque de hello.</span><span class="sxs-lookup"><span data-stu-id="6b84b-147">Type **w** toowrite hello settings for hello disk.</span></span>

    ![Écrire les modifications de disque hello](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="6b84b-149">Maintenant, vous pouvez créer des système de fichiers hello sur la nouvelle partition de hello.</span><span class="sxs-lookup"><span data-stu-id="6b84b-149">Now you can create hello file system on hello new partition.</span></span> <span data-ttu-id="6b84b-150">Ajouter l’ID de périphérique hello partition numéro toohello (Bonjour exemple `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="6b84b-150">Append hello partition number toohello device ID (in hello following example `/dev/sdc1`).</span></span> <span data-ttu-id="6b84b-151">Hello exemple suivant crée une partition ext4 sur /dev/sdc1 :</span><span class="sxs-lookup"><span data-stu-id="6b84b-151">hello following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Créer le système de fichiers](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="6b84b-153">Les systèmes SUSE Linux Enterprise 11 ne prennent en charge que l’accès en lecture seule aux systèmes de fichiers ext4.</span><span class="sxs-lookup"><span data-stu-id="6b84b-153">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="6b84b-154">Pour ces systèmes, il est recommandé de tooformat hello nouveau système de fichiers comme ext3 plutôt qu’ext4.</span><span class="sxs-lookup"><span data-stu-id="6b84b-154">For these systems, it is recommended tooformat hello new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="6b84b-155">Effectuez un répertoire toomount hello nouveau système de fichiers, comme suit :</span><span class="sxs-lookup"><span data-stu-id="6b84b-155">Make a directory toomount hello new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="6b84b-156">Enfin, vous pouvez monter le lecteur de hello, comme suit :</span><span class="sxs-lookup"><span data-stu-id="6b84b-156">Finally you can mount hello drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="6b84b-157">Hello disque de données est maintenant prêt toouse comme **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="6b84b-157">hello data disk is now ready toouse as **/datadrive**.</span></span>
   
    ![Créer hello active et montage hello le disque](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="6b84b-159">Ajoutez hello nouveau lecteur trop/etc/fstab :</span><span class="sxs-lookup"><span data-stu-id="6b84b-159">Add hello new drive too/etc/fstab:</span></span>
   
    <span data-ttu-id="6b84b-160">lecteur de hello tooensure est remontée automatiquement après qu’un redémarrage, qu'il doit être ajouté le fichier/etc/fstab de toohello.</span><span class="sxs-lookup"><span data-stu-id="6b84b-160">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="6b84b-161">En outre, il est recommandé que hello UUID (universellement Unique IDentifier) est utilisé dans/etc/fstab toorefer toohello lecteur plutôt que simplement hello nom de périphérique (par exemple, /dev/sdc1).</span><span class="sxs-lookup"><span data-stu-id="6b84b-161">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="6b84b-162">À l’aide de hello UUID évite hello incorrect disque monté tooa emplacement donné si hello du système d’exploitation détecte une erreur disque pendant le démarrage et les disques de données restants en étant celles reçoivent un ID de périphérique.</span><span class="sxs-lookup"><span data-stu-id="6b84b-162">Using hello UUID avoids hello incorrect disk being mounted tooa given location if hello OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="6b84b-163">toofind hello UUID du nouveau lecteur de hello, vous pouvez utiliser hello **blkid** utilitaire :</span><span class="sxs-lookup"><span data-stu-id="6b84b-163">toofind hello UUID of hello new drive, you can use hello **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="6b84b-164">sortie de Hello semble similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6b84b-164">hello output looks similar toohello following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="6b84b-165">Mal modification hello **/etc/fstab** fichier peut entraîner un système non démarrable.</span><span class="sxs-lookup"><span data-stu-id="6b84b-165">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="6b84b-166">En cas de doute, consultez la documentation de la distribution toohello pour plus d’informations sur la façon dont tooproperly modifier ce fichier.</span><span class="sxs-lookup"><span data-stu-id="6b84b-166">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="6b84b-167">Il est également recommandé qu’une sauvegarde de fichier/etc/fstab de hello est créée avant la modification.</span><span class="sxs-lookup"><span data-stu-id="6b84b-167">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="6b84b-168">Ensuite, ouvrez hello **/etc/fstab** fichier dans un éditeur de texte :</span><span class="sxs-lookup"><span data-stu-id="6b84b-168">Next, open hello **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="6b84b-169">Dans cet exemple, nous utilisons valeur UUID de hello pour hello nouvelle **/dev/sdc1** périphérique qui a été créé dans les étapes précédentes hello et point de montage hello **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="6b84b-169">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="6b84b-170">Ajouter hello suivant la fin ligne toohello Hello **/etc/fstab** fichier :</span><span class="sxs-lookup"><span data-stu-id="6b84b-170">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="6b84b-171">Ou, sur les systèmes basés sur SuSE Linux, vous devrez peut-être toouse un format légèrement différent :</span><span class="sxs-lookup"><span data-stu-id="6b84b-171">Or, on systems based on SuSE Linux you may need toouse a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="6b84b-172">Hello `nofail` option garantit que hello machine virtuelle démarre, même si le système de fichiers hello est endommagé ou disque de hello n’existe pas au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="6b84b-172">hello `nofail` option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="6b84b-173">Sans cette option, vous pouvez rencontrer le problème comme décrit dans [ne peut pas SSH tooLinux machine virtuelle en raison d’erreurs de tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span><span class="sxs-lookup"><span data-stu-id="6b84b-173">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="6b84b-174">Vous pouvez maintenant tester que le système de fichiers hello est monté correctement par le démontage et de réinstaller le système de fichiers hello, c'est-à-dire à l’aide de point de montage exemple hello `/datadrive` créé Bonjour étapes précédemment :</span><span class="sxs-lookup"><span data-stu-id="6b84b-174">You can now test that hello file system is mounted properly by unmounting and then remounting hello file system, i.e. using hello example mount point `/datadrive` created in hello earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="6b84b-175">Si hello `mount` commande génère une erreur, vérifiez hello fichier/etc/fstab pour la syntaxe correcte.</span><span class="sxs-lookup"><span data-stu-id="6b84b-175">If hello `mount` command produces an error, check hello /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="6b84b-176">Si des disques de données ou partitions supplémentaires sont créés, ajoutez-les séparément au fichier /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="6b84b-176">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="6b84b-177">Que les données du lecteur hello accessible en écriture à l’aide de cette commande :</span><span class="sxs-lookup"><span data-stu-id="6b84b-177">Make hello drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="6b84b-178">Suppression par la suite d’un disque de données sans avoir à modifier fstab pourrait hello VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="6b84b-178">Subsequently removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="6b84b-179">Si cela se produit fréquemment, la plupart des distributions fournissent soit hello `nofail` et/ou `nobootwait` fstab options qui permettent un tooboot système même en cas de disque de hello toomount au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="6b84b-179">If this is a common occurrence, most distributions provide either hello `nofail` and/or `nobootwait` fstab options that allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="6b84b-180">Pour plus d’informations sur ces paramètres, consultez la documentation de votre distribution.</span><span class="sxs-lookup"><span data-stu-id="6b84b-180">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="6b84b-181">Prise en charge de TRIM/UNMAP pour Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="6b84b-181">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="6b84b-182">Certains noyaux Linux prend en charge TRIM/annuler le mappage operations toodiscard les blocs inutilisés sur le disque de hello.</span><span class="sxs-lookup"><span data-stu-id="6b84b-182">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="6b84b-183">Ces opérations sont principalement dans tooinform standard de stockage Azure qui pages supprimées ne sont plus valides et peuvent être ignorées.</span><span class="sxs-lookup"><span data-stu-id="6b84b-183">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="6b84b-184">Le fait d’ignorer des pages peut vous permettre de réaliser des économies si vous créez des fichiers volumineux, puis les supprimez.</span><span class="sxs-lookup"><span data-stu-id="6b84b-184">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="6b84b-185">Il existe deux façons tooenable TRIM prend en charge dans votre VM Linux.</span><span class="sxs-lookup"><span data-stu-id="6b84b-185">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="6b84b-186">Comme d’habitude, consultez votre distribution pour hello approche recommandée :</span><span class="sxs-lookup"><span data-stu-id="6b84b-186">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="6b84b-187">Hello d’utilisation `discard` monter option dans `/etc/fstab`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="6b84b-187">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="6b84b-188">Dans certains hello cas `discard` option peut avoir des conséquences sur les performances.</span><span class="sxs-lookup"><span data-stu-id="6b84b-188">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="6b84b-189">Vous pouvez également exécuter hello `fstrim` commande manuellement à partir de la ligne de commande hello ou ajoutez-le tooyour crontab toorun régulièrement :</span><span class="sxs-lookup"><span data-stu-id="6b84b-189">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="6b84b-190">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="6b84b-190">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="6b84b-191">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="6b84b-191">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="6b84b-192">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="6b84b-192">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="6b84b-193">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6b84b-193">Next Steps</span></span>
<span data-ttu-id="6b84b-194">Vous pouvez en savoir plus sur l’utilisation de votre VM Linux Bonjour suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="6b84b-194">You can read more about using your Linux VM in hello following articles:</span></span>

* <span data-ttu-id="6b84b-195">[Comment toolog sur l’ordinateur virtuel de tooa exécutant Linux][Logon]</span><span class="sxs-lookup"><span data-stu-id="6b84b-195">[How toolog on tooa virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="6b84b-196">Comment toodetach un disque à partir d’une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="6b84b-196">How toodetach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="6b84b-197">À l’aide de hello CLI d’Azure avec le modèle de déploiement classique de hello</span><span class="sxs-lookup"><span data-stu-id="6b84b-197">Using hello Azure CLI with hello Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="6b84b-198">Configurer RAID sur une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="6b84b-198">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="6b84b-199">Configurer LVM sur une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="6b84b-199">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
