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
# <a name="add-a-disk-tooa-linux-vm"></a>Ajouter un tooa de disque Linux VM
Cet article explique tooattach un persistant de disque tooyour VM afin que vous pouvez conserver vos données : même si votre machine virtuelle est remise en service en raison de toomaintenance ou redimensionnement. 

## <a name="quick-commands"></a>Commandes rapides
Hello suivants exemple attache un `50`Go disque toohello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:

toouse des disques gérés :

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

disques toouse non managée :

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a>Attacher un disque géré

L’utilisation de disques gérés vous permet toofocus sur vos machines virtuelles et leurs disques sans vous préoccuper des comptes de stockage Azure. Vous pouvez rapidement créer et attacher un disque géré à l’aide de machine virtuelle tooa hello même groupe de ressources Azure, ou vous pouvez créer n’importe quel nombre de disques et définissez-les.


### <a name="attach-a-new-disk-tooa-vm"></a>Attacher un tooa disque nouvelle machine virtuelle

Si vous devez simplement un nouveau disque sur votre machine virtuelle, vous pouvez utiliser hello `az vm disk attach` commande.

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a>Association d'un disque existant 

Dans de nombreux cas, vous attachez des disques qui ont déjà été créés. Tout d’abord rechercher les id de disque hello et la transmettez ce toohello `az vm disk attach` commande. Hello exemple suivant utilise un disque créé avec `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

Hello sortie ressemble à hello suivante (vous pouvez utiliser hello `-o table` option tooany tooformat hello saisies dans) :

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


## <a name="attach-an-unmanaged-disk"></a>Attacher un disque non géré

Attacher un disque est rapide si vous occupez pas de création d’un disque Bonjour même compte de stockage que votre machine virtuelle. Type `azure vm disk attach-new` toocreate et attacher un disque Go pour votre machine virtuelle. Si vous n’identifiez pas explicitement d’un compte de stockage, n’importe quel disque que vous créez se trouve dans hello même compte de stockage où se trouve le disque du système d’exploitation. Hello suivants exemple attache un `50`Go disque toohello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a>Se connecter toohello nouveau disque Linux VM toomount hello
> [!NOTE]
> Cette rubrique connecte tooa machine virtuelle à l’aide des noms d’utilisateur et mots de passe. toocommunicate de paires de clés publiques et privées toouse avec votre machine virtuelle, consultez [comment tooUse SSH avec Linux sur Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
> 
> 

Vous devez tooSSH dans votre machine virtuelle Azure toopartition, mettre en forme et monter votre nouveau disque votre VM Linux peut l’utiliser. Si vous n’êtes pas familiarisé avec la connexion avec **ssh**, commande hello prend la forme de hello `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`et l’aspect de hello suivantes :

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

Sortie

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

Maintenant que vous êtes connecté tooyour machine virtuelle, vous êtes prêt tooattach un disque.  Tout d’abord rechercher hello sur le disque, à l’aide de `dmesg | grep SCSI` (méthode hello vous utilisez toodiscover votre nouveau disque peut-être varier). Le résultat est alors le suivant :

```bash
dmesg | grep SCSI
```

Sortie

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

et dans les cas de hello de cette rubrique, hello `sdc` disque est hello celui escompté. Maintenant la partition hello disque avec `sudo fdisk /dev/sdc` --en supposant que dans votre cas hello disque a été `sdc`, rendre un disque principal sur la partition 1 et acceptez hello autres valeurs par défaut.

```bash
sudo fdisk /dev/sdc
```

Sortie

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

Créer la partition de hello en tapant `p` invite hello :

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

Et d’écriture d’une partition toohello à l’aide de hello **mkfs** commande, en spécifiant le nom du périphérique hello et de type de système de fichiers. Dans cette rubrique, nous utilisons `ext4` et `/dev/sdc1` (voir ci-dessus) :

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Sortie

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

Maintenant nous créons un répertoire toomount hello fichier système en utilisant `mkdir`:

```bash
sudo mkdir /datadrive
```

Et vous montez à l’aide du répertoire hello `mount`:

```bash
sudo mount /dev/sdc1 /datadrive
```

Hello disque de données est maintenant prêt toouse comme `/datadrive`.

```bash
ls
```

Sortie

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

lecteur de hello tooensure est remontée automatiquement après qu’un redémarrage, qu'il doit être ajouté le fichier/etc/fstab de toohello. En outre, il est fortement recommandé que hello UUID (universellement Unique IDentifier) est utilisé dans/etc/fstab toorefer toohello lecteur au lieu du nom du périphérique hello simplement (tel que `/dev/sdc1`). Si hello du système d’exploitation détecte une erreur de disque au cours du démarrage, à l’aide de hello UUID évite hello incorrect disque monté tooa un emplacement donné. Les disques de données restants reçoivent alors les mêmes ID d’appareil. toofind hello UUID du nouveau lecteur de hello, utilisez hello **blkid** utilitaire :

```bash
sudo -i blkid
```

sortie de Hello recherche similaire toohello suivantes :

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> Mal modification hello **/etc/fstab** fichier peut entraîner un système non démarrable. En cas de doute, consultez la documentation de la distribution toohello pour plus d’informations sur la façon dont tooproperly modifier ce fichier. Il est également recommandé qu’une sauvegarde de fichier/etc/fstab de hello est créée avant la modification.
> 
> 

Ensuite, ouvrez hello **/etc/fstab** fichier dans un éditeur de texte :

```bash
sudo vi /etc/fstab
```

Dans cet exemple, nous utilisons valeur UUID de hello pour hello nouvelle **/dev/sdc1** périphérique qui a été créé dans les étapes précédentes hello et point de montage hello **/datadrive**. Ajouter hello suivant la fin ligne toohello Hello **/etc/fstab** fichier :

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> Suppression d’un disque de données ultérieurement sans avoir à modifier fstab peut entraîner hello VM toofail tooboot. La plupart des distributions fournissent soit hello `nofail` et/ou `nobootwait` fstab options. Ces options permettent une tooboot système même en cas de disque de hello toomount au moment du démarrage. Pour plus d’informations sur ces paramètres, consultez la documentation de votre distribution.
> 
> Hello **nofail** option garantit que hello machine virtuelle démarre, même si le système de fichiers hello est endommagé ou disque de hello n’existe pas au moment du démarrage. Sans cette option, vous pouvez rencontrer le problème comme décrit dans [ne peut pas SSH tooLinux machine virtuelle en raison d’erreurs de tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)

### <a name="trimunmap-support-for-linux-in-azure"></a>Prise en charge de TRIM/UNMAP pour Linux dans Azure
Certains noyaux Linux prend en charge TRIM/annuler le mappage operations toodiscard les blocs inutilisés sur le disque de hello. Cela est surtout utile dans tooinform standard de stockage Azure qui pages supprimées ne sont plus valides et peuvent être ignorées. Vous pouvez ainsi faire des économies si vous créez des fichiers volumineux, puis les supprimez.

Il existe deux façons tooenable TRIM prend en charge dans votre VM Linux. Comme d’habitude, consultez votre distribution pour hello approche recommandée :

* Hello d’utilisation `discard` monter option dans `/etc/fstab`, par exemple :

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* Dans certains hello cas `discard` option peut avoir des conséquences sur les performances. Vous pouvez également exécuter hello `fstrim` commande manuellement à partir de la ligne de commande hello ou ajoutez-le tooyour crontab toorun régulièrement :
  
    **Ubuntu**
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    **RHEL/CentOS**

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a>Résolution des problèmes
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Étapes suivantes
* N’oubliez pas que votre nouveau disque n’est pas disponible toohello machine virtuelle si elle redémarre, sauf si vous écrivez ce tooyour informations [fstab](http://en.wikipedia.org/wiki/Fstab) fichier.
* tooensure votre VM Linux est configuré correctement, examinez hello [optimiser les performances de votre ordinateur Linux](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recommandations.
* Développez votre capacité de stockage en ajoutant des disques supplémentaires et [configurez RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour augmenter les performances.

