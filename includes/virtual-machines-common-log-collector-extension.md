
<span data-ttu-id="8a8df-101">Diagnostic des problèmes avec un service cloud Microsoft Azure requiert la collecte des journaux du service hello sur des machines virtuelles comme hello problèmes se produisent.</span><span class="sxs-lookup"><span data-stu-id="8a8df-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting hello service’s log files on virtual machines as hello issues occur.</span></span> <span data-ttu-id="8a8df-102">Vous pouvez utiliser hello AzureLogCollector extension à la demande tooperfom une collecte unique des journaux à partir d’un ou plusieurs ordinateurs virtuels de services Cloud (à partir de rôles web et rôles de travail) et le transfert hello collectée fichiers tooan compte de stockage Azure – tout cela sans connexion à distance tooany Hello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8a8df-102">You can use hello AzureLogCollector extension on-demand tooperfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer hello collected files tooan Azure storage account – all without remotely logging on tooany of hello VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="8a8df-103">Vous trouverez des descriptions pour la plupart des informations de hello connecté à http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span><span class="sxs-lookup"><span data-stu-id="8a8df-103">Descriptions for most of hello logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span></span>
> 
> 

<span data-ttu-id="8a8df-104">Il existe deux modes de collection dépend des types hello de toobe fichiers collectés.</span><span class="sxs-lookup"><span data-stu-id="8a8df-104">There are two modes of collection dependent on hello types of files toobe collected.</span></span>

* <span data-ttu-id="8a8df-105">Journaux des agents invités Azure uniquement (GA).</span><span class="sxs-lookup"><span data-stu-id="8a8df-105">Azure Guest Agent Logs only (GA).</span></span> <span data-ttu-id="8a8df-106">Ce mode de collecte inclut tous les agents d’invité tooAzure connexes hello journaux et d’autres composants Azure.</span><span class="sxs-lookup"><span data-stu-id="8a8df-106">This collection mode includes all hello logs related tooAzure guest agents and other Azure components.</span></span>
* <span data-ttu-id="8a8df-107">Tous les journaux (complète).</span><span class="sxs-lookup"><span data-stu-id="8a8df-107">All Logs (Full).</span></span> <span data-ttu-id="8a8df-108">Ce mode de collecte recueille tous les fichiers en mode GA plus :</span><span class="sxs-lookup"><span data-stu-id="8a8df-108">This collection mode will collect all files in GA mode plus:</span></span>
  
  * <span data-ttu-id="8a8df-109">journaux des événements système et d’application</span><span class="sxs-lookup"><span data-stu-id="8a8df-109">system and application event logs</span></span>
  * <span data-ttu-id="8a8df-110">Journaux d’erreurs HTTP</span><span class="sxs-lookup"><span data-stu-id="8a8df-110">HTTP error logs</span></span>
  * <span data-ttu-id="8a8df-111">Journaux IIS</span><span class="sxs-lookup"><span data-stu-id="8a8df-111">IIS Logs</span></span>
  * <span data-ttu-id="8a8df-112">Fichiers journaux d’installation</span><span class="sxs-lookup"><span data-stu-id="8a8df-112">Setup logs</span></span>
  * <span data-ttu-id="8a8df-113">autres journaux système.</span><span class="sxs-lookup"><span data-stu-id="8a8df-113">other system logs</span></span>

<span data-ttu-id="8a8df-114">Dans les deux modes de collecte, dossiers de collection de données supplémentaires peuvent être spécifiés à l’aide d’une collection de hello suivant la structure :</span><span class="sxs-lookup"><span data-stu-id="8a8df-114">In both collection modes, additional data collection folders can be specified by using a collection of hello following structure:</span></span>

