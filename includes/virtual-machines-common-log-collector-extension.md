
<span data-ttu-id="3a044-101">Les problèmes de diagnostic avec un service cloud Microsoft Azure nécessite la collecte des fichiers journaux de service sur les machines virtuelles lorsque les problèmes surviennent.</span><span class="sxs-lookup"><span data-stu-id="3a044-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting the service’s log files on virtual machines as the issues occur.</span></span> <span data-ttu-id="3a044-102">Vous pouvez utiliser l’extension AzureLogCollector à la demande pour exécuter une collecte unique de journaux depuis une ou plusieurs machines virtuelles de Service Cloud (à partir des rôles web et de travail) et transférer les fichiers collectés dans un compte de stockage Azure, le tout sans connexion à distance à une machine virtuelle quelconque.</span><span class="sxs-lookup"><span data-stu-id="3a044-102">You can use the AzureLogCollector extension on-demand to perfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer the collected files to an Azure storage account – all without remotely logging on to any of the VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="3a044-103">La description de la plupart des informations journalisées est accessible à l’adresse http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span><span class="sxs-lookup"><span data-stu-id="3a044-103">Descriptions for most of the logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span></span>
> 
> 

<span data-ttu-id="3a044-104">Il existe deux modes de collecte dépendant des types de fichiers à recueillir.</span><span class="sxs-lookup"><span data-stu-id="3a044-104">There are two modes of collection dependent on the types of files to be collected.</span></span>

* <span data-ttu-id="3a044-105">Journaux des agents invités Azure uniquement (GA).</span><span class="sxs-lookup"><span data-stu-id="3a044-105">Azure Guest Agent Logs only (GA).</span></span> <span data-ttu-id="3a044-106">Ce mode de collecte inclut tous les journaux liés aux agents invités Azure et d’autres composants Azure.</span><span class="sxs-lookup"><span data-stu-id="3a044-106">This collection mode includes all the logs related to Azure guest agents and other Azure components.</span></span>
* <span data-ttu-id="3a044-107">Tous les journaux (complète).</span><span class="sxs-lookup"><span data-stu-id="3a044-107">All Logs (Full).</span></span> <span data-ttu-id="3a044-108">Ce mode de collecte recueille tous les fichiers en mode GA plus :</span><span class="sxs-lookup"><span data-stu-id="3a044-108">This collection mode will collect all files in GA mode plus:</span></span>
  
  * <span data-ttu-id="3a044-109">journaux des événements système et d’application</span><span class="sxs-lookup"><span data-stu-id="3a044-109">system and application event logs</span></span>
  * <span data-ttu-id="3a044-110">Journaux d’erreurs HTTP</span><span class="sxs-lookup"><span data-stu-id="3a044-110">HTTP error logs</span></span>
  * <span data-ttu-id="3a044-111">Journaux IIS</span><span class="sxs-lookup"><span data-stu-id="3a044-111">IIS Logs</span></span>
  * <span data-ttu-id="3a044-112">Fichiers journaux d’installation</span><span class="sxs-lookup"><span data-stu-id="3a044-112">Setup logs</span></span>
  * <span data-ttu-id="3a044-113">autres journaux système.</span><span class="sxs-lookup"><span data-stu-id="3a044-113">other system logs</span></span>

<span data-ttu-id="3a044-114">Dans les deux modes de collecte, les dossiers de collecte de données supplémentaires peuvent être spécifiés à l’aide d’une collection de la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="3a044-114">In both collection modes, additional data collection folders can be specified by using a collection of the following structure:</span></span>

