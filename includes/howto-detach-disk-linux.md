<span data-ttu-id="4f5d6-101">Lorsque vous n’avez plus besoin un disque de données est attachée tooa virtual machine (VM), vous pouvez facilement la détacher.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-101">When you no longer need a data disk that's attached tooa virtual machine (VM), you can easily detach it.</span></span> <span data-ttu-id="4f5d6-102">Lorsque vous détachez un disque à partir de la machine virtuelle de hello, disque de hello n’est pas supprimé de stockage.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-102">When you detach a disk from hello VM, hello disk is not removed it from storage.</span></span> <span data-ttu-id="4f5d6-103">Si vous souhaitez toouse hello données existantes hello disque à nouveau, vous pouvez rattacher il toohello même machine virtuelle, ou un autre.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same VM, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="4f5d6-104">Dans Azure, une machine virtuelle utilise différents types de disque, comme le disque du système d’exploitation, un disque temporaire local et des disques de données facultatifs.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-104">A VM in Azure uses different types of disks - an operating system disk, a local temporary disk, and optional data disks.</span></span> <span data-ttu-id="4f5d6-105">Pour plus d’informations, consultez l’article [À propos des disques et VHD pour machines virtuelles](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4f5d6-105">For details, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4f5d6-106">Impossible de détacher un disque de système d’exploitation, sauf si vous supprimez également hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-106">You cannot detach an operating system disk unless you also delete hello VM.</span></span>

## <a name="find-hello-disk"></a><span data-ttu-id="4f5d6-107">Trouver de disque de hello</span><span class="sxs-lookup"><span data-stu-id="4f5d6-107">Find hello disk</span></span>
<span data-ttu-id="4f5d6-108">Avant de pouvoir détacher un disque à partir d’une machine virtuelle, vous devez toofind out hello numéro LUN, ce qui est un identificateur de toobe de disque hello détachée.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-108">Before you can detach a disk from a VM you need toofind out hello LUN number, which is an identifier for hello disk toobe detached.</span></span> <span data-ttu-id="4f5d6-109">toodo qui, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4f5d6-109">toodo that, follow these steps:</span></span>

