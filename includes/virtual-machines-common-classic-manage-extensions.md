


## <a name="using-vm-extensions"></a><span data-ttu-id="d11d9-101">Utilisation d'extensions de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="d11d9-101">Using VM Extensions</span></span>
<span data-ttu-id="d11d9-102">Les extensions de machines virtuelles Azure mettent en œuvre des comportements ou des fonctionnalités grâce auxquels d’autres programmes peuvent fonctionner sur des machines virtuelles Azure (par exemple, l’extension **WebDeployForVSDevTest** permet à Visual Studio de déployer des solutions web sur votre machine virtuelle Azure) ou d’interagir avec votre machine virtuelle pour prendre en charge un autre comportement (par exemple, vous pouvez utiliser les extensions d’accès à la machine virtuelle à partir de PowerShell, l’interface de ligne de commande Azure et des clients REST pour réinitialiser ou modifier des valeurs d’accès à distance de votre machine virtuelle Azure).</span><span class="sxs-lookup"><span data-stu-id="d11d9-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, the **WebDeployForVSDevTest** extension allows Visual Studio to Web Deploy solutions on your Azure VM) or provide the ability for you to interact with the VM to support some other behavior (for example, you can use the VM Access extensions from PowerShell, the Azure CLI, and REST clients to reset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d11d9-103">Pour obtenir une liste complète des extensions en fonction des fonctionnalités prises en charge, consultez [Fonctionnalités et extensions de machine virtuelle Azure](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d11d9-103">For a complete list of extensions by the features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="d11d9-104">Étant donné que chaque extension de machine virtuelle prend en charge une fonctionnalité spécifique, elle détermine ce que vous pouvez et ne pouvez pas faire avec une extension.</span><span class="sxs-lookup"><span data-stu-id="d11d9-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on the extension.</span></span> <span data-ttu-id="d11d9-105">Par conséquent, avant de modifier votre machine virtuelle, assurez-vous d'avoir bien lu la documentation relative à l'extension de machine virtuelle que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="d11d9-105">Therefore, before modifying your VM, make sure you have read the documentation for the VM Extension you want to use.</span></span> <span data-ttu-id="d11d9-106">La suppression de certaines extensions de machine virtuelle n'est pas prise en charge. D'autres ont des propriétés qui peuvent être définies et qui modifient radicalement le comportement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d11d9-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="d11d9-107">Les tâches les plus courantes sont :</span><span class="sxs-lookup"><span data-stu-id="d11d9-107">The most common tasks are:</span></span>

1. <span data-ttu-id="d11d9-108">Recherche d'extensions disponibles</span><span class="sxs-lookup"><span data-stu-id="d11d9-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="d11d9-109">Mise à jour des extensions chargées</span><span class="sxs-lookup"><span data-stu-id="d11d9-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="d11d9-110">Ajout d'extensions</span><span class="sxs-lookup"><span data-stu-id="d11d9-110">Adding Extensions</span></span>
4. <span data-ttu-id="d11d9-111">Suppression d'extensions</span><span class="sxs-lookup"><span data-stu-id="d11d9-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="d11d9-112">Recherche d'extensions disponibles</span><span class="sxs-lookup"><span data-stu-id="d11d9-112">Find Available Extensions</span></span>
<span data-ttu-id="d11d9-113">Vous pouvez localiser l’extension et obtenir des informations étendues en utilisant :</span><span class="sxs-lookup"><span data-stu-id="d11d9-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="d11d9-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d11d9-114">PowerShell</span></span>
* <span data-ttu-id="d11d9-115">Interface de ligne de commande interplateforme Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="d11d9-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="d11d9-116">API REST de gestion de service</span><span class="sxs-lookup"><span data-stu-id="d11d9-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="d11d9-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d11d9-117">Azure PowerShell</span></span>
<span data-ttu-id="d11d9-118">Certaines extensions disposent d’applets de commande PowerShell spécifiques, ce qui simplifie leur configuration à partir de PowerShell. Mais les applets de commande suivantes fonctionnent pour toutes les extensions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d11d9-118">Some extensions have PowerShell cmdlets that are specific to them, which may make their configuration from PowerShell easier; but the following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="d11d9-119">Vous pouvez utiliser les applets de commande suivantes pour obtenir des informations sur les extensions disponibles :</span><span class="sxs-lookup"><span data-stu-id="d11d9-119">You can use the following cmdlets to obtain information about available extensions:</span></span>

* <span data-ttu-id="d11d9-120">Pour les instances de rôles web ou de travail, vous pouvez utiliser l’applet de commande [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d11d9-120">For instances of web roles or worker roles, you can use the [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="d11d9-121">Pour les instances de machines virtuelles, vous pouvez utiliser l’applet de commande [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d11d9-121">For instances of Virtual Machines, you can use the [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="d11d9-122">Par exemple, le code qui suit montre comment obtenir les informations sur l’extension **IaaSDiagnostics** avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d11d9-122">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using PowerShell.</span></span>
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="d11d9-123">Interface de ligne de commande Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="d11d9-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="d11d9-124">Certaines extensions ont leurs propres commandes Azure CLI (par exemple, l'extension de machine virtuelle Docker), ce qui peut faciliter leur configuration. Mais les commandes suivantes fonctionnent pour toutes les extensions de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d11d9-124">Some extensions have Azure CLI commands that are specific to them (the Docker VM Extension is one example), which may make their configuration easier; but the following commands work for all VM extensions.</span></span>

<span data-ttu-id="d11d9-125">La commande **azure vm extension list** permet d’obtenir des informations sur les extensions disponibles et l’option **–-json** permet d’afficher toutes les informations disponibles sur une ou plusieurs extensions.</span><span class="sxs-lookup"><span data-stu-id="d11d9-125">You can use the **azure vm extension list** command to obtain information about available extensions, and use the **–-json** option to display all available information about one or more extensions.</span></span> <span data-ttu-id="d11d9-126">Si vous n’utilisez pas de nom d’extension, la commande renvoie une description JSON de toutes les extensions disponibles.</span><span class="sxs-lookup"><span data-stu-id="d11d9-126">If you do not use an extension name, the command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="d11d9-127">Ainsi, l’exemple de code suivant montre comment répertorier les informations relatives à l’extension **IaaSDiagnostics** à l’aide de la commande Azure CLI **azure vm extension list** et utilise l’option **–-json** pour renvoyer des informations complètes.</span><span class="sxs-lookup"><span data-stu-id="d11d9-127">For example, the following code example shows how to list the information for the **IaaSDiagnostics** extension using the Azure CLI **azure vm extension list** command and uses the **–-json** option to return complete information.</span></span>

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a><span data-ttu-id="d11d9-128">API REST de gestion de service</span><span class="sxs-lookup"><span data-stu-id="d11d9-128">Service Management REST APIs</span></span>
<span data-ttu-id="d11d9-129">Vous pouvez utiliser les API REST suivantes pour obtenir des informations sur les extensions disponibles :</span><span class="sxs-lookup"><span data-stu-id="d11d9-129">You can use the following REST APIs to obtain information about available extensions:</span></span>

* <span data-ttu-id="d11d9-130">Pour les instances de rôles web ou de travail, vous pouvez utiliser l’opération [Liste des extensions disponibles](https://msdn.microsoft.com/library/dn169559.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d11d9-130">For instances of web roles or worker roles, you can use the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="d11d9-131">Pour dresser une liste des versions des extensions disponibles, vous pouvez utiliser l’opération [Liste des versions d’extension](https://msdn.microsoft.com/library/dn495437.aspx).</span><span class="sxs-lookup"><span data-stu-id="d11d9-131">To list the versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="d11d9-132">Pour les instances de machines virtuelles, vous pouvez utiliser l’opération [Liste des extensions des ressources](https://msdn.microsoft.com/library/dn495441.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d11d9-132">For instances of Virtual Machines, you can use the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="d11d9-133">Pour dresser une liste des versions des extensions disponibles, vous pouvez utiliser l’opération [Liste des versions d’extension des ressources](https://msdn.microsoft.com/library/dn495440.aspx).</span><span class="sxs-lookup"><span data-stu-id="d11d9-133">To list the versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="d11d9-134">Ajout, mise à jour ou désactivation des extensions</span><span class="sxs-lookup"><span data-stu-id="d11d9-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="d11d9-135">Des extensions peuvent être ajoutées à une instance créée ou déjà exécutée.</span><span class="sxs-lookup"><span data-stu-id="d11d9-135">Extensions can be added when an instance is created or they can be added to a running instance.</span></span> <span data-ttu-id="d11d9-136">Des extensions peuvent être mises à jour, désactivées ou supprimées.</span><span class="sxs-lookup"><span data-stu-id="d11d9-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="d11d9-137">Vous pouvez effectuer ces actions à l'aide des applets de commande Azure PowerShell ou des opérations de l'API REST de gestion des services.</span><span class="sxs-lookup"><span data-stu-id="d11d9-137">You can perform these actions by using Azure PowerShell cmdlets or by using the Service Management REST API operations.</span></span> <span data-ttu-id="d11d9-138">Des paramètres sont requis pour installer et configurer certaines extensions.</span><span class="sxs-lookup"><span data-stu-id="d11d9-138">Parameters are required to install and set up some extensions.</span></span> <span data-ttu-id="d11d9-139">Des paramètres publics et privés sont pris en charge pour les extensions.</span><span class="sxs-lookup"><span data-stu-id="d11d9-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="d11d9-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d11d9-140">Azure PowerShell</span></span>
<span data-ttu-id="d11d9-141">Le moyen le plus simple pour ajouter et mettre à jour des extensions consiste à utiliser les applets de commande Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d11d9-141">Using Azure PowerShell cmdlets is the easiest way to add and update extensions.</span></span> <span data-ttu-id="d11d9-142">Lorsque vous utilisez les applets de commande de l'extension, la majeure partie de la configuration de l'extension est effectuée pour vous.</span><span class="sxs-lookup"><span data-stu-id="d11d9-142">When you use the extension cmdlets, most of the configuration of the extension is done for you.</span></span> <span data-ttu-id="d11d9-143">Il peut arriver que vous deviez ajouter une extension par programmation.</span><span class="sxs-lookup"><span data-stu-id="d11d9-143">At times, you may need to programmatically add an extension.</span></span> <span data-ttu-id="d11d9-144">Le cas échéant, vous devez indiquer la configuration de l'extension.</span><span class="sxs-lookup"><span data-stu-id="d11d9-144">When you need to do this, you must provide the configuration of the extension.</span></span>

<span data-ttu-id="d11d9-145">Vous pouvez utiliser les applets de commande suivantes pour savoir si une extension nécessite une configuration de paramètres publics et privés :</span><span class="sxs-lookup"><span data-stu-id="d11d9-145">You can use the following cmdlets to know whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="d11d9-146">Pour les instances de rôles web ou de travail, vous pouvez utiliser l’applet de commande **Get-AzureServiceAvailableExtension** .</span><span class="sxs-lookup"><span data-stu-id="d11d9-146">For instances of web roles or worker roles, you can use the **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="d11d9-147">Pour les instances de machines virtuelles, vous pouvez utiliser l’applet de commande **Get-AzureVMAvailableExtension** .</span><span class="sxs-lookup"><span data-stu-id="d11d9-147">For instances of Virtual Machines, you can use the **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="d11d9-148">API REST de gestion de service</span><span class="sxs-lookup"><span data-stu-id="d11d9-148">Service Management REST APIs</span></span>
<span data-ttu-id="d11d9-149">Lorsque vous récupérez une liste d'extensions disponibles à l'aide des API REST, vous recevez des informations sur la procédure de configuration de l'extension.</span><span class="sxs-lookup"><span data-stu-id="d11d9-149">When you retrieve a listing of available extensions by using the REST APIs, you receive information about how the extension is to be configured.</span></span> <span data-ttu-id="d11d9-150">Elles peuvent comporter des informations sur les paramètres représentés par un schéma public et un schéma privé.</span><span class="sxs-lookup"><span data-stu-id="d11d9-150">The information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="d11d9-151">Les valeurs de paramètres publics sont renvoyées dans des requêtes relatives aux instances.</span><span class="sxs-lookup"><span data-stu-id="d11d9-151">Public parameter values are returned in queries about the instances.</span></span> <span data-ttu-id="d11d9-152">Les valeurs de paramètres privés ne sont pas renvoyées.</span><span class="sxs-lookup"><span data-stu-id="d11d9-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="d11d9-153">Vous pouvez utiliser les API REST suivantes pour savoir si une extension nécessite une configuration de paramètres publics et privés :</span><span class="sxs-lookup"><span data-stu-id="d11d9-153">You can use the following REST APIs to know whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="d11d9-154">Pour les instances de rôles web ou de travail, les éléments **PublicConfigurationSchema** et **PrivateConfigurationSchema** contiennent les informations dans la réponse provenant de l’opération [Liste des extensions disponibles](https://msdn.microsoft.com/library/dn169559.aspx).</span><span class="sxs-lookup"><span data-stu-id="d11d9-154">For instances of web roles or worker roles, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="d11d9-155">pour les instances de machines virtuelles, les éléments **PublicConfigurationSchema** et **PrivateConfigurationSchema** contiennent les informations dans la réponse provenant de l’opération [Liste des extensions de ressources](https://msdn.microsoft.com/library/dn495441.aspx).</span><span class="sxs-lookup"><span data-stu-id="d11d9-155">For instances of Virtual Machines, the **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain the information in the response from the [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="d11d9-156">Des extensions peuvent également utiliser des configurations définies avec JSON.</span><span class="sxs-lookup"><span data-stu-id="d11d9-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="d11d9-157">En cas d’utilisation de ces types d’extension, seul l’élément **SampleConfig** est utilisé.</span><span class="sxs-lookup"><span data-stu-id="d11d9-157">When these types of extensions are used, only the **SampleConfig** element is used.</span></span>
> 
> 