* <span data-ttu-id="3a044-115">**Nom**: nom de la collection qui sera utilisé comme nom de sous-dossier dans le fichier zip à collecter.</span><span class="sxs-lookup"><span data-stu-id="3a044-115">**Name**: The name of the collection, which will be used as the name of subfolder inside the zip file to be collected.</span></span>
* <span data-ttu-id="3a044-116">**Emplacement**: chemin d’accès au dossier sur l’ordinateur virtuel dans lequel les fichiers seront collectés.</span><span class="sxs-lookup"><span data-stu-id="3a044-116">**Location**: The path to the folder on the virtual machine where file will be collected.</span></span>
* <span data-ttu-id="3a044-117">**Modèle de recherche**: modèle des noms de fichiers à collecter.</span><span class="sxs-lookup"><span data-stu-id="3a044-117">**SearchPattern**: The pattern of the names of files to be collected.</span></span> <span data-ttu-id="3a044-118">« * » constitue la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="3a044-118">Default is “*”</span></span>
* <span data-ttu-id="3a044-119">**Récursive**: si les fichiers sont collectés de façon récursive sous le dossier.</span><span class="sxs-lookup"><span data-stu-id="3a044-119">**Recursive**: if the files will be collected recursively under the folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a044-120">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3a044-120">Prerequisites</span></span>
* <span data-ttu-id="3a044-121">Vous devez disposer d’un compte de stockage pour une extension pour enregistrer les fichiers zip générés.</span><span class="sxs-lookup"><span data-stu-id="3a044-121">You need to have a storage account for extension to save generated zip files.</span></span>
* <span data-ttu-id="3a044-122">Vous devez vous assurer que vous utilisez des applets de commande Azure PowerShell V0.8.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3a044-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span></span> <span data-ttu-id="3a044-123">Pour plus d’informations, consultez la rubrique [Téléchargements Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3a044-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>

## <a name="add-the-extension"></a><span data-ttu-id="3a044-124">Ajouter l’extension</span><span class="sxs-lookup"><span data-stu-id="3a044-124">Add the extension</span></span>
<span data-ttu-id="3a044-125">Vous pouvez utiliser les applets de commande [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) ou les [API REST Gestion des services](https://msdn.microsoft.com/library/ee460799.aspx) pour ajouter l’extension AzureLogCollector.</span><span class="sxs-lookup"><span data-stu-id="3a044-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) to add the AzureLogCollector extension.</span></span>

<span data-ttu-id="3a044-126">Pour les services cloud, l’applet de commande Powershell de Azure existante **Set-AzureServiceExtension**, peut être utilisée pour activer l’extension sur les instances de rôle de service cloud.</span><span class="sxs-lookup"><span data-stu-id="3a044-126">For Cloud Services, the existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used to enable the extension on Cloud Service role instances.</span></span> <span data-ttu-id="3a044-127">Chaque fois que cette extension est activée via cette applet de commande, la collecte des journaux est déclenchée sur les instances de rôle choisies pour les rôles sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="3a044-127">Every time this extension is enabled through this cmdlet, log collection is triggered on the selected role instances of selected roles.</span></span>

<span data-ttu-id="3a044-128">Pour les machines virtuelles, l’applet de commande Azure Powershell existante **Set-AzureVMExtension**peut être utilisée pour activer l’extension sur des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="3a044-128">For Virtual Machines, the existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used to enable the extension on Virtual Machines.</span></span> <span data-ttu-id="3a044-129">À chaque fois que cette extension est activée via les applets de commande, la collecte des journaux est déclenchée sur chaque instance.</span><span class="sxs-lookup"><span data-stu-id="3a044-129">Every time this extension is enabled through the cmdlets, log collection is triggered on each instance.</span></span>

<span data-ttu-id="3a044-130">En interne, cette extension utilise les configurations PublicConfiguration et PrivateConfiguration basées sur JSON.</span><span class="sxs-lookup"><span data-stu-id="3a044-130">Internally, this extension uses the JSON-based PublicConfiguration and PrivateConfiguration.</span></span> <span data-ttu-id="3a044-131">Voici la disposition d’un exemple de JSON pour la configuration publique et privée.</span><span class="sxs-lookup"><span data-stu-id="3a044-131">The following is the layout of a sample JSON for public and private configuration.</span></span>

### <a name="publicconfiguration"></a><span data-ttu-id="3a044-132">PublicConfiguration</span><span class="sxs-lookup"><span data-stu-id="3a044-132">PublicConfiguration</span></span>
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri to your storage account with sp=wl",
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

### <a name="privateconfiguration"></a><span data-ttu-id="3a044-133">PrivateConfiguration</span><span class="sxs-lookup"><span data-stu-id="3a044-133">PrivateConfiguration</span></span>
    {

    }

> [!NOTE]
> <span data-ttu-id="3a044-134">Cette extension n’a pas besoin de **privateConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="3a044-134">This extension doesn’t need **privateConfiguration**.</span></span> <span data-ttu-id="3a044-135">Vous pouvez simplement fournir une structure vide pour l’argument **–PrivateConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="3a044-135">You can just provide an empty structure for the **–PrivateConfiguration** argument.</span></span>
> 
> 

<span data-ttu-id="3a044-136">Vous pouvez exécuter l’une des deux étapes suivantes pour ajouter AzureLogCollector à une ou plusieurs instances d’un Service Cloud ou d’une machine virtuelle des rôles sélectionnés, ce qui déclenche les collectes sur chaque machine virtuelle à exécuter et envoyer aux fichiers recueillis à un compte Azure spécifié.</span><span class="sxs-lookup"><span data-stu-id="3a044-136">You can follow one of the two following steps to add the AzureLogCollector to one or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers the collections on each VM to run and send the collected files to Azure account specified.</span></span>

## <a name="adding-as-a-service-extension"></a><span data-ttu-id="3a044-137">Ajout d’une Extension de service</span><span class="sxs-lookup"><span data-stu-id="3a044-137">Adding as a Service Extension</span></span>
1. <span data-ttu-id="3a044-138">Suivez les instructions pour connecter Azure PowerShell à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="3a044-138">Follow the instructions to connect Azure PowerShell to your subscription.</span></span>
2. <span data-ttu-id="3a044-139">Spécifiez le nom de service, l’emplacement, les rôles et les instances de rôle auxquels vous souhaitez ajouter et activer l’extension AzureLogCollector.</span><span class="sxs-lookup"><span data-stu-id="3a044-139">Specify the service name, slot, roles, and role instances to which you want to add and enable the AzureLogCollector extension.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify the slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified the roles on which the extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify the instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify the collection mode, "Full" or "GA"
        $mode = "GA"
3. <span data-ttu-id="3a044-140">Spécifiez le dossier de données supplémentaires pour lequel les fichiers seront collectés (cette étape est facultative).</span><span class="sxs-lookup"><span data-stu-id="3a044-140">Specify the additional data folder for which files will be collected (this step is optional).</span></span>
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > <span data-ttu-id="3a044-141">Vous pouvez utiliser le jeton `%roleroot%` pour spécifier le lecteur racine de rôle, car il n’utilise pas un lecteur fixe.</span><span class="sxs-lookup"><span data-stu-id="3a044-141">You can use token `%roleroot%` to specify the role root drive since it doesn’t use a fixed drive.</span></span>
   > 
   > 
4. <span data-ttu-id="3a044-142">Fournissez le nom du compte de stockage Azure et la clé vers laquelle les fichiers recueillis seront téléchargés.</span><span class="sxs-lookup"><span data-stu-id="3a044-142">Provide the Azure storage account name and key to which collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. <span data-ttu-id="3a044-143">Appelez le SetAzureServiceLogCollector.ps1 (inclus à la fin de l’article) comme suit pour activer l’extension AzureLogCollector pour un Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="3a044-143">Call the SetAzureServiceLogCollector.ps1 (included at the end of the article) as follows to enable the AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="3a044-144">Une fois l’exécution achevée, vous trouverez le fichier téléchargé sous `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span><span class="sxs-lookup"><span data-stu-id="3a044-144">Once the execution is completed, you can find the uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span></span>
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

<span data-ttu-id="3a044-145">Voici la définition des paramètres transmis au script.</span><span class="sxs-lookup"><span data-stu-id="3a044-145">The following is the definition of the parameters passed to the script.</span></span> <span data-ttu-id="3a044-146">(Également copié ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="3a044-146">(This is copied below as well.)</span></span>

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

* <span data-ttu-id="3a044-147">*ServiceName*: nom de votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="3a044-147">*ServiceName*: Your cloud service name.</span></span>
* <span data-ttu-id="3a044-148">*Rôles*: une liste de rôles, tels que « WebRole1 » ou « WorkerRole1 ».</span><span class="sxs-lookup"><span data-stu-id="3a044-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span></span>
* <span data-ttu-id="3a044-149">*Instances*: liste de noms des instances de rôle séparés par des virgules, utilisez la chaîne de caractères génériques (« * ») pour toutes les instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="3a044-149">*Instances*: A list of the names of role instances separated by comma -- use the wildcard string (“*”) for all role instances.</span></span>
* <span data-ttu-id="3a044-150">*Emplacement*: nom de l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="3a044-150">*Slot*: Slot name.</span></span> <span data-ttu-id="3a044-151">« Production » ou « Intermédiaire ».</span><span class="sxs-lookup"><span data-stu-id="3a044-151">“Production” or “Staging”.</span></span>
* <span data-ttu-id="3a044-152">*Mode*: mode de collecte.</span><span class="sxs-lookup"><span data-stu-id="3a044-152">*Mode*: Collection mode.</span></span> <span data-ttu-id="3a044-153">« Complet » ou « GA ».</span><span class="sxs-lookup"><span data-stu-id="3a044-153">“Full” or “GA”.</span></span>
* <span data-ttu-id="3a044-154">*StorageAccountName*: nom du compte de stockage Azure pour le stockage des données recueillies.</span><span class="sxs-lookup"><span data-stu-id="3a044-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="3a044-155">*StorageAccountKey*: nom de clé de compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3a044-155">*StorageAccountKey*: Name of Azure storage account key.</span></span>
* <span data-ttu-id="3a044-156">*AdditionalDataLocationList*: liste obéissant à la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="3a044-156">*AdditionalDataLocationList*: A list of the following structure:</span></span>
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a><span data-ttu-id="3a044-157">Ajout d’une extension de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="3a044-157">Adding as a VM Extension</span></span>
<span data-ttu-id="3a044-158">Suivez les instructions pour connecter Azure PowerShell à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="3a044-158">Follow the instructions to connect Azure PowerShell to your subscription.</span></span>

1. <span data-ttu-id="3a044-159">Spécifiez le nom du service, la machine virtuelle et le mode de collecte.</span><span class="sxs-lookup"><span data-stu-id="3a044-159">Specify the service name, VM, and the collection mode.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify the VM name
        $VMName = "'YourVMName'"
   
        #Specify the collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify the additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. <span data-ttu-id="3a044-160">Fournissez le nom du compte de stockage Azure et la clé vers laquelle les fichiers recueillis seront téléchargés.</span><span class="sxs-lookup"><span data-stu-id="3a044-160">Provide the Azure storage account name and key to which collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. <span data-ttu-id="3a044-161">Appelez le SetAzureVMLogCollector.ps1 (inclus à la fin de l’article) comme suit pour activer l’extension AzureLogCollector pour Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="3a044-161">Call the SetAzureVMLogCollector.ps1 (included at the end of the article) as follows to enable the AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="3a044-162">Une fois l’exécution effectuée, le fichier chargé est accessible sous https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span><span class="sxs-lookup"><span data-stu-id="3a044-162">Once the execution is completed, you can find the uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span></span>

<span data-ttu-id="3a044-163">Voici la définition des paramètres transmis au script.</span><span class="sxs-lookup"><span data-stu-id="3a044-163">The following is the definition of the parameters passed to the script.</span></span> <span data-ttu-id="3a044-164">(Également copié ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="3a044-164">(This is copied below as well.)</span></span>

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

* <span data-ttu-id="3a044-165">ServiceName : est le nom de votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="3a044-165">ServiceName: Your cloud service name.</span></span>
* <span data-ttu-id="3a044-166">VMName Nom de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3a044-166">VMName The name of the VM.</span></span>
* <span data-ttu-id="3a044-167">Mode : mode de collecte.</span><span class="sxs-lookup"><span data-stu-id="3a044-167">Mode: Collection mode.</span></span> <span data-ttu-id="3a044-168">« Complet » ou « GA ».</span><span class="sxs-lookup"><span data-stu-id="3a044-168">“Full” or “GA”.</span></span>
* <span data-ttu-id="3a044-169">StorageAccountName : nom du compte de stockage Azure pour le stockage des données recueillies.</span><span class="sxs-lookup"><span data-stu-id="3a044-169">StorageAccountName: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="3a044-170">StorageAccountKey : nom de clé de compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3a044-170">StorageAccountKey: Name of Azure storage account key.</span></span>
* <span data-ttu-id="3a044-171">AdditionalDataLocationList : liste de la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="3a044-171">AdditionalDataLocationList: A list of the following structure:</span></span>

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a><span data-ttu-id="3a044-172">Fichiers script PowerShell d’extension</span><span class="sxs-lookup"><span data-stu-id="3a044-172">Extention PowerShell Script files</span></span>
<span data-ttu-id="3a044-173">SetAzureServiceLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="3a044-173">SetAzureServiceLogCollector.ps1</span></span>

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
    else  #For all instances if not specified.  The value should be a space or *
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
    #we need to get the Sasuri from StorageAccount and containers
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
    #Add AdditionalData to collect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it to JSON format
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
    #This is an optional step: generate a sasUri to the container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "The container for uploaded file can be accessed using this link:`r`n$sasuri"


<span data-ttu-id="3a044-174">SetAzureVMLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="3a044-174">SetAzureVMLogCollector.ps1</span></span>

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
    #we need to get the Sasuri from StorageAccount and containers
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
    #Add AdditionalData to collect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it to JSON format
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
                #We will check the VM status to find if operation by extension has been completed or not. The completion of the operation,either succeed or fail, can be indicated by
                #the presence of SubstatusList field.
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
                              Write-Output "Waiting for operation to complete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access to the file, we can generate a read-only SasUri directly to the file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "The uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove the extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, the extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, the extension cannot be enabled"
    }

## <a name="next-steps"></a><span data-ttu-id="3a044-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3a044-175">Next Steps</span></span>
<span data-ttu-id="3a044-176">Vous pouvez maintenant examiner ou copier vos journaux depuis un emplacement très simple.</span><span class="sxs-lookup"><span data-stu-id="3a044-176">Now you can examine or copy your logs from one very simple location.</span></span>

