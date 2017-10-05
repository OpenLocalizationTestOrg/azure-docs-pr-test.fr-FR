---
title: "Attacher un disque à une machine virtuelle Linux dans Azure | Microsoft Docs"
description: "Découvrez comment attacher un disque de données à une machine virtuelle Linux à l’aide du modèle de déploiement Classic, et initialiser le disque de sorte qu’il soit prêt à l’emploi"
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
ms.openlocfilehash: 017ba7197e11c2b222082833d5acabb9e542b762
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-a-data-disk-to-a-linux-virtual-machine"></a><span data-ttu-id="e17a0-103">Association d’un disque de données à une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="e17a0-103">How to Attach a Data Disk to a Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="e17a0-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e17a0-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e17a0-105">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="e17a0-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="e17a0-106">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e17a0-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="e17a0-107">Apprenez comment [attacher un disque de données à l’aide du modèle de déploiement Resource Manager](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e17a0-107">See how to [attach a data disk using the Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="e17a0-108">Vous pouvez connecter des disques à vos machines virtuelles Azure, qu’ils soient vides ou non.</span><span class="sxs-lookup"><span data-stu-id="e17a0-108">You can attach both empty disks and disks that contain data to your Azure VMs.</span></span> <span data-ttu-id="e17a0-109">Les deux types de disques sont des fichiers .vhd conservés dans un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e17a0-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="e17a0-110">Comme avec l’ajout d’un disque à une machine Linux, après avoir connecté le disque vous devez l’initialiser et le formater afin qu’il soit prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="e17a0-110">As with adding any disk to a Linux machine, after you attach the disk you need to initialize and format it so it's ready for use.</span></span> <span data-ttu-id="e17a0-111">Cet article explique comment connecter des disques vides ou contenant des données à vos machines virtuelles, ainsi que comment initialiser et formater un nouveau disque.</span><span class="sxs-lookup"><span data-stu-id="e17a0-111">This article details attaching both empty disks and disks already containing data to your VMs, as well as how to then initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="e17a0-112">Il est recommandé d'utiliser un ou plusieurs disques distincts pour stocker les données d'une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e17a0-112">It's a best practice to use one or more separate disks to store a virtual machine's data.</span></span> <span data-ttu-id="e17a0-113">Lorsque vous créez une machine virtuelle Azure, celle-ci possède un disque de système d'exploitation et un disque temporaire.</span><span class="sxs-lookup"><span data-stu-id="e17a0-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="e17a0-114">**N’utilisez pas le disque temporaire pour stocker les données persistantes.**</span><span class="sxs-lookup"><span data-stu-id="e17a0-114">**Do not use the temporary disk to store persistent data.**</span></span> <span data-ttu-id="e17a0-115">Comme son nom l’indique, il ne permet qu’un stockage temporaire.</span><span class="sxs-lookup"><span data-stu-id="e17a0-115">As the name implies, it provides temporary storage only.</span></span> <span data-ttu-id="e17a0-116">Il n'offre aucune possibilité de redondance ou de sauvegarde, car il ne réside pas dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e17a0-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="e17a0-117">Le disque de ressources est habituellement géré par l’agent Linux Azure et monté automatiquement dans **/mnt/resource** (ou **/mnt** pour les images Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="e17a0-117">The temporary disk is typically managed by the Azure Linux Agent and automatically mounted to **/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="e17a0-118">Par contre, un disque de données peut être nommé par le noyau Linux, par exemple en `/dev/sdc`. Vous devez alors partitionner, formater et monter cette ressource.</span><span class="sxs-lookup"><span data-stu-id="e17a0-118">On the other hand, a data disk might be named by the Linux kernel something like `/dev/sdc`, and you need to partition, format, and mount this resource.</span></span> <span data-ttu-id="e17a0-119">Consultez le [Guide de l’utilisateur de l’Agent Linux Azure][Agent] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="e17a0-119">See the [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="e17a0-120">Initialisation d’un nouveau disque de données sous Linux</span><span class="sxs-lookup"><span data-stu-id="e17a0-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="e17a0-121">Connectez-vous avec SSH à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e17a0-121">SSH to your VM.</span></span> <span data-ttu-id="e17a0-122">Pour plus d’informations, consultez [Connexion à une machine virtuelle sous Linux][Logon].</span><span class="sxs-lookup"><span data-stu-id="e17a0-122">For more information, see [How to log on to a virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="e17a0-123">Ensuite, vous devez rechercher l'identificateur de périphérique pour initialiser le disque de données.</span><span class="sxs-lookup"><span data-stu-id="e17a0-123">Next you need to find the device identifier for the data disk to initialize.</span></span> <span data-ttu-id="e17a0-124">Il existe deux façons d'effectuer cette opération :</span><span class="sxs-lookup"><span data-stu-id="e17a0-124">There are two ways to do that:</span></span>
   
    <span data-ttu-id="e17a0-125">(a) Grep pour les appareils SCSI dans les fichiers journaux, par exemple avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e17a0-125">a) Grep for SCSI devices in the logs, such as in the following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="e17a0-126">Pour les distributions Ubuntu récentes, vous devrez peut-être utiliser `sudo grep SCSI /var/log/syslog` car l’enregistrement vers `/var/log/messages` peut être désactivé par défaut.</span><span class="sxs-lookup"><span data-stu-id="e17a0-126">For recent Ubuntu distributions, you may need to use `sudo grep SCSI /var/log/syslog` because logging to `/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="e17a0-127">L’identificateur du dernier disque de données ajouté est disponible dans les messages qui s’affichent.</span><span class="sxs-lookup"><span data-stu-id="e17a0-127">You can find the identifier of the last data disk that was added in the messages that are displayed.</span></span>
   
    ![Obtenir les messages du disque](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="e17a0-129">OU</span><span class="sxs-lookup"><span data-stu-id="e17a0-129">OR</span></span>
   
    <span data-ttu-id="e17a0-130">b) Utilisez la commande `lsscsi` pour rechercher l'ID de périphérique.</span><span class="sxs-lookup"><span data-stu-id="e17a0-130">b) Use the `lsscsi` command to find out the device id.</span></span> <span data-ttu-id="e17a0-131">`lsscsi` peut être installé par `yum install lsscsi` (dans des distributions Red Hat) ou `apt-get install lsscsi` (dans des distributions Debian).</span><span class="sxs-lookup"><span data-stu-id="e17a0-131">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="e17a0-132">Vous pouvez retrouver le disque que vous recherchez par son *LUN* ou **numéro d'unité logique**.</span><span class="sxs-lookup"><span data-stu-id="e17a0-132">You can find the disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="e17a0-133">Par exemple, le *LUN* pour les disques attachés peuvent être vus facilement à partir de `azure vm disk list <virtual-machine>` en tant que :</span><span class="sxs-lookup"><span data-stu-id="e17a0-133">For example, the *lun* for the disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="e17a0-134">Le résultat ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="e17a0-134">The output is similar to the following:</span></span>

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
   
    <span data-ttu-id="e17a0-135">Comparez ces données à la sortie de `lsscsi` pour le même exemple de machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="e17a0-135">Compare this data with the output of `lsscsi` for the same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="e17a0-136">Le dernier numéro du tuple dans chaque ligne est le *LUN*.</span><span class="sxs-lookup"><span data-stu-id="e17a0-136">The last number in the tuple in each row is the *lun*.</span></span> <span data-ttu-id="e17a0-137">Pour plus d'informations, consultez `man lsscsi` .</span><span class="sxs-lookup"><span data-stu-id="e17a0-137">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="e17a0-138">À l’invite, tapez la commande suivante pour créer votre appareil :</span><span class="sxs-lookup"><span data-stu-id="e17a0-138">At the prompt, type the following command to create your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="e17a0-139">Lorsque vous y êtes invité, tapez  **n**  pour créer une partition.</span><span class="sxs-lookup"><span data-stu-id="e17a0-139">When prompted, type **n** to create a partition.</span></span>

    ![Créer un appareil](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="e17a0-141">Lorsque vous y êtes invité, tapez **p** pour faire de la partition la partition principale.</span><span class="sxs-lookup"><span data-stu-id="e17a0-141">When prompted, type **p** to make the partition the primary partition.</span></span> <span data-ttu-id="e17a0-142">Tapez **1** pour la définir comme première partition, puis appuyez sur Entrée pour accepter la valeur par défaut du cylindre.</span><span class="sxs-lookup"><span data-stu-id="e17a0-142">Type **1** to make it the first partition, and then type enter to accept the default value for the cylinder.</span></span> <span data-ttu-id="e17a0-143">Sur certains systèmes, il est possible que les valeurs par défaut des premier et dernier secteurs s’affichent à la place de celles du cylindre.</span><span class="sxs-lookup"><span data-stu-id="e17a0-143">On some systems, it can show the default values of the first and the last sectors, instead of the cylinder.</span></span> <span data-ttu-id="e17a0-144">Vous pouvez choisir d’accepter ces valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="e17a0-144">You can choose to accept these defaults.</span></span>

    ![Créer une partition](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="e17a0-146">Tapez **p** pour afficher les détails relatifs au disque faisant l’objet de la partition.</span><span class="sxs-lookup"><span data-stu-id="e17a0-146">Type **p** to see the details about the disk that is being partitioned.</span></span>

    ![Répertorier les informations sur le disque](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="e17a0-148">Tapez **w** pour écrire les paramètres du disque.</span><span class="sxs-lookup"><span data-stu-id="e17a0-148">Type **w** to write the settings for the disk.</span></span>

    ![Écrire les modifications apportées au disque](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="e17a0-150">Vous pouvez alors créer le système de fichiers sur la nouvelle partition.</span><span class="sxs-lookup"><span data-stu-id="e17a0-150">Now you can create the file system on the new partition.</span></span> <span data-ttu-id="e17a0-151">Ajoutez le numéro de partition à l’identifiant d’appareil (dans l’exemple suivant `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="e17a0-151">Append the partition number to the device ID (in the following example `/dev/sdc1`).</span></span> <span data-ttu-id="e17a0-152">L’exemple suivant crée une partition ext4 sur /dev/sdc1 :</span><span class="sxs-lookup"><span data-stu-id="e17a0-152">The following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Créer le système de fichiers](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="e17a0-154">Les systèmes SUSE Linux Enterprise 11 ne prennent en charge que l’accès en lecture seule aux systèmes de fichiers ext4.</span><span class="sxs-lookup"><span data-stu-id="e17a0-154">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="e17a0-155">Pour ces systèmes, il est recommandé de formater le nouveau système de fichiers en ext3 plutôt que ext4.</span><span class="sxs-lookup"><span data-stu-id="e17a0-155">For these systems, it is recommended to format the new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="e17a0-156">Créez un répertoire pour monter le nouveau système de fichiers, comme suit :</span><span class="sxs-lookup"><span data-stu-id="e17a0-156">Make a directory to mount the new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="e17a0-157">Vous pouvez alors monter le lecteur, comme suit :</span><span class="sxs-lookup"><span data-stu-id="e17a0-157">Finally you can mount the drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="e17a0-158">Le disque de données est désormais prêt à être utilisé en tant que **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="e17a0-158">The data disk is now ready to use as **/datadrive**.</span></span>
   
    ![Créer le répertoire et monter le disque](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="e17a0-160">Ajoutez le nouveau lecteur à /etc/fstab :</span><span class="sxs-lookup"><span data-stu-id="e17a0-160">Add the new drive to /etc/fstab:</span></span>
   
    <span data-ttu-id="e17a0-161">Pour vous assurer que le lecteur est remonté automatiquement après un redémarrage, vous devez l’ajouter au fichier /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="e17a0-161">To ensure the drive is remounted automatically after a reboot it must be added to the /etc/fstab file.</span></span> <span data-ttu-id="e17a0-162">En outre, il est vivement recommandé d’utiliser l’UUID (identificateur global unique) dans /etc/fstab comme référence au lecteur, plutôt que le nom d’appareil uniquement (par exemple, /dev/sdc1).</span><span class="sxs-lookup"><span data-stu-id="e17a0-162">In addition, it is highly recommended that the UUID (Universally Unique IDentifier) is used in /etc/fstab to refer to the drive rather than just the device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="e17a0-163">L’utilisation de l’UUID évite le montage d’un disque incorrect sur un emplacement donné si le système d’exploitation détecte une erreur de disque lors du démarrage, et l’affectation des disques de données restants éventuels à ces ID d’appareils.</span><span class="sxs-lookup"><span data-stu-id="e17a0-163">Using the UUID avoids the incorrect disk being mounted to a given location if the OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="e17a0-164">Pour rechercher l’UUID du nouveau lecteur, vous pouvez vous servir de l’utilitaire **blkid** :</span><span class="sxs-lookup"><span data-stu-id="e17a0-164">To find the UUID of the new drive, you can use the **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="e17a0-165">Le résultat ressemble à l’exemple qui suit :</span><span class="sxs-lookup"><span data-stu-id="e17a0-165">The output looks similar to the following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="e17a0-166">si vous ne modifiez pas correctement le fichier **/etc/fstab** , il se peut que le système ne puisse plus démarrer.</span><span class="sxs-lookup"><span data-stu-id="e17a0-166">Improperly editing the **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="e17a0-167">En cas de doute, reportez-vous à la documentation de la distribution pour obtenir des informations sur la modification adéquate de ce fichier.</span><span class="sxs-lookup"><span data-stu-id="e17a0-167">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="e17a0-168">Il est par ailleurs vivement recommandé de créer une sauvegarde du fichier /etc/fstab avant de le modifier.</span><span class="sxs-lookup"><span data-stu-id="e17a0-168">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="e17a0-169">Ensuite, ouvrez le fichier **/etc/fstab** dans un éditeur de texte :</span><span class="sxs-lookup"><span data-stu-id="e17a0-169">Next, open the **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="e17a0-170">Dans cet exemple, nous utilisons la valeur UUID pour le nouvel appareil **/dev/sdc1** créé lors des étapes précédentes et le point de montage **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="e17a0-170">In this example, we use the UUID value for the new **/dev/sdc1** device that was created in the previous steps, and the mountpoint **/datadrive**.</span></span> <span data-ttu-id="e17a0-171">Ajoutez la ligne suivante à la fin du fichier **/etc/fstab** :</span><span class="sxs-lookup"><span data-stu-id="e17a0-171">Add the following line to the end of the **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="e17a0-172">Ou, sur les systèmes basés sur SUSE Linux, vous pouvez être amené à devoir utiliser un format légèrement différent :</span><span class="sxs-lookup"><span data-stu-id="e17a0-172">Or, on systems based on SuSE Linux you may need to use a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="e17a0-173">L’option `nofail` garantit que la machine virtuelle démarre même si le système de fichiers est endommagé ou si le disque n’existe pas au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="e17a0-173">The `nofail` option ensures that the VM starts even if the filesystem is corrupt or the disk does not exist at boot time.</span></span> <span data-ttu-id="e17a0-174">Sans cette option, vous pouvez être confronté au comportement décrit dans [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/) (Connexion SSH vers machine virtuelle Linux impossible en raison d’erreurs FSTAB).</span><span class="sxs-lookup"><span data-stu-id="e17a0-174">Without this option, you may encounter behavior as described in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="e17a0-175">Vous pouvez désormais vérifier si le système de fichiers est monté correctement en le démontant puis en le remontant, par exemple</span><span class="sxs-lookup"><span data-stu-id="e17a0-175">You can now test that the file system is mounted properly by unmounting and then remounting the file system, i.e.</span></span> <span data-ttu-id="e17a0-176">en utilisant l’exemple de point de montage `/datadrive` créé lors des étapes précédentes :</span><span class="sxs-lookup"><span data-stu-id="e17a0-176">using the example mount point `/datadrive` created in the earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="e17a0-177">Si la commande `mount` génère une erreur, vérifiez que la syntaxe utilisée dans le fichier /etc/fstab est correcte.</span><span class="sxs-lookup"><span data-stu-id="e17a0-177">If the `mount` command produces an error, check the /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="e17a0-178">Si des disques de données ou partitions supplémentaires sont créés, ajoutez-les séparément au fichier /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="e17a0-178">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="e17a0-179">Utilisez cette commande pour rendre le disque accessible en écriture :</span><span class="sxs-lookup"><span data-stu-id="e17a0-179">Make the drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="e17a0-180">La suppression ultérieure d’un disque de données sans modifier fstab pourrait entraîner l’échec du démarrage de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e17a0-180">Subsequently removing a data disk without editing fstab could cause the VM to fail to boot.</span></span> <span data-ttu-id="e17a0-181">S’il s’agit d’une occurrence courante, la plupart des distributions proposent les options fstab `nofail` et/ou `nobootwait` qui permettent à un système de démarrer même si le disque n’est pas monté au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="e17a0-181">If this is a common occurrence, most distributions provide either the `nofail` and/or `nobootwait` fstab options that allow a system to boot even if the disk fails to mount at boot time.</span></span> <span data-ttu-id="e17a0-182">Pour plus d’informations sur ces paramètres, consultez la documentation de votre distribution.</span><span class="sxs-lookup"><span data-stu-id="e17a0-182">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="e17a0-183">Prise en charge de TRIM/UNMAP pour Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="e17a0-183">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="e17a0-184">Certains noyaux Linux prennent en charge les opérations TRIM/UNMAP pour ignorer les blocs inutilisés sur le disque.</span><span class="sxs-lookup"><span data-stu-id="e17a0-184">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="e17a0-185">Ces opérations sont particulièrement utiles dans un stockage standard pour informer Azure que des pages supprimées ne sont plus valides et peuvent être ignorées.</span><span class="sxs-lookup"><span data-stu-id="e17a0-185">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="e17a0-186">Le fait d’ignorer des pages peut vous permettre de réaliser des économies si vous créez des fichiers volumineux, puis les supprimez.</span><span class="sxs-lookup"><span data-stu-id="e17a0-186">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="e17a0-187">Il existe deux façons d’activer la prise en charge de TRIM sur votre machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="e17a0-187">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="e17a0-188">Comme d’habitude, consultez votre distribution pour connaître l’approche recommandée :</span><span class="sxs-lookup"><span data-stu-id="e17a0-188">As usual, consult your distribution for the recommended approach:</span></span>

* <span data-ttu-id="e17a0-189">Utilisez l’option de montage `discard` dans `/etc/fstab`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="e17a0-189">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="e17a0-190">Dans certains cas, l’option `discard` peut avoir un impact sur la performance.</span><span class="sxs-lookup"><span data-stu-id="e17a0-190">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="e17a0-191">Vous pouvez également exécuter la commande `fstrim` manuellement à partir de la ligne de commande ou l’ajouter à votre crontab pour l’exécuter régulièrement :</span><span class="sxs-lookup"><span data-stu-id="e17a0-191">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>
  
    <span data-ttu-id="e17a0-192">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="e17a0-192">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="e17a0-193">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="e17a0-193">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="e17a0-194">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="e17a0-194">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="e17a0-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e17a0-195">Next Steps</span></span>
<span data-ttu-id="e17a0-196">Vous trouverez plus d’informations sur l’utilisation de votre machine virtuelle Linux dans les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="e17a0-196">You can read more about using your Linux VM in the following articles:</span></span>

* <span data-ttu-id="e17a0-197">[Connexion à une machine virtuelle exécutant Linux][Logon]</span><span class="sxs-lookup"><span data-stu-id="e17a0-197">[How to log on to a virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="e17a0-198">Détachement d'un disque d'une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="e17a0-198">How to detach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="e17a0-199">Utilisation de l’interface CLI Azure avec le modèle de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="e17a0-199">Using the Azure CLI with the Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="e17a0-200">Configurer RAID sur une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="e17a0-200">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="e17a0-201">Configurer LVM sur une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="e17a0-201">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
