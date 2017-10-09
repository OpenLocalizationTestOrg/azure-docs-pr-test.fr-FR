


## <a name="using-vm-extensions"></a>Utilisation d'extensions de machines virtuelles
Les Extensions de machine virtuelle Azure implémenter des comportements ou des fonctionnalités qui soit à autres programmes de fonctionner sur des machines virtuelles Azure (par exemple, hello **WebDeployForVSDevTest** extension permet de déployer des solutions Visual Studio tooWeb sur votre machine virtuelle Azure) ou fournir Hello possibilité pour vous toointeract avec hello VM toosupport un autre comportement (par exemple, vous pouvez utiliser PowerShell, hello CLI d’Azure et les autres clients tooreset les extensions VM accès hello ou modifier les valeurs de l’accès à distance sur votre machine virtuelle Azure).

> [!IMPORTANT]
> Pour obtenir une liste complète des extensions en fonctionnalités hello prises en charge, consultez [fonctionnalités et Extensions de machine virtuelle Azure](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Étant donné que chaque extension de machine virtuelle prend en charge une fonctionnalité spécifique, exactement ce que vous pouvez et ne peut pas faire avec une extension dépend hello extension. Par conséquent, avant de modifier votre machine virtuelle, assurez-vous que vous avez lu la documentation hello pour hello machine virtuelle de l’Extension toouse. La suppression de certaines extensions de machine virtuelle n'est pas prise en charge. D'autres ont des propriétés qui peuvent être définies et qui modifient radicalement le comportement de la machine virtuelle.
> 
> 

les tâches les plus courantes Hello sont :

1. Recherche d'extensions disponibles
2. Mise à jour des extensions chargées
3. Ajout d'extensions
4. Suppression d'extensions

## <a name="find-available-extensions"></a>Recherche d'extensions disponibles
Vous pouvez localiser l’extension et obtenir des informations étendues en utilisant :

* PowerShell
* Interface de ligne de commande interplateforme Azure (Azure CLI)
* API REST de gestion de service

### <a name="azure-powershell"></a>Azure PowerShell
Certaines extensions ont les applets de commande PowerShell sont toothem spécifique, ce qui peut faciliter leur configuration à partir de PowerShell ; mais hello applets de commande suivantes fonctionnent pour toutes les extensions de machine virtuelle.

Vous pouvez utiliser hello suivant d’applets de commande tooobtain plus d’informations sur les extensions disponibles :

* Pour les instances de rôles web ou les rôles de travail, vous pouvez utiliser hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) applet de commande.
* Pour les instances d’ordinateurs virtuels, vous pouvez utiliser hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) applet de commande.
  
   Par exemple, hello suivant exemple de code montre comment toolist les informations de hello **IaaSDiagnostics** extension à l’aide de PowerShell.
  
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

### <a name="azure-command-line-interface-azure-cli"></a>Interface de ligne de commande Azure (Azure CLI)
Certaines extensions ont des commandes CLI d’Azure toothem spécifique (hello Extension de machine virtuelle Docker est un exemple), ce qui peut faciliter leur configuration ; mais suivant de hello des commandes pour toutes les extensions de machine virtuelle.

Vous pouvez utiliser hello **liste des extensions de machine virtuelle azure** tooobtain plus d’informations sur les extensions disponibles de commandes et utilisez hello **–-json** option toodisplay toutes les informations disponibles sur une ou plusieurs extensions. Si vous n’utilisez pas un nom d’extension, la commande hello retourne une description JSON de toutes les extensions disponibles.

Par exemple, hello, exemple de code suivant montre comment toolist hello concernant hello **IaaSDiagnostics** à l’aide de l’extension hello CLI d’Azure **liste des extensions de machine virtuelle azure** hello de commande et utilise **–-json** option tooreturn obtenir des informations complètes.

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



### <a name="service-management-rest-apis"></a>API REST de gestion de service
Vous pouvez utiliser hello API REST des informations de tooobtain sur les extensions disponibles suivantes :

* Pour les instances de rôles web ou les rôles de travail, vous pouvez utiliser hello [liste des Extensions disponibles](https://msdn.microsoft.com/library/dn169559.aspx) opération. versions de hello toolist des extensions disponibles, vous pouvez utiliser [liste des Versions d’Extension](https://msdn.microsoft.com/library/dn495437.aspx).
* Pour les instances d’ordinateurs virtuels, vous pouvez utiliser hello [liste des Extensions de ressource](https://msdn.microsoft.com/library/dn495441.aspx) opération. versions de hello toolist des extensions disponibles, vous pouvez utiliser [liste des Versions d’Extension de ressource](https://msdn.microsoft.com/library/dn495440.aspx).

## <a name="add-update-or-disable-extensions"></a>Ajout, mise à jour ou désactivation des extensions
Extensions peuvent être ajoutées lors de la création d’une instance ou qu’ils peuvent être ajoutés tooa instance en cours d’exécution. Des extensions peuvent être mises à jour, désactivées ou supprimées. Vous pouvez effectuer ces actions à l’aide des applets de commande PowerShell de Azure ou à l’aide d’opérations d’API REST Service Management hello. Les paramètres sont tooinstall requis et configurer certaines extensions. Des paramètres publics et privés sont pris en charge pour les extensions.

### <a name="azure-powershell"></a>Azure PowerShell
À l’aide des applets de commande PowerShell de Azure est hello plus simple façon tooadd et mise à jour extensions. Lorsque vous utilisez les applets de commande hello extension, la plupart des configuration hello d’extension de hello est effectuée pour vous. Dans certains cas, vous devrez peut-être tooprogrammatically Ajout d’une extension. Lorsque vous devez toodo cela, vous devez fournir la configuration hello d’extension de hello.

Vous pouvez utiliser hello suivant d’applets de commande tooknow si une extension nécessite une configuration de paramètres publics et privés :

* Pour les instances de rôles web ou les rôles de travail, vous pouvez utiliser hello **Get-AzureServiceAvailableExtension** applet de commande.
* Pour les instances d’ordinateurs virtuels, vous pouvez utiliser hello **Get-AzureVMAvailableExtension** applet de commande.

### <a name="service-management-rest-apis"></a>API REST de gestion de service
Lorsque vous récupérez une liste d’extensions disponibles à l’aide des API REST de hello, vous recevez des informations sur l’extension de hello toobe configuré. informations Hello retourné peuvent afficher des informations de paramètre représentées par un schéma public et un schéma privé. Valeurs de paramètres publics sont retournés dans les requêtes sur les instances de hello. Les valeurs de paramètres privés ne sont pas renvoyées.

Vous pouvez utiliser hello suivant l’API REST tooknow si une extension nécessite une configuration de paramètres publics et privés :

* Pour les instances de rôles web ou des rôles de travail, hello **PublicConfigurationSchema** et **PrivateConfigurationSchema** éléments contiennent des informations de hello en réponse hello hello [liste Extensions disponibles](https://msdn.microsoft.com/library/dn169559.aspx) opération.
* Pour les instances de Machines virtuelles, hello **PublicConfigurationSchema** et **PrivateConfigurationSchema** éléments contiennent des informations de hello en réponse hello hello [liste Extensions de ressource](https://msdn.microsoft.com/library/dn495441.aspx) opération.

> [!NOTE]
> Des extensions peuvent également utiliser des configurations définies avec JSON. Lorsque ces types d’extensions sont utilisés, vous devez uniquement hello **SampleConfig** élément est utilisé.
> 
> 

