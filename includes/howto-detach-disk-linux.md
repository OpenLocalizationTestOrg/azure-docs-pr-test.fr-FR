Lorsque vous n’avez plus besoin un disque de données est attachée tooa virtual machine (VM), vous pouvez facilement la détacher. Lorsque vous détachez un disque à partir de la machine virtuelle de hello, disque de hello n’est pas supprimé de stockage. Si vous souhaitez toouse hello données existantes hello disque à nouveau, vous pouvez rattacher il toohello même machine virtuelle, ou un autre.  

> [!NOTE]
> Dans Azure, une machine virtuelle utilise différents types de disque, comme le disque du système d’exploitation, un disque temporaire local et des disques de données facultatifs. Pour plus d’informations, consultez l’article [À propos des disques et VHD pour machines virtuelles](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Impossible de détacher un disque de système d’exploitation, sauf si vous supprimez également hello machine virtuelle.

## <a name="find-hello-disk"></a>Trouver de disque de hello
Avant de pouvoir détacher un disque à partir d’une machine virtuelle, vous devez toofind out hello numéro LUN, ce qui est un identificateur de toobe de disque hello détachée. toodo qui, procédez comme suit :

1. Ouvrez CLI d’Azure et [connecter tooyour abonnement Azure](../articles/xplat-cli-connect.md). Assurez-vous que vous êtes en mode Azure Service Management (`azure config mode asm`).
2. Découvrez quels sont les disques attaché tooyour machine virtuelle. Hello exemple suivant répertorie les disques pour hello ordinateur virtuel nommé `myVM`:

    ```azurecli
    azure vm disk list myVM
    ```

    Hello la sortie est similaire toohello l’exemple suivant :

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. Remarque : hello numéro d’unité logique ou hello **numéro d’unité logique** pour disque hello que vous souhaitez toodetach.

## <a name="remove-operating-system-references-toohello-disk"></a>Supprimer le disque de système d’exploitation références toohello
Avant de détacher le disque hello Bonjour Linux invité, vous devez vous assurer que toutes les partitions sur le disque de hello ne sont pas en cours d’utilisation. Vérifiez le système d’exploitation hello n’essaie pas de tooremount après un redémarrage. Ces étapes Annuler configuration hello vous avez probablement créé lorsque [attachement](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) disque de hello.

1. Hello d’utilisation `lsscsi` identificateur de disque commande toodiscover hello. `lsscsi` peut être installé par `yum install lsscsi` (dans des distributions Red Hat) ou `apt-get install lsscsi` (dans des distributions Debian). Vous pouvez trouver l’identificateur de disque hello que vous cherchez à l’aide du numéro d’unité logique hello. dernier numéro de tuple hello dans chaque ligne Hello est hello numéro d’unité logique. Bonjour à partir de l’exemple suivant `lsscsi`, LUN 0 mappe trop  */dev/sdc*

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. Utilisez `fdisk -l <disk>` partitions de hello toodiscover associées toobe de disque hello détachée. exemple Hello présente sortie hello pour `/dev/sdc`:

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. Démontez chaque partition répertoriée pour le disque de hello. démonte Hello exemple `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

4. Hello d’utilisation `blkid` commande toodiscovery hello UUID pour toutes les partitions. Hello la sortie est similaire toohello l’exemple suivant :

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. Supprimer les entrées dans hello **/etc/fstab** fichier associée à chemins d’accès de périphérique hello ou UUID pour toutes les partitions pour hello disque toobe est détachée.  Pour cet exemple, les entrées peuvent être les suivantes :

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    ou
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a>Détacher un disque de hello
Après avoir trouvé le nombre de numéro d’unité logique de hello de disque de hello et références de système d’exploitation hello supprimé, vous êtes prêt toodetach il :

1. Détachement du disque sélectionné de hello à partir de l’ordinateur virtuel de hello en exécutant la commande hello `azure vm disk detach
   <virtual-machine-name> <LUN>`. exemple Hello détache LUN `0` de hello ordinateur virtuel nommé `myVM`:
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. Vous pouvez vérifier si le disque de hello est détaché en exécutant `azure vm disk list` à nouveau. Hello contrôles de l’exemple hello ordinateur virtuel nommé `myVM`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    la sortie est similaire toohello suivant exemple, qui illustre le disque de données hello n’est plus attaché Hello :

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

disque de Hello détachée reste dans le stockage, mais n’est plus attaché tooa virtual machine.

