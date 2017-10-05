---
title: "Ajouter un disque à une machine virtuelle Linux avec Azure CLI | Microsoft Docs"
description: "Découvrez comment ajouter un disque persistant à votre machine virtuelle Linux avec Azure CLI 1.0 et 2.0."
keywords: machine virtuelle Linux, ajouter un disque de ressources
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 3005a066-7a84-4dc5-bdaa-574c75e6e411
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 02/02/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 185dd276cd79cb7053605d651e8ecdc7fd1e7636
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="add-a-disk-to-a-linux-vm"></a><span data-ttu-id="87439-104">Ajouter un disque à une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="87439-104">Add a disk to a Linux VM</span></span>
<span data-ttu-id="87439-105">Cet article explique comment attacher un disque persistant à votre machine virtuelle afin de conserver vos données, et ce, même si votre machine virtuelle est remise en service en raison d’une opération de maintenance ou de redimensionnement.</span><span class="sxs-lookup"><span data-stu-id="87439-105">This article shows how to attach a persistent disk to your VM so that you can preserve your data - even if your VM is reprovisioned due to maintenance or resizing.</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="87439-106">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="87439-106">Quick Commands</span></span>
<span data-ttu-id="87439-107">L’exemple suivant attache un disque de `50` Go à la machine virtuelle nommée `myVM` dans le groupe de ressources nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="87439-107">The following example attaches a `50`GB disk to the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

<span data-ttu-id="87439-108">Pour utiliser des disques gérés :</span><span class="sxs-lookup"><span data-stu-id="87439-108">To use managed disks:</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

<span data-ttu-id="87439-109">Pour utiliser des disques non gérés :</span><span class="sxs-lookup"><span data-stu-id="87439-109">To use unmanaged disks:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a><span data-ttu-id="87439-110">Attacher un disque géré</span><span class="sxs-lookup"><span data-stu-id="87439-110">Attach a managed disk</span></span>

<span data-ttu-id="87439-111">En utilisant des disques gérés, vous pouvez vous concentrer sur vos machines virtuelles et leurs disques sans vous soucier des comptes de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="87439-111">Using managed disks enables you to focus on your VMs and their disks without worrying about Azure Storage accounts.</span></span> <span data-ttu-id="87439-112">Vous pouvez rapidement créer et attacher un disque géré à une machine virtuelle en utilisant le même groupe de ressources Azure. Vous pouvez également créer autant de disques que vous le souhaitez et les attacher ensuite à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="87439-112">You can quickly create and attach a managed disk to a VM using the same Azure resource group, or you can create any number of disks and then attach them.</span></span>


### <a name="attach-a-new-disk-to-a-vm"></a><span data-ttu-id="87439-113">Attacher un nouveau disque à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="87439-113">Attach a new disk to a VM</span></span>

<span data-ttu-id="87439-114">Si vous avez uniquement besoin d’un nouveau disque sur votre machine virtuelle, vous pouvez utiliser la commande `az vm disk attach`.</span><span class="sxs-lookup"><span data-stu-id="87439-114">If you just need a new disk on your VM, you can use the `az vm disk attach` command.</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a><span data-ttu-id="87439-115">Association d'un disque existant</span><span class="sxs-lookup"><span data-stu-id="87439-115">Attach an existing disk</span></span> 

<span data-ttu-id="87439-116">Dans de nombreux cas, vous attachez des disques qui ont déjà été créés.</span><span class="sxs-lookup"><span data-stu-id="87439-116">In many cases you attach disks that have already been created.</span></span> <span data-ttu-id="87439-117">Commencez par rechercher l’ID du disque pour l’intégrer à la commande `az vm disk attach`.</span><span class="sxs-lookup"><span data-stu-id="87439-117">You first find the disk id and then pass that to the `az vm disk attach` command.</span></span> <span data-ttu-id="87439-118">L’exemple suivant utilise un disque créé avec `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span><span class="sxs-lookup"><span data-stu-id="87439-118">The following example uses a disk created with `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span></span>

