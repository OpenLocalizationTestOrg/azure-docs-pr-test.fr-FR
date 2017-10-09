
1. <span data-ttu-id="8bc8c-101">Se connecter tooyour abonnement Azure à l’aide des étapes hello répertoriées dans [connecter tooAzure de hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="8bc8c-101">Sign in tooyour Azure subscription using hello steps listed in [Connect tooAzure from hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span></span>

2. <span data-ttu-id="8bc8c-102">Assurez-vous que vous êtes en mode de déploiement classique hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8bc8c-102">Make sure you are in hello Classic deployment mode as follows:</span></span>

    ```azurecli
    azure config mode asm
    ```

3. <span data-ttu-id="8bc8c-103">Découvrez image de hello Linux que vous souhaitez tooload à partir d’images disponibles de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8bc8c-103">Find out hello Linux image that you want tooload from hello available images as follows:</span></span>

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    <span data-ttu-id="8bc8c-104">Dans une fenêtre d’invite de commandes Windows, utilisez **find** au lieu de grep.</span><span class="sxs-lookup"><span data-stu-id="8bc8c-104">In a Windows command-prompt window, use **find** instead of grep.</span></span>
   
4. <span data-ttu-id="8bc8c-105">Utilisez `azure vm create` toocreate une machine virtuelle avec l’image de Linux hello à partir de la liste précédente hello.</span><span class="sxs-lookup"><span data-stu-id="8bc8c-105">Use `azure vm create` toocreate a VM with hello Linux image from hello previous list.</span></span> <span data-ttu-id="8bc8c-106">Cette étape crée un service cloud et un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8bc8c-106">This step creates a cloud service and storage account.</span></span> <span data-ttu-id="8bc8c-107">Vous pourriez également vous connecter cet machine virtuelle tooan service cloud existant avec un `-c` option.</span><span class="sxs-lookup"><span data-stu-id="8bc8c-107">You could also connect this VM tooan existing cloud service with a `-c` option.</span></span> <span data-ttu-id="8bc8c-108">Créer un toolog de point de terminaison SSH dans la machine virtuelle Linux de toohello hello `-e` option.</span><span class="sxs-lookup"><span data-stu-id="8bc8c-108">Create an SSH endpoint toolog in toohello Linux virtual machine with hello `-e` option.</span></span> <span data-ttu-id="8bc8c-109">Hello exemple suivant crée un ordinateur virtuel nommé `myVM` à l’aide de hello `Ubuntu-14_04_4-LTS` image Bonjour `West US` emplacement et ajoute un nom d’utilisateur `ops`:</span><span class="sxs-lookup"><span data-stu-id="8bc8c-109">hello following example creates a VM named `myVM` using hello `Ubuntu-14_04_4-LTS` image in hello `West US` location, and adds a user name `ops`:</span></span>
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    <span data-ttu-id="8bc8c-110">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="8bc8c-110">hello output is similar toohello following example:</span></span>

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > <span data-ttu-id="8bc8c-111">Pour une machine virtuelle Linux, vous devez fournir hello `-e` option `vm create`.</span><span class="sxs-lookup"><span data-stu-id="8bc8c-111">For a Linux virtual machine, you must provide hello `-e` option in `vm create`.</span></span> <span data-ttu-id="8bc8c-112">Il n’est pas possible de tooenable SSH après la création de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="8bc8c-112">It is not possible tooenable SSH after hello virtual machine has been created.</span></span> <span data-ttu-id="8bc8c-113">Pour plus d’informations sur SSH, lisez [comment tooUse SSH avec Linux sur Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8bc8c-113">For more details on SSH, read [How tooUse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

5. <span data-ttu-id="8bc8c-114">Vous pouvez vérifier les attributs hello Hello machine virtuelle à l’aide de hello `azure vm show` commande.</span><span class="sxs-lookup"><span data-stu-id="8bc8c-114">You can verify hello attributes of hello VM by using hello `azure vm show` command.</span></span> <span data-ttu-id="8bc8c-115">Hello exemple suivant répertorie les informations pour hello ordinateur virtuel nommé `myVM`:</span><span class="sxs-lookup"><span data-stu-id="8bc8c-115">hello following example lists information for hello VM named `myVM`:</span></span>

    ```azurecli   
    azure vm show myVM
    ```

6. <span data-ttu-id="8bc8c-116">Démarrez votre machine virtuelle avec hello `azure vm start` commande comme suit :</span><span class="sxs-lookup"><span data-stu-id="8bc8c-116">Start your VM with hello `azure vm start` command as follows:</span></span>

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="8bc8c-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8bc8c-117">Next steps</span></span>
<span data-ttu-id="8bc8c-118">Pour plus d’informations sur toutes les commandes de ces machines virtuelles Azure CLI 1.0, consultez hello [Using hello Azure CLI 1.0 avec l’API du déploiement classique hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="8bc8c-118">For details on all these Azure CLI 1.0 virtual machine commands, read hello [Using hello Azure CLI 1.0 with hello Classic deployment API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

