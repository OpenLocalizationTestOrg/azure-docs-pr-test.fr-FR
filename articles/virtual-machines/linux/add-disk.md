---
title: "une machine virtuelle de tooLinux de disque à l’aide d’aaaAdd hello CLI d’Azure | Documents Microsoft"
description: En savoir plus tooadd un tooyour de disque persistant Linux VM avec hello Azure CLI 1.0 et 2.0.
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
ms.openlocfilehash: 0dc5236be62d96b70dd47a7f621f626a037e22aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-disk-tooa-linux-vm"></a><span data-ttu-id="30f94-104">Ajouter un tooa de disque Linux VM</span><span class="sxs-lookup"><span data-stu-id="30f94-104">Add a disk tooa Linux VM</span></span>
<span data-ttu-id="30f94-105">Cet article explique tooattach un persistant de disque tooyour VM afin que vous pouvez conserver vos données : même si votre machine virtuelle est remise en service en raison de toomaintenance ou redimensionnement.</span><span class="sxs-lookup"><span data-stu-id="30f94-105">This article shows how tooattach a persistent disk tooyour VM so that you can preserve your data - even if your VM is reprovisioned due toomaintenance or resizing.</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="30f94-106">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="30f94-106">Quick Commands</span></span>
<span data-ttu-id="30f94-107">Hello suivants exemple attache un `50`Go disque toohello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="30f94-107">hello following example attaches a `50`GB disk toohello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

<span data-ttu-id="30f94-108">toouse des disques gérés :</span><span class="sxs-lookup"><span data-stu-id="30f94-108">toouse managed disks:</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

<span data-ttu-id="30f94-109">disques toouse non managée :</span><span class="sxs-lookup"><span data-stu-id="30f94-109">toouse unmanaged disks:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a><span data-ttu-id="30f94-110">Attacher un disque géré</span><span class="sxs-lookup"><span data-stu-id="30f94-110">Attach a managed disk</span></span>

<span data-ttu-id="30f94-111">L’utilisation de disques gérés vous permet toofocus sur vos machines virtuelles et leurs disques sans vous préoccuper des comptes de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="30f94-111">Using managed disks enables you toofocus on your VMs and their disks without worrying about Azure Storage accounts.</span></span> <span data-ttu-id="30f94-112">Vous pouvez rapidement créer et attacher un disque géré à l’aide de machine virtuelle tooa hello même groupe de ressources Azure, ou vous pouvez créer n’importe quel nombre de disques et définissez-les.</span><span class="sxs-lookup"><span data-stu-id="30f94-112">You can quickly create and attach a managed disk tooa VM using hello same Azure resource group, or you can create any number of disks and then attach them.</span></span>


### <a name="attach-a-new-disk-tooa-vm"></a><span data-ttu-id="30f94-113">Attacher un tooa disque nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="30f94-113">Attach a new disk tooa VM</span></span>

<span data-ttu-id="30f94-114">Si vous devez simplement un nouveau disque sur votre machine virtuelle, vous pouvez utiliser hello `az vm disk attach` commande.</span><span class="sxs-lookup"><span data-stu-id="30f94-114">If you just need a new disk on your VM, you can use hello `az vm disk attach` command.</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a><span data-ttu-id="30f94-115">Association d'un disque existant</span><span class="sxs-lookup"><span data-stu-id="30f94-115">Attach an existing disk</span></span> 

<span data-ttu-id="30f94-116">Dans de nombreux cas, vous attachez des disques qui ont déjà été créés.</span><span class="sxs-lookup"><span data-stu-id="30f94-116">In many cases you attach disks that have already been created.</span></span> <span data-ttu-id="30f94-117">Tout d’abord rechercher les id de disque hello et la transmettez ce toohello `az vm disk attach` commande.</span><span class="sxs-lookup"><span data-stu-id="30f94-117">You first find hello disk id and then pass that toohello `az vm disk attach` command.</span></span> <span data-ttu-id="30f94-118">Hello exemple suivant utilise un disque créé avec `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span><span class="sxs-lookup"><span data-stu-id="30f94-118">hello following example uses a disk created with `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span></span>

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

