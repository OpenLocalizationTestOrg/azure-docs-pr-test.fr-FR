


<span data-ttu-id="56be7-101">Cette rubrique montre comment :</span><span class="sxs-lookup"><span data-stu-id="56be7-101">This topic describes how to:</span></span>

* <span data-ttu-id="56be7-102">injecter des données dans une machine virtuelle Azure lors de son approvisionnement ;</span><span class="sxs-lookup"><span data-stu-id="56be7-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="56be7-103">les récupérer avec Windows et Linux ;</span><span class="sxs-lookup"><span data-stu-id="56be7-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="56be7-104">utiliser les outils spéciaux disponibles sur certains systèmes pour détecter et gérer les données personnalisées automatiquement.</span><span class="sxs-lookup"><span data-stu-id="56be7-104">Use special tools available on some systems to detect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="56be7-105">Cet article explique comment des données personnalisées peuvent être injectées à l’aide d’une machine virtuelle créée avec l’API Azure Service Management.</span><span class="sxs-lookup"><span data-stu-id="56be7-105">This article describes how custom data can be injected by using a VM created with the Azure Service Management API.</span></span> <span data-ttu-id="56be7-106">Pour savoir comment utiliser l’API de gestion des ressources Azure, consultez cet [exemple de modèle](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span><span class="sxs-lookup"><span data-stu-id="56be7-106">To see how to use the Azure Resource Management API, see [the example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="56be7-107">Injection de données personnalisées dans votre machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="56be7-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="56be7-108">À ce jour, cette fonction est prise en charge uniquement dans [l’interface de ligne de commande Microsoft Azure](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="56be7-108">This feature is currently supported only in the [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="56be7-109">Nous créons ici un fichier `custom-data.txt` qui contient nos données, puis injectons ces données dans la machine virtuelle lors de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="56be7-109">Here we create a `custom-data.txt` file that contains our data, then inject that in to the VM during provisioning.</span></span> <span data-ttu-id="56be7-110">Vous pouvez utiliser toutes les options pour la commande `azure vm create`. L’exemple ci-dessous montre une approche très basique :</span><span class="sxs-lookup"><span data-stu-id="56be7-110">Although you may use any of the options for the `azure vm create` command, the following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-the-virtual-machine"></a><span data-ttu-id="56be7-111">Utilisation de données personnalisées dans la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="56be7-111">Using custom data in the virtual machine</span></span>
* <span data-ttu-id="56be7-112">Si votre machine virtuelle Azure est une machine virtuelle Windows, le fichier de données personnalisées est enregistré à l’emplacement `%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span><span class="sxs-lookup"><span data-stu-id="56be7-112">If your Azure VM is a Windows-based VM, then the custom data file is saved to `%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="56be7-113">Même s’il a été encodé en base 64 pour son transfert depuis l’ordinateur local vers la nouvelle machine virtuelle, il est décodé automatiquement et peut être ouvert et utilisé immédiatement.</span><span class="sxs-lookup"><span data-stu-id="56be7-113">Although it was base64-encoded to transfer from the local computer to the new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="56be7-114">Si le fichier existe, il est remplacé.</span><span class="sxs-lookup"><span data-stu-id="56be7-114">If the file exists, it is overwritten.</span></span> <span data-ttu-id="56be7-115">La sécurité du répertoire est définie sur **Système : Contrôle total** et **Administrateurs : Contrôle total**.</span><span class="sxs-lookup"><span data-stu-id="56be7-115">The security on the directory is set to **System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="56be7-116">Si votre machine virtuelle Azure est une machine virtuelle Linux, le fichier de données personnalisées se trouvera à l’un des deux emplacements suivants, en fonction de votre distribution.</span><span class="sxs-lookup"><span data-stu-id="56be7-116">If your Azure VM is a Linux-based VM, then the custom data file will be located in one of the following places depending on your distro.</span></span> <span data-ttu-id="56be7-117">Les données seront peut-être encodées en base 64. Il se peut donc que vous deviez d’abord les décoder :</span><span class="sxs-lookup"><span data-stu-id="56be7-117">The data may be base64-encoded, so you may need to decode the data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="56be7-118">Cloud-init sur Azure</span><span class="sxs-lookup"><span data-stu-id="56be7-118">Cloud-init on Azure</span></span>
<span data-ttu-id="56be7-119">Si votre machine virtuelle Azure est issue d’une image Ubuntu ou CoreOS, vous pouvez utiliser le fichier CustomData afin d’envoyer un fichier cloud-config à Cloud-init.</span><span class="sxs-lookup"><span data-stu-id="56be7-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData to send a cloud-config to cloud-init.</span></span> <span data-ttu-id="56be7-120">Sinon, si votre fichier de données personnalisées est un script, Cloud-init peut l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="56be7-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="56be7-121">Images cloud Ubuntu</span><span class="sxs-lookup"><span data-stu-id="56be7-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="56be7-122">Dans la plupart des images Azure Linux, il vous faut modifier « /etc/waagent.conf » pour configurer le disque de ressources temporaire et le fichier d’échange.</span><span class="sxs-lookup"><span data-stu-id="56be7-122">In most Azure Linux images, you would edit "/etc/waagent.conf" to configure the temporary resource disk and swap file.</span></span> <span data-ttu-id="56be7-123">Pour plus d’information, consultez le [Guide d’utilisation de l’agent Linux Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="56be7-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="56be7-124">Néanmoins, nous devons utiliser Cloud-init sur les images cloud Ubuntu pour configurer le disque de ressources (en d’autres termes, le disque « éphémère ») et la partition d’échange.</span><span class="sxs-lookup"><span data-stu-id="56be7-124">However, on the Ubuntu Cloud Images, you must use cloud-init to configure the resource disk (that is, the "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="56be7-125">Consultez la page suivante du wiki Ubuntu pour en savoir plus : [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span><span class="sxs-lookup"><span data-stu-id="56be7-125">See the following page on the Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="56be7-126">Étapes suivantes : Utilisation de Cloud-init</span><span class="sxs-lookup"><span data-stu-id="56be7-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="56be7-127">Pour plus d'informations, consultez la [documentation cloud-init pour Ubuntu](https://help.ubuntu.com/community/CloudInit).</span><span class="sxs-lookup"><span data-stu-id="56be7-127">For further information, see the [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="56be7-128">Référence sur l’opération Ajouter un rôle de l’API REST de gestion des services</span><span class="sxs-lookup"><span data-stu-id="56be7-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="56be7-129">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="56be7-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

