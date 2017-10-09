

Les extensions de machine virtuelle peuvent vous aider à :

* modifier les fonctionnalités de sécurité et d'identité telles que la réinitialisation des valeurs de compte et l'utilisation de logiciels anti-programmes malveillants ;
* démarrer, arrêter ou configurer la surveillance et les diagnostics ;
* réinitialiser ou installer des fonctionnalités de connectivité, telles que RDP et SSH ;
* diagnostiquer, surveiller et gérer vos machines virtuelles.

Il existe de nombreuses autres fonctionnalités. De nouvelles fonctionnalités d’extension de machine virtuelle sont publiées régulièrement. Cet article décrit les Agents hello Azure VM pour Windows et Linux, et comment ils prennent en charge la fonctionnalité d’Extension de machine virtuelle. Pour obtenir une liste des extensions de machine virtuelle par catégorie de fonctionnalité, consultez l’article [Fonctionnalités et extensions de machine virtuelle Azure](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="azure-vm-agents-for-windows-and-linux"></a>Agents de machine virtuelle Azure pour Windows et Linux
Bonjour Azure Virtual Machines Agent (Agent de machine virtuelle) est un processus léger sécurisé qui installe, configure et supprime les extensions de machine virtuelle sur les instances de Machines virtuelles Azure. Hello Agent de machine virtuelle joue le rôle service de contrôle local sécurisé hello pour votre machine virtuelle Azure. extensions Hello hello agent charge fournissent tooincrease de fonctionnalités spécifiques votre productivité à l’aide d’instance de hello.

Il existe deux agents de machine virtuelle Azure, un pour les machines virtuelles Windows et l'autre pour les machines virtuelles Linux.

Si vous souhaitez un toouse d’instance de machine virtuelle à un ou plusieurs extensions de machine virtuelle, instance de hello doit avoir un Agent de machine virtuelle installé. Image de machine virtuelle créée à l’aide de hello portail Azure et une image à partir de hello **Marketplace** installe automatiquement un Agent de machine virtuelle dans le processus de création de hello. Si une instance de l’ordinateur virtuel ne dispose pas d’un Agent de machine virtuelle, vous pouvez installer hello Agent de machine virtuelle une fois que l’instance de machine virtuelle hello est créé. Ou bien, vous pouvez installer l’agent de hello dans une image de machine virtuelle personnalisée que vous chargez.

> [!IMPORTANT]
> Ces agents de machine virtuelle sont des services légers permettant la gestion sécurisée des instances de machine virtuelle. Il peut y avoir des cas dans lesquels vous ne souhaitez pas hello Agent de machine virtuelle. Dans ce cas, être sûr de machines virtuelles toocreate qui n’ont pas hello Agent de machine virtuelle installé à l’aide de PowerShell ou hello CLI d’Azure. Bien que hello Agent de machine virtuelle puisse être supprimé, comportement hello d’Extensions de machine virtuelle sur une instance de hello n’est pas défini. Par conséquent, la suppression d’un agent de machine virtuelle installé n’est pas prise en charge.
>

Hello Agent de machine virtuelle est activée dans hello suivant situations :

* Lorsque vous créez une instance d’une machine virtuelle à l’aide de hello portail Azure et en sélectionnant une image à partir de hello **Marketplace**,
* Lorsque vous créez une instance d’une machine virtuelle à l’aide de hello [New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx) ou hello [New-AzureQuickVM](https://msdn.microsoft.com/library/azure/dn495183.aspx) applet de commande. Vous pouvez créer un ordinateur virtuel sans Agent de machine virtuelle en ajoutant hello **– DisableGuestAgent** paramètre toohello [Add-AzureProvisioningConfig](https://msdn.microsoft.com/library/azure/dn495299.aspx) applet de commande

* Lorsque vous manuellement télécharger et installer hello Agent de machine virtuelle sur une instance existante de la machine virtuelle et définir hello **ProvisionGuestAgent** valeur trop**true**. Vous pouvez utiliser cette technique pour les agents Windows et Linux, à l’aide d’une commande PowerShell ou d’un appel REST. (Si vous ne définissez pas hello **ProvisionGuestAgent** valeur après l’installation manuelle hello Agent de machine virtuelle, ajout de hello de hello Agent de machine virtuelle n’est pas correctement détecté.) hello suivant exemple de code montre comment toodo ce à l’aide de PowerShell où hello `$svc` et `$name` arguments ont déjà été déterminées :

      $vm = Get-AzureVM –ServiceName $svc –Name $name
      $vm.VM.ProvisionGuestAgent = $TRUE
      Update-AzureVM –Name $name –VM $vm.VM –ServiceName $svc

* Lorsque vous créez une image de machine virtuelle qui inclut un agent de machine virtuelle installé. Une fois l’image hello avec hello Agent de machine virtuelle existe, vous pouvez télécharger ce tooAzure d’image. Pour une machine virtuelle Windows, téléchargez hello [fichier .msi de l’Agent de machine virtuelle Windows](http://go.microsoft.com/fwlink/?LinkID=394789) et installer hello Agent de machine virtuelle. Pour un VM Linux, installez hello Agent de machine virtuelle à partir du référentiel GitHub de hello situé <https://github.com/Azure/WALinuxAgent>. Pour plus d’informations sur la façon dont tooinstall hello Agent de machine virtuelle sur Linux, consultez hello [Guide de l’utilisateur Agent de machine virtuelle Linux Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

> [!NOTE]
> Dans PaaS, hello Agent de machine virtuelle est appelée **WindowsAzureGuestAgent**et est toujours disponible sur le Web et les machines virtuelles de rôle de travail. (Pour plus d’informations, consultez [Azure Role Architecture](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx).) hello Agent de machine virtuelle pour les machines virtuelles de rôle peut désormais ajouter des extensions toohello cloud service machines virtuelles de hello même façon que pour les Machines virtuelles persistantes. Hello plus grande différence entre les Extensions de machine virtuelle sur des machines virtuelles de rôle et les machines virtuelles persistantes est lors de l’ajout d’extensions de machine virtuelle hello. Avec les machines virtuelles de rôle, les extensions sont ajoutées premier service de cloud toohello, puis toohello déploiements au sein de ce service cloud.
>
> Utilisez le [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) toolist de l’applet de commande toutes les extensions de machine virtuelle de rôle disponibles.
>
>

## <a name="find-add-update-and-remove-vm-extensions"></a>Rechercher, ajouter, mettre à jour et supprimer des extensions de machine virtuelle
Pour plus d’informations sur ces tâches, consultez l’article expliquant comment [ajouter, rechercher, mettre à jour et supprimer des extensions de machines virtuelles Azure](../articles/virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