<span data-ttu-id="30f94-119">Hello sortie ressemble à hello suivante (vous pouvez utiliser hello `-o table` option tooany tooformat hello saisies dans) :</span><span class="sxs-lookup"><span data-stu-id="30f94-119">hello output looks something like hello following (you can use hello `-o table` option tooany command tooformat hello output in ):</span></span>

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


## <a name="attach-an-unmanaged-disk"></a><span data-ttu-id="30f94-120">Attacher un disque non géré</span><span class="sxs-lookup"><span data-stu-id="30f94-120">Attach an unmanaged disk</span></span>

<span data-ttu-id="30f94-121">Attacher un disque est rapide si vous occupez pas de création d’un disque Bonjour même compte de stockage que votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="30f94-121">Attaching a new disk is quick if you do not mind creating a disk in hello same storage account as your VM.</span></span> <span data-ttu-id="30f94-122">Type `azure vm disk attach-new` toocreate et attacher un disque Go pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="30f94-122">Type `azure vm disk attach-new` toocreate and attach a new GB disk for your VM.</span></span> <span data-ttu-id="30f94-123">Si vous n’identifiez pas explicitement d’un compte de stockage, n’importe quel disque que vous créez se trouve dans hello même compte de stockage où se trouve le disque du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="30f94-123">If you do not explicitly identify a storage account, any disk you create is placed in hello same storage account where your OS disk resides.</span></span> <span data-ttu-id="30f94-124">Hello suivants exemple attache un `50`Go disque toohello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="30f94-124">hello following example attaches a `50`GB disk toohello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a><span data-ttu-id="30f94-125">Se connecter toohello nouveau disque Linux VM toomount hello</span><span class="sxs-lookup"><span data-stu-id="30f94-125">Connect toohello Linux VM toomount hello new disk</span></span>
> [!NOTE]
> <span data-ttu-id="30f94-126">Cette rubrique connecte tooa machine virtuelle à l’aide des noms d’utilisateur et mots de passe.</span><span class="sxs-lookup"><span data-stu-id="30f94-126">This topic connects tooa VM using usernames and passwords.</span></span> <span data-ttu-id="30f94-127">toocommunicate de paires de clés publiques et privées toouse avec votre machine virtuelle, consultez [comment tooUse SSH avec Linux sur Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="30f94-127">toouse public and private key pairs toocommunicate with your VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
> 
> 

<span data-ttu-id="30f94-128">Vous devez tooSSH dans votre machine virtuelle Azure toopartition, mettre en forme et monter votre nouveau disque votre VM Linux peut l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="30f94-128">You need tooSSH into your Azure VM toopartition, format, and mount your new disk so your Linux VM can use it.</span></span> <span data-ttu-id="30f94-129">Si vous n’êtes pas familiarisé avec la connexion avec **ssh**, commande hello prend la forme de hello `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`et l’aspect de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="30f94-129">If you're not familiar with connecting with **ssh**, hello command takes hello form `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`, and looks like hello following:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

<span data-ttu-id="30f94-130">Sortie</span><span class="sxs-lookup"><span data-stu-id="30f94-130">Output</span></span>

```bash
hello authenticity of host 'mypublicdns.westus.cloudapp.azure.com (191.239.51.1)' can't be established.
ECDSA key fingerprint is bx:xx:xx:xx:xx:xx:xx:xx:xx:x:x:x:x:x:x:xx.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.westus.cloudapp.azure.com,191.239.51.1' (ECDSA) toohello list of known hosts.
ops@mypublicdns.westus.cloudapp.azure.com's password:
Welcome tooUbuntu 14.04.2 LTS (GNU/Linux 3.16.0-37-generic x86_64)

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

hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

ops@myVM:~$
```

<span data-ttu-id="30f94-131">Maintenant que vous êtes connecté tooyour machine virtuelle, vous êtes prêt tooattach un disque.</span><span class="sxs-lookup"><span data-stu-id="30f94-131">Now that you're connected tooyour VM, you're ready tooattach a disk.</span></span>  <span data-ttu-id="30f94-132">Tout d’abord rechercher hello sur le disque, à l’aide de `dmesg | grep SCSI` (méthode hello vous utilisez toodiscover votre nouveau disque peut-être varier).</span><span class="sxs-lookup"><span data-stu-id="30f94-132">First find hello disk, using `dmesg | grep SCSI` (hello method you use toodiscover your new disk may vary).</span></span> <span data-ttu-id="30f94-133">Le résultat est alors le suivant :</span><span class="sxs-lookup"><span data-stu-id="30f94-133">In this case, it looks something like:</span></span>

```bash
dmesg | grep SCSI
```

<span data-ttu-id="30f94-134">Sortie</span><span class="sxs-lookup"><span data-stu-id="30f94-134">Output</span></span>

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

<span data-ttu-id="30f94-135">et dans les cas de hello de cette rubrique, hello `sdc` disque est hello celui escompté.</span><span class="sxs-lookup"><span data-stu-id="30f94-135">and in hello case of this topic, hello `sdc` disk is hello one that we want.</span></span> <span data-ttu-id="30f94-136">Maintenant la partition hello disque avec `sudo fdisk /dev/sdc` --en supposant que dans votre cas hello disque a été `sdc`, rendre un disque principal sur la partition 1 et acceptez hello autres valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="30f94-136">Now partition hello disk with `sudo fdisk /dev/sdc` -- assuming that in your case hello disk was `sdc`, and make it a primary disk on partition 1, and accept hello other defaults.</span></span>

```bash
sudo fdisk /dev/sdc
```

<span data-ttu-id="30f94-137">Sortie</span><span class="sxs-lookup"><span data-stu-id="30f94-137">Output</span></span>

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide toowrite them.
After that, of course, hello previous content won't be recoverable.

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

<span data-ttu-id="30f94-138">Créer la partition de hello en tapant `p` invite hello :</span><span class="sxs-lookup"><span data-stu-id="30f94-138">Create hello partition by typing `p` at hello prompt:</span></span>

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
hello partition table has been altered!

Calling ioctl() toore-read partition table.
Syncing disks.
```

<span data-ttu-id="30f94-139">Et d’écriture d’une partition toohello à l’aide de hello **mkfs** commande, en spécifiant le nom du périphérique hello et de type de système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="30f94-139">And write a file system toohello partition by using hello **mkfs** command, specifying your filesystem type and hello device name.</span></span> <span data-ttu-id="30f94-140">Dans cette rubrique, nous utilisons `ext4` et `/dev/sdc1` (voir ci-dessus) :</span><span class="sxs-lookup"><span data-stu-id="30f94-140">In this topic, we're using `ext4` and `/dev/sdc1` from above:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="30f94-141">Sortie</span><span class="sxs-lookup"><span data-stu-id="30f94-141">Output</span></span>

```bash
mke2fs 1.42.9 (4-Feb-2014)
Discarding device blocks: done
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
327680 inodes, 1310464 blocks
65523 blocks (5.00%) reserved for hello super user
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

<span data-ttu-id="30f94-142">Maintenant nous créons un répertoire toomount hello fichier système en utilisant `mkdir`:</span><span class="sxs-lookup"><span data-stu-id="30f94-142">Now we create a directory toomount hello file system using `mkdir`:</span></span>

```bash
sudo mkdir /datadrive
```

<span data-ttu-id="30f94-143">Et vous montez à l’aide du répertoire hello `mount`:</span><span class="sxs-lookup"><span data-stu-id="30f94-143">And you mount hello directory using `mount`:</span></span>

```bash
sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="30f94-144">Hello disque de données est maintenant prêt toouse comme `/datadrive`.</span><span class="sxs-lookup"><span data-stu-id="30f94-144">hello data disk is now ready toouse as `/datadrive`.</span></span>

```bash
ls
```

<span data-ttu-id="30f94-145">Sortie</span><span class="sxs-lookup"><span data-stu-id="30f94-145">Output</span></span>

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

<span data-ttu-id="30f94-146">lecteur de hello tooensure est remontée automatiquement après qu’un redémarrage, qu'il doit être ajouté le fichier/etc/fstab de toohello.</span><span class="sxs-lookup"><span data-stu-id="30f94-146">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="30f94-147">En outre, il est fortement recommandé que hello UUID (universellement Unique IDentifier) est utilisé dans/etc/fstab toorefer toohello lecteur au lieu du nom du périphérique hello simplement (tel que `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="30f94-147">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (such as, `/dev/sdc1`).</span></span> <span data-ttu-id="30f94-148">Si hello du système d’exploitation détecte une erreur de disque au cours du démarrage, à l’aide de hello UUID évite hello incorrect disque monté tooa un emplacement donné.</span><span class="sxs-lookup"><span data-stu-id="30f94-148">If hello OS detects a disk error during boot, using hello UUID avoids hello incorrect disk being mounted tooa given location.</span></span> <span data-ttu-id="30f94-149">Les disques de données restants reçoivent alors les mêmes ID d’appareil.</span><span class="sxs-lookup"><span data-stu-id="30f94-149">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="30f94-150">toofind hello UUID du nouveau lecteur de hello, utilisez hello **blkid** utilitaire :</span><span class="sxs-lookup"><span data-stu-id="30f94-150">toofind hello UUID of hello new drive, use hello **blkid** utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="30f94-151">sortie de Hello recherche similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="30f94-151">hello output looks similar toohello following:</span></span>

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> <span data-ttu-id="30f94-152">Mal modification hello **/etc/fstab** fichier peut entraîner un système non démarrable.</span><span class="sxs-lookup"><span data-stu-id="30f94-152">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="30f94-153">En cas de doute, consultez la documentation de la distribution toohello pour plus d’informations sur la façon dont tooproperly modifier ce fichier.</span><span class="sxs-lookup"><span data-stu-id="30f94-153">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="30f94-154">Il est également recommandé qu’une sauvegarde de fichier/etc/fstab de hello est créée avant la modification.</span><span class="sxs-lookup"><span data-stu-id="30f94-154">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>
> 
> 

<span data-ttu-id="30f94-155">Ensuite, ouvrez hello **/etc/fstab** fichier dans un éditeur de texte :</span><span class="sxs-lookup"><span data-stu-id="30f94-155">Next, open hello **/etc/fstab** file in a text editor:</span></span>

```bash
sudo vi /etc/fstab
```

<span data-ttu-id="30f94-156">Dans cet exemple, nous utilisons valeur UUID de hello pour hello nouvelle **/dev/sdc1** périphérique qui a été créé dans les étapes précédentes hello et point de montage hello **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="30f94-156">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="30f94-157">Ajouter hello suivant la fin ligne toohello Hello **/etc/fstab** fichier :</span><span class="sxs-lookup"><span data-stu-id="30f94-157">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> <span data-ttu-id="30f94-158">Suppression d’un disque de données ultérieurement sans avoir à modifier fstab peut entraîner hello VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="30f94-158">Later removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="30f94-159">La plupart des distributions fournissent soit hello `nofail` et/ou `nobootwait` fstab options.</span><span class="sxs-lookup"><span data-stu-id="30f94-159">Most distributions provide either hello `nofail` and/or `nobootwait` fstab options.</span></span> <span data-ttu-id="30f94-160">Ces options permettent une tooboot système même en cas de disque de hello toomount au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="30f94-160">These options allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="30f94-161">Pour plus d’informations sur ces paramètres, consultez la documentation de votre distribution.</span><span class="sxs-lookup"><span data-stu-id="30f94-161">Consult your distribution's documentation for more information on these parameters.</span></span>
> 
> <span data-ttu-id="30f94-162">Hello **nofail** option garantit que hello machine virtuelle démarre, même si le système de fichiers hello est endommagé ou disque de hello n’existe pas au moment du démarrage.</span><span class="sxs-lookup"><span data-stu-id="30f94-162">hello **nofail** option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="30f94-163">Sans cette option, vous pouvez rencontrer le problème comme décrit dans [ne peut pas SSH tooLinux machine virtuelle en raison d’erreurs de tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span><span class="sxs-lookup"><span data-stu-id="30f94-163">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="30f94-164">Prise en charge de TRIM/UNMAP pour Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="30f94-164">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="30f94-165">Certains noyaux Linux prend en charge TRIM/annuler le mappage operations toodiscard les blocs inutilisés sur le disque de hello.</span><span class="sxs-lookup"><span data-stu-id="30f94-165">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="30f94-166">Cela est surtout utile dans tooinform standard de stockage Azure qui pages supprimées ne sont plus valides et peuvent être ignorées.</span><span class="sxs-lookup"><span data-stu-id="30f94-166">This is primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="30f94-167">Vous pouvez ainsi faire des économies si vous créez des fichiers volumineux, puis les supprimez.</span><span class="sxs-lookup"><span data-stu-id="30f94-167">This can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="30f94-168">Il existe deux façons tooenable TRIM prend en charge dans votre VM Linux.</span><span class="sxs-lookup"><span data-stu-id="30f94-168">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="30f94-169">Comme d’habitude, consultez votre distribution pour hello approche recommandée :</span><span class="sxs-lookup"><span data-stu-id="30f94-169">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="30f94-170">Hello d’utilisation `discard` monter option dans `/etc/fstab`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="30f94-170">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* <span data-ttu-id="30f94-171">Dans certains hello cas `discard` option peut avoir des conséquences sur les performances.</span><span class="sxs-lookup"><span data-stu-id="30f94-171">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="30f94-172">Vous pouvez également exécuter hello `fstrim` commande manuellement à partir de la ligne de commande hello ou ajoutez-le tooyour crontab toorun régulièrement :</span><span class="sxs-lookup"><span data-stu-id="30f94-172">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="30f94-173">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="30f94-173">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="30f94-174">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="30f94-174">**RHEL/CentOS**</span></span>

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="30f94-175">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="30f94-175">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="30f94-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="30f94-176">Next Steps</span></span>
* <span data-ttu-id="30f94-177">N’oubliez pas que votre nouveau disque n’est pas disponible toohello machine virtuelle si elle redémarre, sauf si vous écrivez ce tooyour informations [fstab](http://en.wikipedia.org/wiki/Fstab) fichier.</span><span class="sxs-lookup"><span data-stu-id="30f94-177">Remember, that your new disk is not available toohello VM if it reboots unless you write that information tooyour [fstab](http://en.wikipedia.org/wiki/Fstab) file.</span></span>
* <span data-ttu-id="30f94-178">tooensure votre VM Linux est configuré correctement, examinez hello [optimiser les performances de votre ordinateur Linux](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recommandations.</span><span class="sxs-lookup"><span data-stu-id="30f94-178">tooensure your Linux VM is configured correctly, review hello [Optimize your Linux machine performance](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recommendations.</span></span>
* <span data-ttu-id="30f94-179">Développez votre capacité de stockage en ajoutant des disques supplémentaires et [configurez RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour augmenter les performances.</span><span class="sxs-lookup"><span data-stu-id="30f94-179">Expand your storage capacity by adding additional disks and [configure RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional performance.</span></span>

