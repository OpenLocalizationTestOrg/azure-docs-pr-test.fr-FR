
Diagnostic des problèmes avec un service cloud Microsoft Azure requiert la collecte des journaux du service hello sur des machines virtuelles comme hello problèmes se produisent. Vous pouvez utiliser hello AzureLogCollector extension à la demande tooperfom une collecte unique des journaux à partir d’un ou plusieurs ordinateurs virtuels de services Cloud (à partir de rôles web et rôles de travail) et le transfert hello collectée fichiers tooan compte de stockage Azure – tout cela sans connexion à distance tooany Hello machines virtuelles.

> [!NOTE]
> Vous trouverez des descriptions pour la plupart des informations de hello connecté à http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.
> 
> 

Il existe deux modes de collection dépend des types hello de toobe fichiers collectés.

* Journaux des agents invités Azure uniquement (GA). Ce mode de collecte inclut tous les agents d’invité tooAzure connexes hello journaux et d’autres composants Azure.
* Tous les journaux (complète). Ce mode de collecte recueille tous les fichiers en mode GA plus :
  
  * journaux des événements système et d’application
  * Journaux d’erreurs HTTP
  * Journaux IIS
  * Fichiers journaux d’installation
  * autres journaux système.

Dans les deux modes de collecte, dossiers de collection de données supplémentaires peuvent être spécifiés à l’aide d’une collection de hello suivant la structure :

* **Nom**: nom hello de collection de hello, qui sera utilisée comme nom de hello de sous-dossier dans toobe de fichier zip hello collectées.
* **Emplacement**: hello chemin d’accès toohello dossier sur l’ordinateur virtuel de hello où les fichiers seront collectés.
* **Modèle de recherche**: modèle hello des noms de hello des fichiers toobe collectées. « * » constitue la valeur par défaut.
* **Récursive**: si les fichiers hello seront collectés de façon récursive sous le dossier de hello.

## <a name="prerequisites"></a>Composants requis
* Vous devez toohave un compte de stockage pour les fichiers zip toosave généré d’extension.
* Vous devez vous assurer que vous utilisez des applets de commande Azure PowerShell V0.8.0 ou version ultérieure. Pour plus d’informations, consultez la rubrique [Téléchargements Azure](https://azure.microsoft.com/downloads/).

## <a name="add-hello-extension"></a>Ajouter une extension de hello
Vous pouvez utiliser [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) applets de commande ou [API REST de gestion Service](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello extension AzureLogCollector.

Services de cloud computing, hello applet de commande Powershell Azure existante, **Set-AzureServiceExtension**, peut être extension de hello tooenable utilisés sur des instances de rôle Service de cloud computing. Chaque fois que cette extension est activée via cette applet de commande, la collecte des journaux est déclenchée sur hello sélectionné des instances de rôle des rôles sélectionnés.

Pour les ordinateurs virtuels, hello applet de commande Powershell Azure existante, **Set-AzureVMExtension**, peut être l’extension de hello tooenable utilisés sur des ordinateurs virtuels. Chaque fois que cette extension est activée via les applets de commande hello, collecte des journaux est déclenchée sur chaque instance.

En interne, cette extension utilise hello JSON en fonction de PublicConfiguration et PrivateConfiguration. Hello Voici disposition hello d’un exemple de JSON pour la configuration publique et privée.

### <a name="publicconfiguration"></a>PublicConfiguration
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

### <a name="privateconfiguration"></a>PrivateConfiguration
    {

    }

> [!NOTE]
> Cette extension n’a pas besoin de **privateConfiguration**. Vous pouvez fournir uniquement une structure vide pour hello **– PrivateConfiguration** argument.
> 
> 

Vous pouvez suivre l’une de deux de hello suivant les étapes tooadd hello AzureLogCollector tooone ou plusieurs instances d’un Service Cloud ou d’ordinateur virtuel des rôles sélectionnés, les déclencheurs hello collections sur chaque machine virtuelle de toorun et envoient les fichiers hello collectée tooAzure compte spécifié.

## <a name="adding-as-a-service-extension"></a>Ajout d’une Extension de service
1. Suivez l’abonnement de tooyour hello instructions tooconnect Azure PowerShell.
2. Spécifiez le nom du service hello, slot, rôles et toowhich d’instances de rôle vous le souhaitez tooadd et activez l’extension de AzureLogCollector hello.
   
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
3. Spécifiez le dossier de données supplémentaire hello pour lequel les fichiers seront collectés (cette étape est facultative).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > Vous pouvez utiliser le jeton `%roleroot%` lecteur racine rôle toospecify de hello, car il n’utilise pas un lecteur fixe.
   > 
   > 
4. Fournir le nom de compte de stockage Windows Azure hello et les fichiers de clé toowhich collectée seront téléchargés.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. Appelez hello SetAzureServiceLogCollector.ps1 (inclus à fin hello d’article de hello) en tant qu’extension AzureLogCollector de suit tooenable hello pour un Service Cloud. Une fois terminée l’exécution de hello, vous pouvez trouver le fichier hello téléchargé sous`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

Hello Voici définition hello de paramètres hello passé toohello script. (Également copié ci-dessous.)

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

* *ServiceName*: nom de votre service cloud.
* *Rôles*: une liste de rôles, tels que « WebRole1 » ou « WorkerRole1 ».
* *Instances*: une liste de noms hello d’instances de rôle séparés par des virgules, utilisez la chaîne de caractères génériques hello (« * ») pour toutes les instances de rôle.
* *Emplacement*: nom de l’emplacement. « Production » ou « Intermédiaire ».
* *Mode*: mode de collecte. « Complet » ou « GA ».
* *StorageAccountName*: nom du compte de stockage Azure pour le stockage des données recueillies.
* *StorageAccountKey*: nom de clé de compte de stockage Azure.
* *AdditionalDataLocationList*: une liste de hello suivant structure :
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a>Ajout d’une extension de machine virtuelle
Suivez l’abonnement de tooyour hello instructions tooconnect Azure PowerShell.

1. Spécifier le nom du service hello, machine virtuelle et le mode de collecte hello.
   
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
2. Fournir le nom de compte de stockage Windows Azure hello et les fichiers de clé toowhich collectée seront téléchargés.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. Appelez hello SetAzureVMLogCollector.ps1 (inclus à fin hello d’article de hello) en tant qu’extension AzureLogCollector de suit tooenable hello pour un Service Cloud. Une fois terminée l’exécution de hello, vous pouvez trouver le fichier hello téléchargé sous https://YouareStorageAccountName.BLOB.Core.Windows.NET/vmlogs

Hello Voici définition hello de paramètres hello passé toohello script. (Également copié ci-dessous.)

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

* ServiceName : est le nom de votre service cloud.
* Nom de hello VMName Hello machine virtuelle.
* Mode : mode de collecte. « Complet » ou « GA ».
* StorageAccountName : nom du compte de stockage Azure pour le stockage des données recueillies.
* StorageAccountKey : nom de clé de compte de stockage Azure.
* AdditionalDataLocationList : Une liste de hello suivant structure :

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a>Fichiers script PowerShell d’extension
SetAzureServiceLogCollector.ps1

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


SetAzureVMLogCollector.ps1

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

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez maintenant examiner ou copier vos journaux depuis un emplacement très simple.