1. <span data-ttu-id="4f5d6-110">Ouvrez CLI d’Azure et [connecter tooyour abonnement Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="4f5d6-110">Open Azure CLI and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="4f5d6-111">Assurez-vous que vous êtes en mode Azure Service Management (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="4f5d6-111">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="4f5d6-112">Découvrez quels sont les disques attaché tooyour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-112">Find out which disks are attached tooyour VM.</span></span> <span data-ttu-id="4f5d6-113">Hello exemple suivant répertorie les disques pour hello ordinateur virtuel nommé `myVM`:</span><span class="sxs-lookup"><span data-stu-id="4f5d6-113">hello following example lists disks for hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="4f5d6-114">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="4f5d6-114">hello output is similar toohello following example:</span></span>

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

3. <span data-ttu-id="4f5d6-115">Remarque : hello numéro d’unité logique ou hello **numéro d’unité logique** pour disque hello que vous souhaitez toodetach.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-115">Note hello LUN or hello **logical unit number** for hello disk that you want toodetach.</span></span>

## <a name="remove-operating-system-references-toohello-disk"></a><span data-ttu-id="4f5d6-116">Supprimer le disque de système d’exploitation références toohello</span><span class="sxs-lookup"><span data-stu-id="4f5d6-116">Remove operating system references toohello disk</span></span>
<span data-ttu-id="4f5d6-117">Avant de détacher le disque hello Bonjour Linux invité, vous devez vous assurer que toutes les partitions sur le disque de hello ne sont pas en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-117">Before detaching hello disk from hello Linux guest, you should make sure that all partitions on hello disk are not in use.</span></span> <span data-ttu-id="4f5d6-118">Vérifiez le système d’exploitation hello n’essaie pas de tooremount après un redémarrage.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-118">Ensure that hello operating system does not attempt tooremount them after a reboot.</span></span> <span data-ttu-id="4f5d6-119">Ces étapes Annuler configuration hello vous avez probablement créé lorsque [attachement](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) disque de hello.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-119">These steps undo hello configuration you likely created when [attaching](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello disk.</span></span>

1. <span data-ttu-id="4f5d6-120">Hello d’utilisation `lsscsi` identificateur de disque commande toodiscover hello.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-120">Use hello `lsscsi` command toodiscover hello disk identifier.</span></span> <span data-ttu-id="4f5d6-121">`lsscsi` peut être installé par `yum install lsscsi` (dans des distributions Red Hat) ou `apt-get install lsscsi` (dans des distributions Debian).</span><span class="sxs-lookup"><span data-stu-id="4f5d6-121">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="4f5d6-122">Vous pouvez trouver l’identificateur de disque hello que vous cherchez à l’aide du numéro d’unité logique hello.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-122">You can find hello disk identifier you are looking for by using hello LUN number.</span></span> <span data-ttu-id="4f5d6-123">dernier numéro de tuple hello dans chaque ligne Hello est hello numéro d’unité logique.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-123">hello last number in hello tuple in each row is hello LUN.</span></span> <span data-ttu-id="4f5d6-124">Bonjour à partir de l’exemple suivant `lsscsi`, LUN 0 mappe trop  */dev/sdc*</span><span class="sxs-lookup"><span data-stu-id="4f5d6-124">In hello following example from `lsscsi`, LUN 0 maps too*/dev/sdc*</span></span>

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. <span data-ttu-id="4f5d6-125">Utilisez `fdisk -l <disk>` partitions de hello toodiscover associées toobe de disque hello détachée.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-125">Use `fdisk -l <disk>` toodiscover hello partitions associated with hello disk toobe detached.</span></span> <span data-ttu-id="4f5d6-126">exemple Hello présente sortie hello pour `/dev/sdc`:</span><span class="sxs-lookup"><span data-stu-id="4f5d6-126">hello following example shows hello output for `/dev/sdc`:</span></span>

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

3. <span data-ttu-id="4f5d6-127">Démontez chaque partition répertoriée pour le disque de hello.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-127">Unmount each partition listed for hello disk.</span></span> <span data-ttu-id="4f5d6-128">démonte Hello exemple `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="4f5d6-128">hello following example unmounts `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

4. <span data-ttu-id="4f5d6-129">Hello d’utilisation `blkid` commande toodiscovery hello UUID pour toutes les partitions.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-129">Use hello `blkid` command toodiscovery hello UUIDs for all partitions.</span></span> <span data-ttu-id="4f5d6-130">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="4f5d6-130">hello output is similar toohello following example:</span></span>

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. <span data-ttu-id="4f5d6-131">Supprimer les entrées dans hello **/etc/fstab** fichier associée à chemins d’accès de périphérique hello ou UUID pour toutes les partitions pour hello disque toobe est détachée.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-131">Remove entries in hello **/etc/fstab** file associated with either hello device paths or UUIDs for all partitions for hello disk toobe detached.</span></span>  <span data-ttu-id="4f5d6-132">Pour cet exemple, les entrées peuvent être les suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f5d6-132">Entries for this example might be:</span></span>

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    <span data-ttu-id="4f5d6-133">ou</span><span class="sxs-lookup"><span data-stu-id="4f5d6-133">or</span></span>
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a><span data-ttu-id="4f5d6-134">Détacher un disque de hello</span><span class="sxs-lookup"><span data-stu-id="4f5d6-134">Detach hello disk</span></span>
<span data-ttu-id="4f5d6-135">Après avoir trouvé le nombre de numéro d’unité logique de hello de disque de hello et références de système d’exploitation hello supprimé, vous êtes prêt toodetach il :</span><span class="sxs-lookup"><span data-stu-id="4f5d6-135">After you find hello LUN number of hello disk and removed hello operating system references, you're ready toodetach it:</span></span>

1. <span data-ttu-id="4f5d6-136">Détachement du disque sélectionné de hello à partir de l’ordinateur virtuel de hello en exécutant la commande hello `azure vm disk detach
   <virtual-machine-name> <LUN>`.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-136">Detach hello selected disk from hello virtual machine by running hello command `azure vm disk detach
<virtual-machine-name> <LUN>`.</span></span> <span data-ttu-id="4f5d6-137">exemple Hello détache LUN `0` de hello ordinateur virtuel nommé `myVM`:</span><span class="sxs-lookup"><span data-stu-id="4f5d6-137">hello following example detaches LUN `0` from hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. <span data-ttu-id="4f5d6-138">Vous pouvez vérifier si le disque de hello est détaché en exécutant `azure vm disk list` à nouveau.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-138">You can check if hello disk got detached by running `azure vm disk list` again.</span></span> <span data-ttu-id="4f5d6-139">Hello contrôles de l’exemple hello ordinateur virtuel nommé `myVM`:</span><span class="sxs-lookup"><span data-stu-id="4f5d6-139">hello following example checks hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="4f5d6-140">la sortie est similaire toohello suivant exemple, qui illustre le disque de données hello n’est plus attaché Hello :</span><span class="sxs-lookup"><span data-stu-id="4f5d6-140">hello output is similar toohello following example, which shows hello data disk is no longer attached:</span></span>

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

<span data-ttu-id="4f5d6-141">disque de Hello détachée reste dans le stockage, mais n’est plus attaché tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="4f5d6-141">hello detached disk remains in storage but is no longer attached tooa virtual machine.</span></span>

