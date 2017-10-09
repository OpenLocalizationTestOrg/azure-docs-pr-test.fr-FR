


## <a name="using-vm-extensions"></a><span data-ttu-id="1916e-101">Utilisation d'extensions de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="1916e-101">Using VM Extensions</span></span>
<span data-ttu-id="1916e-102">Les Extensions de machine virtuelle Azure implémenter des comportements ou des fonctionnalités qui soit à autres programmes de fonctionner sur des machines virtuelles Azure (par exemple, hello **WebDeployForVSDevTest** extension permet de déployer des solutions Visual Studio tooWeb sur votre machine virtuelle Azure) ou fournir Hello possibilité pour vous toointeract avec hello VM toosupport un autre comportement (par exemple, vous pouvez utiliser PowerShell, hello CLI d’Azure et les autres clients tooreset les extensions VM accès hello ou modifier les valeurs de l’accès à distance sur votre machine virtuelle Azure).</span><span class="sxs-lookup"><span data-stu-id="1916e-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, hello **WebDeployForVSDevTest** extension allows Visual Studio tooWeb Deploy solutions on your Azure VM) or provide hello ability for you toointeract with hello VM toosupport some other behavior (for example, you can use hello VM Access extensions from PowerShell, hello Azure CLI, and REST clients tooreset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1916e-103">Pour obtenir une liste complète des extensions en fonctionnalités hello prises en charge, consultez [fonctionnalités et Extensions de machine virtuelle Azure](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1916e-103">For a complete list of extensions by hello features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1916e-104">Étant donné que chaque extension de machine virtuelle prend en charge une fonctionnalité spécifique, exactement ce que vous pouvez et ne peut pas faire avec une extension dépend hello extension.</span><span class="sxs-lookup"><span data-stu-id="1916e-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on hello extension.</span></span> <span data-ttu-id="1916e-105">Par conséquent, avant de modifier votre machine virtuelle, assurez-vous que vous avez lu la documentation hello pour hello machine virtuelle de l’Extension toouse.</span><span class="sxs-lookup"><span data-stu-id="1916e-105">Therefore, before modifying your VM, make sure you have read hello documentation for hello VM Extension you want toouse.</span></span> <span data-ttu-id="1916e-106">La suppression de certaines extensions de machine virtuelle n'est pas prise en charge. D'autres ont des propriétés qui peuvent être définies et qui modifient radicalement le comportement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1916e-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="1916e-107">les tâches les plus courantes Hello sont :</span><span class="sxs-lookup"><span data-stu-id="1916e-107">hello most common tasks are:</span></span>

1. <span data-ttu-id="1916e-108">Recherche d'extensions disponibles</span><span class="sxs-lookup"><span data-stu-id="1916e-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="1916e-109">Mise à jour des extensions chargées</span><span class="sxs-lookup"><span data-stu-id="1916e-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="1916e-110">Ajout d'extensions</span><span class="sxs-lookup"><span data-stu-id="1916e-110">Adding Extensions</span></span>
4. <span data-ttu-id="1916e-111">Suppression d'extensions</span><span class="sxs-lookup"><span data-stu-id="1916e-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="1916e-112">Recherche d'extensions disponibles</span><span class="sxs-lookup"><span data-stu-id="1916e-112">Find Available Extensions</span></span>
<span data-ttu-id="1916e-113">Vous pouvez localiser l’extension et obtenir des informations étendues en utilisant :</span><span class="sxs-lookup"><span data-stu-id="1916e-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="1916e-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1916e-114">PowerShell</span></span>
* <span data-ttu-id="1916e-115">Interface de ligne de commande interplateforme Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="1916e-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="1916e-116">API REST de gestion de service</span><span class="sxs-lookup"><span data-stu-id="1916e-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="1916e-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1916e-117">Azure PowerShell</span></span>
<span data-ttu-id="1916e-118">Certaines extensions ont les applets de commande PowerShell sont toothem spécifique, ce qui peut faciliter leur configuration à partir de PowerShell ; mais hello applets de commande suivantes fonctionnent pour toutes les extensions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1916e-118">Some extensions have PowerShell cmdlets that are specific toothem, which may make their configuration from PowerShell easier; but hello following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="1916e-119">Vous pouvez utiliser hello suivant d’applets de commande tooobtain plus d’informations sur les extensions disponibles :</span><span class="sxs-lookup"><span data-stu-id="1916e-119">You can use hello following cmdlets tooobtain information about available extensions:</span></span>

* <span data-ttu-id="1916e-120">Pour les instances de rôles web ou les rôles de travail, vous pouvez utiliser hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="1916e-120">For instances of web roles or worker roles, you can use hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="1916e-121">Pour les instances d’ordinateurs virtuels, vous pouvez utiliser hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="1916e-121">For instances of Virtual Machines, you can use hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="1916e-122">Par exemple, hello suivant exemple de code montre comment toolist les informations de hello **IaaSDiagnostics** extension à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1916e-122">For example, hello following code example shows how toolist the information for hello **IaaSDiagnostics** extension using PowerShell.</span></span>
  
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

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="1916e-123">Interface de ligne de commande Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="1916e-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="1916e-124">Certaines extensions ont des commandes CLI d’Azure toothem spécifique (hello Extension de machine virtuelle Docker est un exemple), ce qui peut faciliter leur configuration ; mais suivant de hello des commandes pour toutes les extensions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1916e-124">Some extensions have Azure CLI commands that are specific toothem (hello Docker VM Extension is one example), which may make their configuration easier; but hello following commands work for all VM extensions.</span></span>

<span data-ttu-id="1916e-125">Vous pouvez utiliser hello **liste des extensions de machine virtuelle azure** tooobtain plus d’informations sur les extensions disponibles de commandes et utilisez hello **–-json** option toodisplay toutes les informations disponibles sur une ou plusieurs extensions.</span><span class="sxs-lookup"><span data-stu-id="1916e-125">You can use hello **azure vm extension list** command tooobtain information about available extensions, and use hello **–-json** option toodisplay all available information about one or more extensions.</span></span> <span data-ttu-id="1916e-126">Si vous n’utilisez pas un nom d’extension, la commande hello retourne une description JSON de toutes les extensions disponibles.</span><span class="sxs-lookup"><span data-stu-id="1916e-126">If you do not use an extension name, hello command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="1916e-127">Par exemple, hello, exemple de code suivant montre comment toolist hello concernant hello **IaaSDiagnostics** à l’aide de l’extension hello CLI d’Azure **liste des extensions de machine virtuelle azure** hello de commande et utilise **–-json** option tooreturn obtenir des informations complètes.</span><span class="sxs-lookup"><span data-stu-id="1916e-127">For example, hello following code example shows how toolist hello information for hello **IaaSDiagnostics** extension using hello Azure CLI **azure vm extension list** command and uses hello **–-json** option tooreturn complete information.</span></span>

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



### <a name="service-management-rest-apis"></a><span data-ttu-id="1916e-128">API REST de gestion de service</span><span class="sxs-lookup"><span data-stu-id="1916e-128">Service Management REST APIs</span></span>
<span data-ttu-id="1916e-129">Vous pouvez utiliser hello API REST des informations de tooobtain sur les extensions disponibles suivantes :</span><span class="sxs-lookup"><span data-stu-id="1916e-129">You can use hello following REST APIs tooobtain information about available extensions:</span></span>

* <span data-ttu-id="1916e-130">Pour les instances de rôles web ou les rôles de travail, vous pouvez utiliser hello [liste des Extensions disponibles](https://msdn.microsoft.com/library/dn169559.aspx) opération.</span><span class="sxs-lookup"><span data-stu-id="1916e-130">For instances of web roles or worker roles, you can use hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="1916e-131">versions de hello toolist des extensions disponibles, vous pouvez utiliser [liste des Versions d’Extension](https://msdn.microsoft.com/library/dn495437.aspx).</span><span class="sxs-lookup"><span data-stu-id="1916e-131">toolist hello versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="1916e-132">Pour les instances d’ordinateurs virtuels, vous pouvez utiliser hello [liste des Extensions de ressource](https://msdn.microsoft.com/library/dn495441.aspx) opération.</span><span class="sxs-lookup"><span data-stu-id="1916e-132">For instances of Virtual Machines, you can use hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="1916e-133">versions de hello toolist des extensions disponibles, vous pouvez utiliser [liste des Versions d’Extension de ressource](https://msdn.microsoft.com/library/dn495440.aspx).</span><span class="sxs-lookup"><span data-stu-id="1916e-133">toolist hello versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="1916e-134">Ajout, mise à jour ou désactivation des extensions</span><span class="sxs-lookup"><span data-stu-id="1916e-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="1916e-135">Extensions peuvent être ajoutées lors de la création d’une instance ou qu’ils peuvent être ajoutés tooa instance en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1916e-135">Extensions can be added when an instance is created or they can be added tooa running instance.</span></span> <span data-ttu-id="1916e-136">Des extensions peuvent être mises à jour, désactivées ou supprimées.</span><span class="sxs-lookup"><span data-stu-id="1916e-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="1916e-137">Vous pouvez effectuer ces actions à l’aide des applets de commande PowerShell de Azure ou à l’aide d’opérations d’API REST Service Management hello.</span><span class="sxs-lookup"><span data-stu-id="1916e-137">You can perform these actions by using Azure PowerShell cmdlets or by using hello Service Management REST API operations.</span></span> <span data-ttu-id="1916e-138">Les paramètres sont tooinstall requis et configurer certaines extensions.</span><span class="sxs-lookup"><span data-stu-id="1916e-138">Parameters are required tooinstall and set up some extensions.</span></span> <span data-ttu-id="1916e-139">Des paramètres publics et privés sont pris en charge pour les extensions.</span><span class="sxs-lookup"><span data-stu-id="1916e-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="1916e-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1916e-140">Azure PowerShell</span></span>
<span data-ttu-id="1916e-141">À l’aide des applets de commande PowerShell de Azure est hello plus simple façon tooadd et mise à jour extensions.</span><span class="sxs-lookup"><span data-stu-id="1916e-141">Using Azure PowerShell cmdlets is hello easiest way tooadd and update extensions.</span></span> <span data-ttu-id="1916e-142">Lorsque vous utilisez les applets de commande hello extension, la plupart des configuration hello d’extension de hello est effectuée pour vous.</span><span class="sxs-lookup"><span data-stu-id="1916e-142">When you use hello extension cmdlets, most of hello configuration of hello extension is done for you.</span></span> <span data-ttu-id="1916e-143">Dans certains cas, vous devrez peut-être tooprogrammatically Ajout d’une extension.</span><span class="sxs-lookup"><span data-stu-id="1916e-143">At times, you may need tooprogrammatically add an extension.</span></span> <span data-ttu-id="1916e-144">Lorsque vous devez toodo cela, vous devez fournir la configuration hello d’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="1916e-144">When you need toodo this, you must provide hello configuration of hello extension.</span></span>

<span data-ttu-id="1916e-145">Vous pouvez utiliser hello suivant d’applets de commande tooknow si une extension nécessite une configuration de paramètres publics et privés :</span><span class="sxs-lookup"><span data-stu-id="1916e-145">You can use hello following cmdlets tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="1916e-146">Pour les instances de rôles web ou les rôles de travail, vous pouvez utiliser hello **Get-AzureServiceAvailableExtension** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="1916e-146">For instances of web roles or worker roles, you can use hello **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="1916e-147">Pour les instances d’ordinateurs virtuels, vous pouvez utiliser hello **Get-AzureVMAvailableExtension** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="1916e-147">For instances of Virtual Machines, you can use hello **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="1916e-148">API REST de gestion de service</span><span class="sxs-lookup"><span data-stu-id="1916e-148">Service Management REST APIs</span></span>
<span data-ttu-id="1916e-149">Lorsque vous récupérez une liste d’extensions disponibles à l’aide des API REST de hello, vous recevez des informations sur l’extension de hello toobe configuré.</span><span class="sxs-lookup"><span data-stu-id="1916e-149">When you retrieve a listing of available extensions by using hello REST APIs, you receive information about how hello extension is toobe configured.</span></span> <span data-ttu-id="1916e-150">informations Hello retourné peuvent afficher des informations de paramètre représentées par un schéma public et un schéma privé.</span><span class="sxs-lookup"><span data-stu-id="1916e-150">hello information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="1916e-151">Valeurs de paramètres publics sont retournés dans les requêtes sur les instances de hello.</span><span class="sxs-lookup"><span data-stu-id="1916e-151">Public parameter values are returned in queries about hello instances.</span></span> <span data-ttu-id="1916e-152">Les valeurs de paramètres privés ne sont pas renvoyées.</span><span class="sxs-lookup"><span data-stu-id="1916e-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="1916e-153">Vous pouvez utiliser hello suivant l’API REST tooknow si une extension nécessite une configuration de paramètres publics et privés :</span><span class="sxs-lookup"><span data-stu-id="1916e-153">You can use hello following REST APIs tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="1916e-154">Pour les instances de rôles web ou des rôles de travail, hello **PublicConfigurationSchema** et **PrivateConfigurationSchema** éléments contiennent des informations de hello en réponse hello hello [liste Extensions disponibles](https://msdn.microsoft.com/library/dn169559.aspx) opération.</span><span class="sxs-lookup"><span data-stu-id="1916e-154">For instances of web roles or worker roles, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="1916e-155">Pour les instances de Machines virtuelles, hello **PublicConfigurationSchema** et **PrivateConfigurationSchema** éléments contiennent des informations de hello en réponse hello hello [liste Extensions de ressource](https://msdn.microsoft.com/library/dn495441.aspx) opération.</span><span class="sxs-lookup"><span data-stu-id="1916e-155">For instances of Virtual Machines, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="1916e-156">Des extensions peuvent également utiliser des configurations définies avec JSON.</span><span class="sxs-lookup"><span data-stu-id="1916e-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="1916e-157">Lorsque ces types d’extensions sont utilisés, vous devez uniquement hello **SampleConfig** élément est utilisé.</span><span class="sxs-lookup"><span data-stu-id="1916e-157">When these types of extensions are used, only hello **SampleConfig** element is used.</span></span>
> 
> 