```azurecli
# find the disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

<span data-ttu-id="87439-119">Le résultat ressemble à ce qui suit (vous pouvez appliquer l’option `-o table` à n’importe quelle commande afin d’obtenir le bon format de sortie) :</span><span class="sxs-lookup"><span data-stu-id="87439-119">The output looks something like the following (you can use the `-o table` option to any command to format the output in ):</span></span>

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Empty",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": null,
    "storageAccountId": null
  },
  "diskSizeGb": 50,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/rasquill-script/providers/Microsoft.Compute/disks/myDataDisk",
  "location": "westus",
  "name": "myDataDisk",
  "osType": null,
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-02T23:35:47.708082+00:00",
  "type": "Microsoft.Compute/disks"
}
```


## <a name="attach-an-unmanaged-disk"></a><span data-ttu-id="87439-120">Attacher un disque non géré</span><span class="sxs-lookup"><span data-stu-id="87439-120">Attach an unmanaged disk</span></span>

<span data-ttu-id="87439-121">Vous pouvez rapidement ajouter un nouveau disque qui sera créé dans le même compte de stockage que votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="87439-121">Attaching a new disk is quick if you do not mind creating a disk in the same storage account as your VM.</span></span> <span data-ttu-id="87439-122">Tapez `azure vm disk attach-new` afin de créer un nouveau disque (Go) et de l’associer à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="87439-122">Type `azure vm disk attach-new` to create and attach a new GB disk for your VM.</span></span> <span data-ttu-id="87439-123">Si vous n'identifiez pas explicitement un compte de stockage, les disques que vous créez sont placés dans le même compte de stockage que celui sur lequel réside le disque du système d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="87439-123">If you do not explicitly identify a storage account, any disk you create is placed in the same storage account where your OS disk resides.</span></span> <span data-ttu-id="87439-124">L’exemple suivant attache un disque de `50` Go à la machine virtuelle nommée `myVM` dans le groupe de ressources nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="87439-124">The following example attaches a `50`GB disk to the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-to-the-linux-vm-to-mount-the-new-disk"></a><span data-ttu-id="87439-125">Se connecter à la machine virtuelle Linux afin de monter le nouveau disque</span><span class="sxs-lookup"><span data-stu-id="87439-125">Connect to the Linux VM to mount the new disk</span></span>
> [!NOTE]
> <span data-ttu-id="87439-126">Dans cette rubrique, la connexion à la machine virtuelle est effectuée à l’aide de noms d’utilisateurs et de mots de passe.</span><span class="sxs-lookup"><span data-stu-id="87439-126">This topic connects to a VM using usernames and passwords.</span></span> <span data-ttu-id="87439-127">Pour utiliser des paires de clés publiques et privées pour interagir avec votre machine virtuelle, consultez [Utilisation de SSH avec Linux sur Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="87439-127">To use public and private key pairs to communicate with your VM, see [How to Use SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
> 
> 

<span data-ttu-id="87439-128">Vous devez exécuter SSH dans votre machine virtuelle Azure afin de partitionner, de formater et de monter votre nouveau disque pour que la machine virtuelle Linux puisse l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="87439-128">You need to SSH into your Azure VM to partition, format, and mount your new disk so your Linux VM can use it.</span></span> <span data-ttu-id="87439-129">Si vous n’êtes pas familier de la connexion via **ssh**, la commande prend la forme `ssh <username>@<FQDNofAzureVM> -p <the ssh port>` et ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="87439-129">If you're not familiar with connecting with **ssh**, the command takes the form `ssh <username>@<FQDNofAzureVM> -p <the ssh port>`, and looks like the following:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

<span data-ttu-id="87439-130">Sortie</span><span class="sxs-lookup"><span data-stu-id="87439-130">Output</span></span>

```bash
The authenticity of host 'mypublicdns.westus.cloudapp.azure.com (191.239.51.1)' can't be established.
ECDSA key fingerprint is bx:xx:xx:xx:xx:xx:xx:xx:xx:x:x:x:x:x:x:xx.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.westus.cloudapp.azure.com,191.239.51.1' (ECDSA) to the list of known hosts.
ops@mypublicdns.westus.cloudapp.azure.com's password:
Welcome to Ubuntu 14.04.2 LTS (GNU/Linux 3.16.0-37-generic x86_64)

* Documentation:  https://help.ubuntu.com/

System information as of Fri May 22 21:02:32 UTC 2015

System load: 0.37              Memory usage: 2%   Processes:       207
Usage of /:  41.4% of 1.94GB   Swap usage:   0%   Users logged in: 0

Graph this data and manage this system at:
  https://landscape.canonical.com/

Get cloud support with Ubuntu Advantage Cloud Guest:
  http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

ops@myVM:~$
```

<span data-ttu-id="87439-131">Maintenant que vous êtes connecté à votre machine virtuelle, vous êtes prêt à attacher un disque.</span><span class="sxs-lookup"><span data-stu-id="87439-131">Now that you're connected to your VM, you're ready to attach a disk.</span></span>  <span data-ttu-id="87439-132">Recherchez tout d’abord le disque à l’aide de `dmesg | grep SCSI` (La méthode que vous utilisez pour découvrir les capacités du nouveau disque peut varier).</span><span class="sxs-lookup"><span data-stu-id="87439-132">First find the disk, using `dmesg | grep SCSI` (the method you use to discover your new disk may vary).</span></span> <span data-ttu-id="87439-133">Le résultat est alors le suivant :</span><span class="sxs-lookup"><span data-stu-id="87439-133">In this case, it looks something like:</span></span>

```bash
dmesg | grep SCSI
```

<span data-ttu-id="87439-134">Sortie</span><span class="sxs-lookup"><span data-stu-id="87439-134">Output</span></span>

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

<span data-ttu-id="87439-135">et dans le scénario évoqué dans cette rubrique, le disque `sdc` est celui que nous voulons.</span><span class="sxs-lookup"><span data-stu-id="87439-135">and in the case of this topic, the `sdc` disk is the one that we want.</span></span> <span data-ttu-id="87439-136">Partitionnons maintenant le disque avec `sudo fdisk /dev/sdc`, en supposant que dans votre cas, il s’agissait d’un disque `sdc` et utilisons-le en tant que disque principal sur la partition 1, en acceptant les autres valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="87439-136">Now partition the disk with `sudo fdisk /dev/sdc` -- assuming that in your case the disk was `sdc`, and make it a primary disk on partition 1, and accept the other defaults.</span></span>

```bash
sudo fdisk /dev/sdc
```

<span data-ttu-id="87439-137">Sortie</span><span class="sxs-lookup"><span data-stu-id="87439-137">Output</span></span>

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide to write them.
After that, of course, the previous content won't be recoverable.

Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-10485759, default 2048):
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-10485759, default 10485759):
Using default value 10485759
```

<span data-ttu-id="87439-138">Créez la partition en saisissant `p` lors de l’invite :</span><span class="sxs-lookup"><span data-stu-id="87439-138">Create the partition by typing `p` at the prompt:</span></span>

```bash
Command (m for help): p

