


<span data-ttu-id="3fee9-101">Un groupe à haute disponibilité maintient la disponibilité de vos machines virtuelles pendant une interruption (par exemple, en cas de maintenance).</span><span class="sxs-lookup"><span data-stu-id="3fee9-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="3fee9-102">Placer deux ou plusieurs machines virtuelles configurées de manière similaire dans un ensemble de disponibilité crée hello redondance nécessitée toomaintain disponibilité hello services ou applications qui s’exécute de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3fee9-102">Placing two or more similarly configured virtual machines in an availability set creates hello redundancy needed toomaintain availability of hello applications or services that your virtual machine runs.</span></span> <span data-ttu-id="3fee9-103">Pour plus d’informations sur cette procédure, consultez [gérer la disponibilité hello des machines virtuelles][Manage hello availability of virtual machines].</span><span class="sxs-lookup"><span data-stu-id="3fee9-103">For details about how this works, see [Manage hello availability of virtual machines][Manage hello availability of virtual machines].</span></span>

<span data-ttu-id="3fee9-104">Il s’agit d’une meilleure toouse de pratique à haute disponibilité et l’équilibrage de charge de toohelp de points de terminaison vous assurer que votre application est toujours disponible et en cours d’exécution efficace.</span><span class="sxs-lookup"><span data-stu-id="3fee9-104">It's a best practice toouse both availability sets and load-balancing endpoints toohelp ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="3fee9-105">Pour plus d’informations sur les points de terminaison à équilibrage de la charge, consultez la page [Équilibrage de charge pour les services d’infrastructure Azure][Load balancing for Azure infrastructure services].</span><span class="sxs-lookup"><span data-stu-id="3fee9-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="3fee9-106">Vous pouvez ajouter des machines virtuelles classiques dans un groupe à haute disponibilité en utilisant l’une des deux options suivantes :</span><span class="sxs-lookup"><span data-stu-id="3fee9-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="3fee9-107">[Option 1 : Créer un ordinateur virtuel et un ensemble de disponibilité à hello même temps][Option 1: Create a virtual machine and an availability set at hello same time].</span><span class="sxs-lookup"><span data-stu-id="3fee9-107">[Option 1: Create a virtual machine and an availability set at hello same time][Option 1: Create a virtual machine and an availability set at hello same time].</span></span> <span data-ttu-id="3fee9-108">Ensuite, ajoutez de nouvelles machines virtuelles toohello définie lorsque vous créez ces ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="3fee9-108">Then, add new virtual machines toohello set when you create those virtual machines.</span></span>
* <span data-ttu-id="3fee9-109">[Option 2 : Ajout d’un ensemble de disponibilité tooan machine virtuelle existante][Option 2: Add an existing virtual machine tooan availability set].</span><span class="sxs-lookup"><span data-stu-id="3fee9-109">[Option 2: Add an existing virtual machine tooan availability set][Option 2: Add an existing virtual machine tooan availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="3fee9-110">Dans le modèle classique de hello, les machines virtuelles que vous voulez tooput dans hello même groupe à haute disponibilité doit appartenir toohello même service cloud.</span><span class="sxs-lookup"><span data-stu-id="3fee9-110">In hello classic model, virtual machines that you want tooput in hello same availability set must belong toohello same cloud service.</span></span>
> 
> 

## <span data-ttu-id="3fee9-111"><a id="createset"></a>Option 1 : créer un ordinateur virtuel et un ensemble de disponibilité à hello même temps</span><span class="sxs-lookup"><span data-stu-id="3fee9-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="3fee9-112">Vous pouvez utiliser soit hello portail Azure ou Azure PowerShell des commandes toodo cela.</span><span class="sxs-lookup"><span data-stu-id="3fee9-112">You can use either hello Azure portal or Azure PowerShell commands toodo this.</span></span>

<span data-ttu-id="3fee9-113">hello toouse portail Azure :</span><span class="sxs-lookup"><span data-stu-id="3fee9-113">toouse hello Azure portal:</span></span>

1. <span data-ttu-id="3fee9-114">Si vous n’avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3fee9-114">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3fee9-115">Dans le menu du hub hello, cliquez sur **+ nouveau**, puis cliquez sur **Machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="3fee9-115">On hello hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="3fee9-117">Sélectionnez l’image de machine virtuelle Marketplace hello toouse vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="3fee9-117">Select hello Marketplace virtual machine image you wish toouse.</span></span> <span data-ttu-id="3fee9-118">Vous pouvez choisir toocreate une machine virtuelle Linux ou Windows.</span><span class="sxs-lookup"><span data-stu-id="3fee9-118">You can choose toocreate a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="3fee9-119">Pour hello sélectionné un ordinateur virtuel, vérifiez que ce modèle de déploiement hello est défini trop**classique** puis cliquez sur **créer**</span><span class="sxs-lookup"><span data-stu-id="3fee9-119">For hello selected virtual machine, verify that hello deployment model is set too**Classic** and then click **Create**</span></span>
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="3fee9-121">Entrez le nom de la machine virtuelle, le nom d’utilisateur et le mot de passe (pour les machines Windows) ou la clé publique SSH (pour les machines Linux).</span><span class="sxs-lookup"><span data-stu-id="3fee9-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="3fee9-122">Taille de machine virtuelle hello et cliquez sur **sélectionnez** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="3fee9-122">Choose hello VM size and then click **Select** toocontinue.</span></span>
7. <span data-ttu-id="3fee9-123">Choisissez **Configuration facultative > haute disponibilité**, puis vous le souhaitez tooadd hello ordinateur virtuel à haute disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="3fee9-123">Choose **Optional Configuration > Availability set**, and select hello availability set you wish tooadd hello virtual machine to.</span></span>
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="3fee9-125">Passez en revue vos paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="3fee9-125">Review your configuration settings.</span></span> <span data-ttu-id="3fee9-126">Une fois ces opérations effectuées, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="3fee9-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="3fee9-127">Alors que Azure crée votre machine virtuelle, vous pouvez suivre la progression de hello sous **virtuels** dans le menu du hub hello.</span><span class="sxs-lookup"><span data-stu-id="3fee9-127">While Azure creates your virtual machine, you can track hello progress under **Virtual Machines** in hello hub menu.</span></span>

<span data-ttu-id="3fee9-128">toouse Azure PowerShell commandes toocreate une machine virtuelle Azure et ajoutez-le tooa à haute disponibilité de nouvelle ou existante, consultez [toocreate d’utiliser Azure PowerShell et préconfigurer des machines virtuelles basées sur Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3fee9-128">toouse Azure PowerShell commands toocreate an Azure virtual machine and add it tooa new or existing availability set, see [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="3fee9-129"><a id="addmachine"></a>Option 2 : ajouter un ensemble de disponibilité tooan ordinateur virtuel existant</span><span class="sxs-lookup"><span data-stu-id="3fee9-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine tooan availability set</span></span>
<span data-ttu-id="3fee9-130">Bonjour portail Azure, vous pouvez ajouter des existant tooan de machines virtuelles classiques existantes du groupe à haute disponibilité ou créez-en un pour les.</span><span class="sxs-lookup"><span data-stu-id="3fee9-130">In hello Azure portal, you can add existing classic virtual machines tooan existing availability set or create a new one for them.</span></span> <span data-ttu-id="3fee9-131">(N’oubliez pas que les machines virtuelles hello hello même groupe à haute disponibilité doit appartenir toohello même service cloud.) étapes de Hello sont presque hello même.</span><span class="sxs-lookup"><span data-stu-id="3fee9-131">(Keep in mind that hello virtual machines in hello same availability set must belong toohello same cloud service.) hello steps are almost hello same.</span></span> <span data-ttu-id="3fee9-132">Avec Azure PowerShell, vous pouvez ajouter hello machine virtuelle tooan à haute disponibilité existant.</span><span class="sxs-lookup"><span data-stu-id="3fee9-132">With Azure PowerShell, you can add hello virtual machine tooan existing availability set.</span></span>

1. <span data-ttu-id="3fee9-133">Si vous ne le n'avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3fee9-133">If you have not already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3fee9-134">Dans le menu du Hub hello, cliquez sur **Machines virtuelles (classiques)**.</span><span class="sxs-lookup"><span data-stu-id="3fee9-134">On hello Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="3fee9-136">À partir de la liste de hello des machines virtuelles, sélectionnez le nom de hello de machine virtuelle de hello que vous souhaitez tooadd toohello ensemble.</span><span class="sxs-lookup"><span data-stu-id="3fee9-136">From hello list of virtual machines, select hello name of hello virtual machine that you want tooadd toohello set.</span></span>
4. <span data-ttu-id="3fee9-137">Choisissez **à haute disponibilité** de la machine virtuelle de hello **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="3fee9-137">Choose **Availability set** from hello virtual machine **Settings**.</span></span>
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="3fee9-139">Sélectionnez vous souhaitez tooadd hello ordinateur virtuel à haute disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="3fee9-139">Select hello availability set you wish tooadd hello virtual machine to.</span></span> <span data-ttu-id="3fee9-140">machine virtuelle de Hello doit appartenir toohello même service cloud en tant que groupe à haute disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="3fee9-140">hello virtual machine must belong toohello same cloud service as hello availability set.</span></span>
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="3fee9-142">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3fee9-142">Click **Save**.</span></span>

<span data-ttu-id="3fee9-143">commandes Azure PowerShell de toouse, ouvrir une session Azure PowerShell de niveau administrateur et exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="3fee9-143">toouse Azure PowerShell commands, open an administrator-level Azure PowerShell session and run hello following command.</span></span> <span data-ttu-id="3fee9-144">Pour les espaces réservés de hello (tel que &lt;VmCloudServiceName&gt;), remplacer tous les éléments entre guillemets hello, y compris hello < et >, avec hello corriger les noms.</span><span class="sxs-lookup"><span data-stu-id="3fee9-144">For hello placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="3fee9-145">machine virtuelle de Hello peut-être toofinish toobe redémarré ajoutant toohello à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="3fee9-145">hello virtual machine might have toobe restarted toofinish adding it toohello availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