* <span data-ttu-id="8a8df-115">**Nom**: nom hello de collection de hello, qui sera utilisée comme nom de hello de sous-dossier dans toobe de fichier zip hello collectées.</span><span class="sxs-lookup"><span data-stu-id="8a8df-115">**Name**: hello name of hello collection, which will be used as hello name of subfolder inside hello zip file toobe collected.</span></span>
* <span data-ttu-id="8a8df-116">**Emplacement**: hello chemin d’accès toohello dossier sur l’ordinateur virtuel de hello où les fichiers seront collectés.</span><span class="sxs-lookup"><span data-stu-id="8a8df-116">**Location**: hello path toohello folder on hello virtual machine where file will be collected.</span></span>
* <span data-ttu-id="8a8df-117">**Modèle de recherche**: modèle hello des noms de hello des fichiers toobe collectées.</span><span class="sxs-lookup"><span data-stu-id="8a8df-117">**SearchPattern**: hello pattern of hello names of files toobe collected.</span></span> <span data-ttu-id="8a8df-118">« * » constitue la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="8a8df-118">Default is “*”</span></span>
* <span data-ttu-id="8a8df-119">**Récursive**: si les fichiers hello seront collectés de façon récursive sous le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="8a8df-119">**Recursive**: if hello files will be collected recursively under hello folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a8df-120">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8a8df-120">Prerequisites</span></span>
* <span data-ttu-id="8a8df-121">Vous devez toohave un compte de stockage pour les fichiers zip toosave généré d’extension.</span><span class="sxs-lookup"><span data-stu-id="8a8df-121">You need toohave a storage account for extension toosave generated zip files.</span></span>
* <span data-ttu-id="8a8df-122">Vous devez vous assurer que vous utilisez des applets de commande Azure PowerShell V0.8.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8a8df-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span></span> <span data-ttu-id="8a8df-123">Pour plus d’informations, consultez la rubrique [Téléchargements Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8a8df-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>

## <a name="add-hello-extension"></a><span data-ttu-id="8a8df-124">Ajouter une extension de hello</span><span class="sxs-lookup"><span data-stu-id="8a8df-124">Add hello extension</span></span>
<span data-ttu-id="8a8df-125">Vous pouvez utiliser [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) applets de commande ou [API REST de gestion Service](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello extension AzureLogCollector.</span><span class="sxs-lookup"><span data-stu-id="8a8df-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector extension.</span></span>

<span data-ttu-id="8a8df-126">Services de cloud computing, hello applet de commande Powershell Azure existante, **Set-AzureServiceExtension**, peut être extension de hello tooenable utilisés sur des instances de rôle Service de cloud computing.</span><span class="sxs-lookup"><span data-stu-id="8a8df-126">For Cloud Services, hello existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used tooenable hello extension on Cloud Service role instances.</span></span> <span data-ttu-id="8a8df-127">Chaque fois que cette extension est activée via cette applet de commande, la collecte des journaux est déclenchée sur hello sélectionné des instances de rôle des rôles sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="8a8df-127">Every time this extension is enabled through this cmdlet, log collection is triggered on hello selected role instances of selected roles.</span></span>

<span data-ttu-id="8a8df-128">Pour les ordinateurs virtuels, hello applet de commande Powershell Azure existante, **Set-AzureVMExtension**, peut être l’extension de hello tooenable utilisés sur des ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="8a8df-128">For Virtual Machines, hello existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used tooenable hello extension on Virtual Machines.</span></span> <span data-ttu-id="8a8df-129">Chaque fois que cette extension est activée via les applets de commande hello, collecte des journaux est déclenchée sur chaque instance.</span><span class="sxs-lookup"><span data-stu-id="8a8df-129">Every time this extension is enabled through hello cmdlets, log collection is triggered on each instance.</span></span>

<span data-ttu-id="8a8df-130">En interne, cette extension utilise hello JSON en fonction de PublicConfiguration et PrivateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="8a8df-130">Internally, this extension uses hello JSON-based PublicConfiguration and PrivateConfiguration.</span></span> <span data-ttu-id="8a8df-131">Hello Voici disposition hello d’un exemple de JSON pour la configuration publique et privée.</span><span class="sxs-lookup"><span data-stu-id="8a8df-131">hello following is hello layout of a sample JSON for public and private configuration.</span></span>

### <a name="publicconfiguration"></a><span data-ttu-id="8a8df-132">PublicConfiguration</span><span class="sxs-lookup"><span data-stu-id="8a8df-132">PublicConfiguration</span></span>
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a><span data-ttu-id="8a8df-133">PrivateConfiguration</span><span class="sxs-lookup"><span data-stu-id="8a8df-133">PrivateConfiguration</span></span>
    {

    }

> [!NOTE]
> <span data-ttu-id="8a8df-134">Cette extension n’a pas besoin de **privateConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="8a8df-134">This extension doesn’t need **privateConfiguration**.</span></span> <span data-ttu-id="8a8df-135">Vous pouvez fournir uniquement une structure vide pour hello **– PrivateConfiguration** argument.</span><span class="sxs-lookup"><span data-stu-id="8a8df-135">You can just provide an empty structure for hello **–PrivateConfiguration** argument.</span></span>
> 
> 

<span data-ttu-id="8a8df-136">Vous pouvez suivre l’une de deux de hello suivant les étapes tooadd hello AzureLogCollector tooone ou plusieurs instances d’un Service Cloud ou d’ordinateur virtuel des rôles sélectionnés, les déclencheurs hello collections sur chaque machine virtuelle de toorun et envoient les fichiers hello collectée tooAzure compte spécifié.</span><span class="sxs-lookup"><span data-stu-id="8a8df-136">You can follow one of hello two following steps tooadd hello AzureLogCollector tooone or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers hello collections on each VM toorun and send hello collected files tooAzure account specified.</span></span>

## <a name="adding-as-a-service-extension"></a><span data-ttu-id="8a8df-137">Ajout d’une Extension de service</span><span class="sxs-lookup"><span data-stu-id="8a8df-137">Adding as a Service Extension</span></span>
1. <span data-ttu-id="8a8df-138">Suivez l’abonnement de tooyour hello instructions tooconnect Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a8df-138">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>
2. <span data-ttu-id="8a8df-139">Spécifiez le nom du service hello, slot, rôles et toowhich d’instances de rôle vous le souhaitez tooadd et activez l’extension de AzureLogCollector hello.</span><span class="sxs-lookup"><span data-stu-id="8a8df-139">Specify hello service name, slot, roles, and role instances toowhich you want tooadd and enable hello AzureLogCollector extension.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. <span data-ttu-id="8a8df-140">Spécifiez le dossier de données supplémentaire hello pour lequel les fichiers seront collectés (cette étape est facultative).</span><span class="sxs-lookup"><span data-stu-id="8a8df-140">Specify hello additional data folder for which files will be collected (this step is optional).</span></span>
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > <span data-ttu-id="8a8df-141">Vous pouvez utiliser le jeton `%roleroot%` lecteur racine rôle toospecify de hello, car il n’utilise pas un lecteur fixe.</span><span class="sxs-lookup"><span data-stu-id="8a8df-141">You can use token `%roleroot%` toospecify hello role root drive since it doesn’t use a fixed drive.</span></span>
   > 
   > 
4. <span data-ttu-id="8a8df-142">Fournir le nom de compte de stockage Windows Azure hello et les fichiers de clé toowhich collectée seront téléchargés.</span><span class="sxs-lookup"><span data-stu-id="8a8df-142">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. <span data-ttu-id="8a8df-143">Appelez hello SetAzureServiceLogCollector.ps1 (inclus à fin hello d’article de hello) en tant qu’extension AzureLogCollector de suit tooenable hello pour un Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="8a8df-143">Call hello SetAzureServiceLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="8a8df-144">Une fois terminée l’exécution de hello, vous pouvez trouver le fichier hello téléchargé sous`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span><span class="sxs-lookup"><span data-stu-id="8a8df-144">Once hello execution is completed, you can find hello uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span></span>
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

<span data-ttu-id="8a8df-145">Hello Voici définition hello de paramètres hello passé toohello script.</span><span class="sxs-lookup"><span data-stu-id="8a8df-145">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="8a8df-146">(Également copié ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="8a8df-146">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* <span data-ttu-id="8a8df-147">*ServiceName*: nom de votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="8a8df-147">*ServiceName*: Your cloud service name.</span></span>
* <span data-ttu-id="8a8df-148">*Rôles*: une liste de rôles, tels que « WebRole1 » ou « WorkerRole1 ».</span><span class="sxs-lookup"><span data-stu-id="8a8df-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span></span>
* <span data-ttu-id="8a8df-149">*Instances*: une liste de noms hello d’instances de rôle séparés par des virgules, utilisez la chaîne de caractères génériques hello (« * ») pour toutes les instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="8a8df-149">*Instances*: A list of hello names of role instances separated by comma -- use hello wildcard string (“*”) for all role instances.</span></span>
* <span data-ttu-id="8a8df-150">*Emplacement*: nom de l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="8a8df-150">*Slot*: Slot name.</span></span> <span data-ttu-id="8a8df-151">« Production » ou « Intermédiaire ».</span><span class="sxs-lookup"><span data-stu-id="8a8df-151">“Production” or “Staging”.</span></span>
* <span data-ttu-id="8a8df-152">*Mode*: mode de collecte.</span><span class="sxs-lookup"><span data-stu-id="8a8df-152">*Mode*: Collection mode.</span></span> <span data-ttu-id="8a8df-153">« Complet » ou « GA ».</span><span class="sxs-lookup"><span data-stu-id="8a8df-153">“Full” or “GA”.</span></span>
* <span data-ttu-id="8a8df-154">*StorageAccountName*: nom du compte de stockage Azure pour le stockage des données recueillies.</span><span class="sxs-lookup"><span data-stu-id="8a8df-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="8a8df-155">*StorageAccountKey*: nom de clé de compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8a8df-155">*StorageAccountKey*: Name of Azure storage account key.</span></span>
* <span data-ttu-id="8a8df-156">*AdditionalDataLocationList*: une liste de hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="8a8df-156">*AdditionalDataLocationList*: A list of hello following structure:</span></span>
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a><span data-ttu-id="8a8df-157">Ajout d’une extension de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8a8df-157">Adding as a VM Extension</span></span>
<span data-ttu-id="8a8df-158">Suivez l’abonnement de tooyour hello instructions tooconnect Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8a8df-158">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>

1. <span data-ttu-id="8a8df-159">Spécifier le nom du service hello, machine virtuelle et le mode de collecte hello.</span><span class="sxs-lookup"><span data-stu-id="8a8df-159">Specify hello service name, VM, and hello collection mode.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. <span data-ttu-id="8a8df-160">Fournir le nom de compte de stockage Windows Azure hello et les fichiers de clé toowhich collectée seront téléchargés.</span><span class="sxs-lookup"><span data-stu-id="8a8df-160">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. <span data-ttu-id="8a8df-161">Appelez hello SetAzureVMLogCollector.ps1 (inclus à fin hello d’article de hello) en tant qu’extension AzureLogCollector de suit tooenable hello pour un Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="8a8df-161">Call hello SetAzureVMLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="8a8df-162">Une fois terminée l’exécution de hello, vous pouvez trouver le fichier hello téléchargé sous https://YouareStorageAccountName.BLOB.Core.Windows.NET/vmlogs</span><span class="sxs-lookup"><span data-stu-id="8a8df-162">Once hello execution is completed, you can find hello uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span></span>

<span data-ttu-id="8a8df-163">Hello Voici définition hello de paramètres hello passé toohello script.</span><span class="sxs-lookup"><span data-stu-id="8a8df-163">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="8a8df-164">(Également copié ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="8a8df-164">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* <span data-ttu-id="8a8df-165">ServiceName : est le nom de votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="8a8df-165">ServiceName: Your cloud service name.</span></span>
* <span data-ttu-id="8a8df-166">Nom de hello VMName Hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8a8df-166">VMName hello name of hello VM.</span></span>
* <span data-ttu-id="8a8df-167">Mode : mode de collecte.</span><span class="sxs-lookup"><span data-stu-id="8a8df-167">Mode: Collection mode.</span></span> <span data-ttu-id="8a8df-168">« Complet » ou « GA ».</span><span class="sxs-lookup"><span data-stu-id="8a8df-168">“Full” or “GA”.</span></span>
* <span data-ttu-id="8a8df-169">StorageAccountName : nom du compte de stockage Azure pour le stockage des données recueillies.</span><span class="sxs-lookup"><span data-stu-id="8a8df-169">StorageAccountName: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="8a8df-170">StorageAccountKey : nom de clé de compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8a8df-170">StorageAccountKey: Name of Azure storage account key.</span></span>
* <span data-ttu-id="8a8df-171">AdditionalDataLocationList : Une liste de hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="8a8df-171">AdditionalDataLocationList: A list of hello following structure:</span></span>

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a><span data-ttu-id="8a8df-172">Fichiers script PowerShell d’extension</span><span class="sxs-lookup"><span data-stu-id="8a8df-172">Extention PowerShell Script files</span></span>
<span data-ttu-id="8a8df-173">SetAzureServiceLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="8a8df-173">SetAzureServiceLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  hello value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


<span data-ttu-id="8a8df-174">SetAzureVMLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="8a8df-174">SetAzureVMLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a><span data-ttu-id="8a8df-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8a8df-175">Next Steps</span></span>
<span data-ttu-id="8a8df-176">Vous pouvez maintenant examiner ou copier vos journaux depuis un emplacement très simple.</span><span class="sxs-lookup"><span data-stu-id="8a8df-176">Now you can examine or copy your logs from one very simple location.</span></span>

