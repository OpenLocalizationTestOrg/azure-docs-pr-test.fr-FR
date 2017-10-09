<span data-ttu-id="24158-101">La prise en charge de deux fonctionnalités de débogage est désormais disponible dans Azure : les supports de Console Output et Screenshot pour le modèle de déploiement Azure Virtual Machines Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="24158-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="24158-102">Lors de la prochaine tooAzure de votre propre image ou même initialisation d’une des images de plateforme hello, il peut y avoir plusieurs raisons pour lesquelles un ordinateur virtuel Obtient dans un état non démarrable.</span><span class="sxs-lookup"><span data-stu-id="24158-102">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="24158-103">Activation de ces fonctionnalités vous tooeasily diagnostiquer et récupérer vos Machines virtuelles des échecs de démarrage.</span><span class="sxs-lookup"><span data-stu-id="24158-103">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="24158-104">Pour les Machines virtuelles Linux, vous pouvez facilement afficher sortie hello de votre journal de console à partir de hello portail :</span><span class="sxs-lookup"><span data-stu-id="24158-104">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Portail Azure](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="24158-106">Toutefois, pour Windows et les ordinateurs virtuels Linux, Azure permet également de toosee une capture d’écran de hello machine virtuelle à partir de l’hyperviseur de hello :</span><span class="sxs-lookup"><span data-stu-id="24158-106">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Error](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="24158-108">Ces deux fonctionnalités sont prises en charge par les Machines Virtuelles Azure dans toutes les régions.</span><span class="sxs-lookup"><span data-stu-id="24158-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="24158-109">Tooappear de minutes too10 dans votre compte de stockage peuvent prendre note des captures d’écran et la sortie.</span><span class="sxs-lookup"><span data-stu-id="24158-109">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="24158-110">Erreurs de démarrage courantes</span><span class="sxs-lookup"><span data-stu-id="24158-110">Common boot errors</span></span>

- [<span data-ttu-id="24158-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="24158-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="24158-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="24158-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="24158-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="24158-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="24158-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="24158-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="24158-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="24158-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="24158-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="24158-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="24158-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="24158-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="24158-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="24158-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="24158-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="24158-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="24158-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="24158-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="24158-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="24158-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="24158-122">Système d’exploitation introuvable.</span><span class="sxs-lookup"><span data-stu-id="24158-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="24158-123">Échec de démarrage ou INACCESSIBLE_BOOT_DEVICE.</span><span class="sxs-lookup"><span data-stu-id="24158-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="24158-124">Activer la fonction de diagnostic sur une nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="24158-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="24158-125">Lorsque vous créez une Machine virtuelle à partir de la version préliminaire du portail de hello, sélectionnez hello **Azure Resource Manager** à partir de la liste déroulante modèle de déploiement hello :</span><span class="sxs-lookup"><span data-stu-id="24158-125">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Gestionnaire de ressources](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="24158-127">Configurer hello analyse option tooselect hello de stockage Azure où vous aimeriez tooplace ces fichiers de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="24158-127">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![Créer une machine virtuelle](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="24158-129">Si vous déployez un modèle Azure Resource Manager, accédez de ressource d’ordinateur virtuel tooyour et ajouter la section de profil de diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="24158-129">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="24158-130">N’oubliez pas d’en-tête de version de l’API de toouse hello « 2015-06-15 ».</span><span class="sxs-lookup"><span data-stu-id="24158-130">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="24158-131">profil de diagnostic Hello vous permet de compte de stockage hello tooselect où vous souhaitez tooput ces journaux.</span><span class="sxs-lookup"><span data-stu-id="24158-131">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

<span data-ttu-id="24158-132">toodeploy un exemple de Machine virtuelle avec les diagnostics de démarrage activées, consultez notre référentiel ici.</span><span class="sxs-lookup"><span data-stu-id="24158-132">toodeploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="24158-133">Mettre à jour une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="24158-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="24158-134">diagnostics de démarrage tooenable via hello Portal, vous pouvez également mettre à jour un ordinateur virtuel existant via hello portail.</span><span class="sxs-lookup"><span data-stu-id="24158-134">tooenable boot diagnostics through hello Portal, you can also update an existing Virtual Machine through hello Portal.</span></span> <span data-ttu-id="24158-135">Sélectionnez hello option Diagnostics de démarrage et les enregistrer.</span><span class="sxs-lookup"><span data-stu-id="24158-135">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="24158-136">Redémarrez l’effet de tootake hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="24158-136">Restart hello VM tootake effect.</span></span>

![Mettre à jour une machine virtuelle existante](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

