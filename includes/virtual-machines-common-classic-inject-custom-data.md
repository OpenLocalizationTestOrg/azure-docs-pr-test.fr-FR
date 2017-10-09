


<span data-ttu-id="bf59c-101">Cette rubrique montre comment :</span><span class="sxs-lookup"><span data-stu-id="bf59c-101">This topic describes how to:</span></span>

* <span data-ttu-id="bf59c-102">injecter des données dans une machine virtuelle Azure lors de son approvisionnement ;</span><span class="sxs-lookup"><span data-stu-id="bf59c-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="bf59c-103">les récupérer avec Windows et Linux ;</span><span class="sxs-lookup"><span data-stu-id="bf59c-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="bf59c-104">Utiliser des outils spéciaux disponibles sur certains systèmes toodetect et gérer automatiquement les données personnalisées.</span><span class="sxs-lookup"><span data-stu-id="bf59c-104">Use special tools available on some systems toodetect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="bf59c-105">Cet article décrit les données personnalisées peuvent être ajoutées à l’aide d’une machine virtuelle créée avec hello API de gestion des services Azure.</span><span class="sxs-lookup"><span data-stu-id="bf59c-105">This article describes how custom data can be injected by using a VM created with hello Azure Service Management API.</span></span> <span data-ttu-id="bf59c-106">toosee toouse hello API de gestion des ressources Azure, voir [exemple de modèle de hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span><span class="sxs-lookup"><span data-stu-id="bf59c-106">toosee how toouse hello Azure Resource Management API, see [hello example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="bf59c-107">Injection de données personnalisées dans votre machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="bf59c-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="bf59c-108">Cette fonctionnalité est actuellement pris en charge uniquement dans hello [Interface de ligne de commande Azure](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="bf59c-108">This feature is currently supported only in hello [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="bf59c-109">Ici, nous créons un `custom-data.txt` fichier qui contient nos données, puis injecter qui dans toohello machine virtuelle lors de la configuration.</span><span class="sxs-lookup"><span data-stu-id="bf59c-109">Here we create a `custom-data.txt` file that contains our data, then inject that in toohello VM during provisioning.</span></span> <span data-ttu-id="bf59c-110">Bien que vous pouvez utiliser une des options de hello pour hello `azure vm create` suivant de hello illustre une approche très élémentaire de la commande :</span><span class="sxs-lookup"><span data-stu-id="bf59c-110">Although you may use any of hello options for hello `azure vm create` command, hello following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a><span data-ttu-id="bf59c-111">À l’aide des données personnalisées dans la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="bf59c-111">Using custom data in hello virtual machine</span></span>
* <span data-ttu-id="bf59c-112">Si votre machine virtuelle Azure est un ordinateur virtuel basé sur Windows, hello données personnalisé est enregistré trop`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span><span class="sxs-lookup"><span data-stu-id="bf59c-112">If your Azure VM is a Windows-based VM, then hello custom data file is saved too`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="bf59c-113">Bien qu’il était codée en base64 de tootransfer de toohello d’ordinateur local hello nouvel ordinateur virtuel, il est automatiquement décodé et peut être ouvert ou utilisées immédiatement.</span><span class="sxs-lookup"><span data-stu-id="bf59c-113">Although it was base64-encoded tootransfer from hello local computer toohello new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="bf59c-114">Si le fichier de hello existe, il est remplacé.</span><span class="sxs-lookup"><span data-stu-id="bf59c-114">If hello file exists, it is overwritten.</span></span> <span data-ttu-id="bf59c-115">sécurité Hello sur le répertoire de hello est définie trop**système : contrôle total** et **administrateurs : contrôle total**.</span><span class="sxs-lookup"><span data-stu-id="bf59c-115">hello security on hello directory is set too**System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="bf59c-116">Si votre machine virtuelle Azure est une machine virtuelle basés sur Linux, puis le fichier de données personnalisées hello se trouve dans un des éléments suivants de hello place en fonction de votre distribution.</span><span class="sxs-lookup"><span data-stu-id="bf59c-116">If your Azure VM is a Linux-based VM, then hello custom data file will be located in one of hello following places depending on your distro.</span></span> <span data-ttu-id="bf59c-117">les données de salutation peuvent être codée en base64, donc vous devez tout d’abord les données de salutation toodecode :</span><span class="sxs-lookup"><span data-stu-id="bf59c-117">hello data may be base64-encoded, so you may need toodecode hello data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="bf59c-118">Cloud-init sur Azure</span><span class="sxs-lookup"><span data-stu-id="bf59c-118">Cloud-init on Azure</span></span>
<span data-ttu-id="bf59c-119">Si votre machine virtuelle Azure est à partir d’une image Ubuntu ou CoreOS, vous pouvez utiliser CustomData toosend un toocloud cloud-config-init.</span><span class="sxs-lookup"><span data-stu-id="bf59c-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData toosend a cloud-config toocloud-init.</span></span> <span data-ttu-id="bf59c-120">Sinon, si votre fichier de données personnalisées est un script, Cloud-init peut l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="bf59c-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="bf59c-121">Images cloud Ubuntu</span><span class="sxs-lookup"><span data-stu-id="bf59c-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="bf59c-122">Dans la plupart des images Azure Linux, vous devez modifier « / etc/waagent.conf » tooconfigure hello temporaire de ressources disque et échange le fichier.</span><span class="sxs-lookup"><span data-stu-id="bf59c-122">In most Azure Linux images, you would edit "/etc/waagent.conf" tooconfigure hello temporary resource disk and swap file.</span></span> <span data-ttu-id="bf59c-123">Pour plus d’information, consultez le [Guide d’utilisation de l’agent Linux Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="bf59c-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="bf59c-124">Toutefois, sur les Images de hello Ubuntu Cloud, vous devez utiliser disque de ressources cloud-init tooconfigure hello (autrement dit, un disque « éphémère » hello) et échange partition.</span><span class="sxs-lookup"><span data-stu-id="bf59c-124">However, on hello Ubuntu Cloud Images, you must use cloud-init tooconfigure hello resource disk (that is, hello "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="bf59c-125">Consultez hello suivant page Wiki d’Ubuntu hello pour plus d’informations : [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span><span class="sxs-lookup"><span data-stu-id="bf59c-125">See hello following page on hello Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="bf59c-126">Étapes suivantes : Utilisation de Cloud-init</span><span class="sxs-lookup"><span data-stu-id="bf59c-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="bf59c-127">Pour plus d’informations, consultez hello [documentation cloud-init pour Ubuntu](https://help.ubuntu.com/community/CloudInit).</span><span class="sxs-lookup"><span data-stu-id="bf59c-127">For further information, see hello [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="bf59c-128">Référence sur l’opération Ajouter un rôle de l’API REST de gestion des services</span><span class="sxs-lookup"><span data-stu-id="bf59c-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="bf59c-129">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="bf59c-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