Disk /dev/sdc: 5368 MB, 5368709120 bytes
255 heads, 63 sectors/track, 652 cylinders, total 10485760 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x2a59b123

   Device Boot      Start         End      Blocks   Id  System
/dev/sdc1            2048    10485759     5241856   83  Linux

Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.
```

<span data-ttu-id="87439-139">Écrivez un système de fichiers sur la partition à l’aide de la commande **mkfs** , en spécifiant le type de votre système de fichier et le nom de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="87439-139">And write a file system to the partition by using the **mkfs** command, specifying your filesystem type and the device name.</span></span> <span data-ttu-id="87439-140">Dans cette rubrique, nous utilisons `ext4` et `/dev/sdc1` (voir ci-dessus) :</span><span class="sxs-lookup"><span data-stu-id="87439-140">In this topic, we're using `ext4` and `/dev/sdc1` from above:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="87439-141">Sortie</span><span class="sxs-lookup"><span data-stu-id="87439-141">Output</span></span>

```bash
mke2fs 1.42.9 (4-Feb-2014)
Discarding device blocks: done
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
327680 inodes, 1310464 blocks
65523 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=1342177280
40 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
    32768, 98304, 163840, 229376, 294912, 819200, 884736
Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done
```

<span data-ttu-id="87439-142">Nous créons désormais un répertoire afin de monter le système de fichiers à l’aide de `mkdir`:</span><span class="sxs-lookup"><span data-stu-id="87439-142">Now we create a directory to mount the file system using `mkdir`:</span></span>

```bash
sudo mkdir /datadrive
```

<span data-ttu-id="87439-143">Vous montez le répertoire à l’aide de `mount`:</span><span class="sxs-lookup"><span data-stu-id="87439-143">And you mount the directory using `mount`:</span></span>

```bash
sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="87439-144">Le disque de données est désormais utilisable en tant que `/datadrive`.</span><span class="sxs-lookup"><span data-stu-id="87439-144">The data disk is now ready to use as `/datadrive`.</span></span>

