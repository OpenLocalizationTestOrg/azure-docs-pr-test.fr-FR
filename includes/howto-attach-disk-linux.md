
<span data-ttu-id="0193e-101">Pour plus d’informations sur les disques, consultez l’article [À propos des disques et VHD pour machines virtuelles](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0193e-101">For more information about disks, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a><span data-ttu-id="0193e-102">Attacher un disque vide</span><span class="sxs-lookup"><span data-stu-id="0193e-102">Attach an empty disk</span></span>
1. <span data-ttu-id="0193e-103">Ouvrez Azure CLI 1.0 et [connecter tooyour abonnement Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="0193e-103">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="0193e-104">Assurez-vous que vous êtes en mode Azure Service Management (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="0193e-104">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="0193e-105">Entrez `azure vm disk attach-new` toocreate et connectez un nouveau disque, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="0193e-105">Enter `azure vm disk attach-new` toocreate and attach a new disk as shown in hello following example.</span></span> <span data-ttu-id="0193e-106">Remplacez *myVM* avec le nom hello de votre Machine virtuelle de Linux et spécifiez la taille hello du disque de hello en Go, ce qui est *100 Go* dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="0193e-106">Replace *myVM* with hello name of your Linux Virtual Machine and specify hello size of hello disk in GB, which is *100GB* in this example:</span></span>

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. <span data-ttu-id="0193e-107">Une fois le disque de données hello est créé et attaché, il est répertorié dans la sortie de hello de `azure vm disk list <virtual-machine-name>` comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0193e-107">After hello data disk is created and attached, it's listed in hello output of `azure vm disk list <virtual-machine-name>` as shown in hello following example:</span></span>
   
    ```azurecli
    azure vm disk list TestVM
    ```

    <span data-ttu-id="0193e-108">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0193e-108">hello output is similar toohello following example:</span></span>

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a><span data-ttu-id="0193e-109">Association d'un disque existant</span><span class="sxs-lookup"><span data-stu-id="0193e-109">Attach an existing disk</span></span>
<span data-ttu-id="0193e-110">Pour attacher un disque existant, vous devez disposer d’un fichier .vhd dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0193e-110">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span>

1. <span data-ttu-id="0193e-111">Ouvrez Azure CLI 1.0 et [connecter tooyour abonnement Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="0193e-111">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="0193e-112">Assurez-vous que vous êtes en mode Azure Service Management (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="0193e-112">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="0193e-113">Vérifier si hello disque dur virtuel que vous souhaitez tooattach est déjà téléchargée tooyour abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="0193e-113">Check if hello VHD you want tooattach is already uploaded tooyour Azure subscription:</span></span>
   
    ```azurecli
    azure vm disk list
    ```

    <span data-ttu-id="0193e-114">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0193e-114">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. <span data-ttu-id="0193e-115">Si vous ne trouvez pas les disques hello que vous souhaitez toouse, vous risquez de télécharger un abonnement tooyour de disque dur virtuel local à l’aide de `azure vm disk create` ou `azure vm disk upload`.</span><span class="sxs-lookup"><span data-stu-id="0193e-115">If you don't find hello disk that you want toouse, you may upload a local VHD tooyour subscription by using `azure vm disk create` or `azure vm disk upload`.</span></span> <span data-ttu-id="0193e-116">Un exemple de `disk create` serait comme hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0193e-116">An example of `disk create` would be as in hello following example:</span></span>
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    <span data-ttu-id="0193e-117">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0193e-117">hello output is similar toohello following example:</span></span>

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   <span data-ttu-id="0193e-118">Vous pouvez également utiliser `azure vm disk upload` tooupload un compte de stockage de disque dur virtuel tooa.</span><span class="sxs-lookup"><span data-stu-id="0193e-118">You may also use `azure vm disk upload` tooupload a VHD tooa specific storage account.</span></span> <span data-ttu-id="0193e-119">Lire plus hello commandes toomanage vos disques de données de machine virtuelle Azure [ici](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="0193e-119">Read more about hello commands toomanage your Azure virtual machine data disks [over here](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

4. <span data-ttu-id="0193e-120">Maintenant vous attachez hello souhaitée virtuels tooyour de disque dur virtuel :</span><span class="sxs-lookup"><span data-stu-id="0193e-120">Now you attach hello desired VHD tooyour virtual machine:</span></span>
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   <span data-ttu-id="0193e-121">Assurez-vous que tooreplace *myVM* avec nom hello de votre machine virtuelle, et *myVHD* avec votre disque dur virtuel souhaité.</span><span class="sxs-lookup"><span data-stu-id="0193e-121">Make sure tooreplace *myVM* with hello name of your virtual machine, and *myVHD* with your desired VHD.</span></span>

5. <span data-ttu-id="0193e-122">Vous pouvez vérifier le disque de hello est attaché toohello machine virtuelle `azure vm disk list <virtual-machine-name>`:</span><span class="sxs-lookup"><span data-stu-id="0193e-122">You can verify hello disk is attached toohello virtual machine with `azure vm disk list <virtual-machine-name>`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="0193e-123">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0193e-123">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> <span data-ttu-id="0193e-124">Après avoir ajouté un disque de données, vous devez toolog sur l’ordinateur virtuel de toohello et initialiser le disque de hello donc hello virtual machine peut utiliser un disque de hello pour le stockage (voir hello suivant les étapes pour plus d’informations sur comment toodo initialiser le disque de hello).</span><span class="sxs-lookup"><span data-stu-id="0193e-124">After you add a data disk, you'll need toolog on toohello virtual machine and initialize hello disk so hello virtual machine can use hello disk for storage (see hello following steps for more information on how toodo initialize hello disk).</span></span>
> 
> 

