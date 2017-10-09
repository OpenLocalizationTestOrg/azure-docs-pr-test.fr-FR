


Un groupe à haute disponibilité maintient la disponibilité de vos machines virtuelles pendant une interruption (par exemple, en cas de maintenance). Placer deux ou plusieurs machines virtuelles configurées de manière similaire dans un ensemble de disponibilité crée hello redondance nécessitée toomaintain disponibilité hello services ou applications qui s’exécute de votre machine virtuelle. Pour plus d’informations sur cette procédure, consultez [gérer la disponibilité hello des machines virtuelles][Manage hello availability of virtual machines].

Il s’agit d’une meilleure toouse de pratique à haute disponibilité et l’équilibrage de charge de toohelp de points de terminaison vous assurer que votre application est toujours disponible et en cours d’exécution efficace. Pour plus d’informations sur les points de terminaison à équilibrage de la charge, consultez la page [Équilibrage de charge pour les services d’infrastructure Azure][Load balancing for Azure infrastructure services].

Vous pouvez ajouter des machines virtuelles classiques dans un groupe à haute disponibilité en utilisant l’une des deux options suivantes :

* [Option 1 : Créer un ordinateur virtuel et un ensemble de disponibilité à hello même temps][Option 1: Create a virtual machine and an availability set at hello same time]. Ensuite, ajoutez de nouvelles machines virtuelles toohello définie lorsque vous créez ces ordinateurs virtuels.
* [Option 2 : Ajout d’un ensemble de disponibilité tooan machine virtuelle existante][Option 2: Add an existing virtual machine tooan availability set].

> [!NOTE]
> Dans le modèle classique de hello, les machines virtuelles que vous voulez tooput dans hello même groupe à haute disponibilité doit appartenir toohello même service cloud.
> 
> 

## <a id="createset"></a>Option 1 : créer un ordinateur virtuel et un ensemble de disponibilité à hello même temps
Vous pouvez utiliser soit hello portail Azure ou Azure PowerShell des commandes toodo cela.

hello toouse portail Azure :

1. Si vous n’avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu du hub hello, cliquez sur **+ nouveau**, puis cliquez sur **Machine virtuelle**.
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. Sélectionnez l’image de machine virtuelle Marketplace hello toouse vous le souhaitez. Vous pouvez choisir toocreate une machine virtuelle Linux ou Windows.
4. Pour hello sélectionné un ordinateur virtuel, vérifiez que ce modèle de déploiement hello est défini trop**classique** puis cliquez sur **créer**
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. Entrez le nom de la machine virtuelle, le nom d’utilisateur et le mot de passe (pour les machines Windows) ou la clé publique SSH (pour les machines Linux). 
6. Taille de machine virtuelle hello et cliquez sur **sélectionnez** toocontinue.
7. Choisissez **Configuration facultative > haute disponibilité**, puis vous le souhaitez tooadd hello ordinateur virtuel à haute disponibilité hello.
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. Passez en revue vos paramètres de configuration. Une fois ces opérations effectuées, cliquez sur **Créer**.
9. Alors que Azure crée votre machine virtuelle, vous pouvez suivre la progression de hello sous **virtuels** dans le menu du hub hello.

toouse Azure PowerShell commandes toocreate une machine virtuelle Azure et ajoutez-le tooa à haute disponibilité de nouvelle ou existante, consultez [toocreate d’utiliser Azure PowerShell et préconfigurer des machines virtuelles basées sur Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a id="addmachine"></a>Option 2 : ajouter un ensemble de disponibilité tooan ordinateur virtuel existant
Bonjour portail Azure, vous pouvez ajouter des existant tooan de machines virtuelles classiques existantes du groupe à haute disponibilité ou créez-en un pour les. (N’oubliez pas que les machines virtuelles hello hello même groupe à haute disponibilité doit appartenir toohello même service cloud.) étapes de Hello sont presque hello même. Avec Azure PowerShell, vous pouvez ajouter hello machine virtuelle tooan à haute disponibilité existant.

1. Si vous ne le n'avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu du Hub hello, cliquez sur **Machines virtuelles (classiques)**.
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. À partir de la liste de hello des machines virtuelles, sélectionnez le nom de hello de machine virtuelle de hello que vous souhaitez tooadd toohello ensemble.
4. Choisissez **à haute disponibilité** de la machine virtuelle de hello **paramètres**.
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. Sélectionnez vous souhaitez tooadd hello ordinateur virtuel à haute disponibilité hello. machine virtuelle de Hello doit appartenir toohello même service cloud en tant que groupe à haute disponibilité hello.
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. Cliquez sur **Enregistrer**.

commandes Azure PowerShell de toouse, ouvrir une session Azure PowerShell de niveau administrateur et exécutez hello commande suivante. Pour les espaces réservés de hello (tel que &lt;VmCloudServiceName&gt;), remplacer tous les éléments entre guillemets hello, y compris hello < et >, avec hello corriger les noms.

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> machine virtuelle de Hello peut-être toofinish toobe redémarré ajoutant toohello à haute disponibilité.
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