```bash
ls
```

<span data-ttu-id="87439-145">Sortie</span><span class="sxs-lookup"><span data-stu-id="87439-145">Output</span></span>

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

<span data-ttu-id="87439-146">Pour vous assurer que le lecteur est remonté automatiquement après un redémarrage, vous devez l’ajouter au fichier /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="87439-146">To ensure the drive is remounted automatically after a reboot it must be added to the /etc/fstab file.</span></span> <span data-ttu-id="87439-147">En outre, il est vivement recommandé d’utiliser l’UUID (identificateur global unique) dans /etc/fstab comme référence au lecteur, plutôt que le nom d’appareil uniquement (par exemple, `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="87439-147">In addition, it is highly recommended that the UUID (Universally Unique IDentifier) is used in /etc/fstab to refer to the drive rather than just the device name (such as, `/dev/sdc1`).</span></span> <span data-ttu-id="87439-148">Si le système d’exploitation détecte une erreur disque pendant le démarrage, l’utilisation de l’UUID évite que le disque incorrect ne soit monté sur un emplacement donné.</span><span class="sxs-lookup"><span data-stu-id="87439-148">If the OS detects a disk error during boot, using the UUID avoids the incorrect disk being mounted to a given location.</span></span> <span data-ttu-id="87439-149">Les disques de données restants reçoivent alors les mêmes ID d’appareil.</span><span class="sxs-lookup"><span data-stu-id="87439-149">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="87439-150">Pour rechercher l’UUID du nouveau lecteur, utilisez l’utilitaire **blkid** :</span><span class="sxs-lookup"><span data-stu-id="87439-150">To find the UUID of the new drive, use the **blkid** utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="87439-151">Le résultat ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="87439-151">The output looks similar to the following:</span></span>

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> <span data-ttu-id="87439-152">si vous ne modifiez pas correctement le fichier **/etc/fstab** , il se peut que le système ne puisse plus démarrer.</span><span class="sxs-lookup"><span data-stu-id="87439-152">Improperly editing the **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="87439-153">En cas de doute, reportez-vous à la documentation de la distribution pour obtenir des informations sur la modification adéquate de ce fichier.</span><span class="sxs-lookup"><span data-stu-id="87439-153">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="87439-154">Il est par ailleurs vivement recommandé de créer une sauvegarde du fichier /etc/fstab avant de le modifier.</span><span class="sxs-lookup"><span data-stu-id="87439-154">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>
> 
> 

<span data-ttu-id="87439-155">Ensuite, ouvrez le fichier **/etc/fstab** dans un éditeur de texte :</span><span class="sxs-lookup"><span data-stu-id="87439-155">Next, open the **/etc/fstab** file in a text editor:</span></span>

```bash
sudo vi /etc/fstab
```

<span data-ttu-id="87439-156">Dans cet exemple, nous utilisons la valeur UUID pour le nouvel appareil **/dev/sdc1** créé lors des étapes précédentes et le point de montage **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="87439-156">In this example, we use the UUID value for the new **/dev/sdc1** device that was created in the previous steps, and the mountpoint **/datadrive**.</span></span> <span data-ttu-id="87439-157">Ajoutez la ligne suivante à la fin du fichier **/etc/fstab** :</span><span class="sxs-lookup"><span data-stu-id="87439-157">Add the following line to the end of the **/etc/fstab** file:</span></span>

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> <span data-ttu-id="87439-158">La suppression ultérieure d’un disque de données sans modifier fstab pourrait entraîner l’échec du démarrage de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="87439-158">Later removing a data disk without editing fstab could cause the VM to fail to boot.</span></span> <span data-ttu-id="87439-159">La plupart des distributions proposent les options fstab `nofail` et/ou `nobootwait`.</span><span class="sxs-lookup"><span data-stu-id="87439-159">Most distributions provide either the `nofail` and/or `nobootwait` fstab options.</span></span> <span data-ttu-id="87439-160">Ces options permettent à un système de démarrer même si le disque n’est pas monté au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="87439-160">These options allow a system to boot even if the disk fails to mount at boot time.</span></span> <span data-ttu-id="87439-161">Pour plus d’informations sur ces paramètres, consultez la documentation de votre distribution.</span><span class="sxs-lookup"><span data-stu-id="87439-161">Consult your distribution's documentation for more information on these parameters.</span></span>
> 
> <span data-ttu-id="87439-162">L’option **nofail** garantit que la machine virtuelle démarre même si le système de fichiers est endommagé ou si le disque n’existe pas au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="87439-162">The **nofail** option ensures that the VM starts even if the filesystem is corrupt or the disk does not exist at boot time.</span></span> <span data-ttu-id="87439-163">Sans cette option, vous pouvez être confronté au comportement décrit dans [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/) (Connexion SSH vers machine virtuelle Linux impossible en raison d’erreurs FSTAB)</span><span class="sxs-lookup"><span data-stu-id="87439-163">Without this option, you may encounter behavior as described in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="87439-164">Prise en charge de TRIM/UNMAP pour Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="87439-164">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="87439-165">Certains noyaux Linux prennent en charge les opérations TRIM/UNMAP pour ignorer les blocs inutilisés sur le disque.</span><span class="sxs-lookup"><span data-stu-id="87439-165">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="87439-166">Cela est particulièrement utile dans le stockage standard pour informer Azure que des pages supprimées ne sont plus valides et peuvent être ignorées.</span><span class="sxs-lookup"><span data-stu-id="87439-166">This is primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="87439-167">Vous pouvez ainsi faire des économies si vous créez des fichiers volumineux, puis les supprimez.</span><span class="sxs-lookup"><span data-stu-id="87439-167">This can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="87439-168">Il existe deux façons d’activer la prise en charge de TRIM sur votre machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="87439-168">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="87439-169">Comme d’habitude, consultez votre distribution pour connaître l’approche recommandée :</span><span class="sxs-lookup"><span data-stu-id="87439-169">As usual, consult your distribution for the recommended approach:</span></span>

* <span data-ttu-id="87439-170">Utilisez l’option de montage `discard` dans `/etc/fstab`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="87439-170">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* <span data-ttu-id="87439-171">Dans certains cas, l’option `discard` peut avoir un impact sur la performance.</span><span class="sxs-lookup"><span data-stu-id="87439-171">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="87439-172">Vous pouvez également exécuter la commande `fstrim` manuellement à partir de la ligne de commande ou l’ajouter à votre crontab pour l’exécuter régulièrement :</span><span class="sxs-lookup"><span data-stu-id="87439-172">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>
  
    <span data-ttu-id="87439-173">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="87439-173">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="87439-174">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="87439-174">**RHEL/CentOS**</span></span>

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="87439-175">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="87439-175">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="87439-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="87439-176">Next Steps</span></span>
* <span data-ttu-id="87439-177">N’oubliez pas que votre nouveau disque n’est pas disponible sur votre machine virtuelle en cas de redémarrage, sauf si vous écrivez les informations sur votre fichier [fstab](http://en.wikipedia.org/wiki/Fstab) .</span><span class="sxs-lookup"><span data-stu-id="87439-177">Remember, that your new disk is not available to the VM if it reboots unless you write that information to your [fstab](http://en.wikipedia.org/wiki/Fstab) file.</span></span>
* <span data-ttu-id="87439-178">Pour vous assurer que votre machine virtuelle Linux est correctement configurée, passez en revue les recommandations visant à [optimiser les performances de votre machine virtuelle Linux](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="87439-178">To ensure your Linux VM is configured correctly, review the [Optimize your Linux machine performance](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recommendations.</span></span>
* <span data-ttu-id="87439-179">Développez votre capacité de stockage en ajoutant des disques supplémentaires et [configurez RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour augmenter les performances.</span><span class="sxs-lookup"><span data-stu-id="87439-179">Expand your storage capacity by adding additional disks and [configure RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional performance.</span></span>

