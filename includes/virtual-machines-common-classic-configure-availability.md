


<span data-ttu-id="c2494-101">Un groupe à haute disponibilité maintient la disponibilité de vos machines virtuelles pendant une interruption (par exemple, en cas de maintenance).</span><span class="sxs-lookup"><span data-stu-id="c2494-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="c2494-102">Le placement de deux machines virtuelles ou plus dans un groupe à haute disponibilité crée les conditions de redondance indispensables au maintien de la disponibilité des applications ou des services exécutés par votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c2494-102">Placing two or more similarly configured virtual machines in an availability set creates the redundancy needed to maintain availability of the applications or services that your virtual machine runs.</span></span> <span data-ttu-id="c2494-103">Pour plus d’informations sur cette procédure, voir la rubrique [Gestion de la disponibilité des machines virtuelles][Manage the availability of virtual machines].</span><span class="sxs-lookup"><span data-stu-id="c2494-103">For details about how this works, see [Manage the availability of virtual machines][Manage the availability of virtual machines].</span></span>

<span data-ttu-id="c2494-104">Il est recommandé d’utiliser des groupes à haute disponibilité et des points de terminaison à équilibrage de charge pour garantir que votre application soit toujours disponible et qu’elle s’exécute correctement.</span><span class="sxs-lookup"><span data-stu-id="c2494-104">It's a best practice to use both availability sets and load-balancing endpoints to help ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="c2494-105">Pour plus d’informations sur les points de terminaison à équilibrage de la charge, consultez la page [Équilibrage de charge pour les services d’infrastructure Azure][Load balancing for Azure infrastructure services].</span><span class="sxs-lookup"><span data-stu-id="c2494-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="c2494-106">Vous pouvez ajouter des machines virtuelles classiques dans un groupe à haute disponibilité en utilisant l’une des deux options suivantes :</span><span class="sxs-lookup"><span data-stu-id="c2494-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="c2494-107">[Option 1 : Créer simultanément une machine virtuelle et un groupe à haute disponibilité][Option 1: Create a virtual machine and an availability set at the same time].</span><span class="sxs-lookup"><span data-stu-id="c2494-107">[Option 1: Create a virtual machine and an availability set at the same time][Option 1: Create a virtual machine and an availability set at the same time].</span></span> <span data-ttu-id="c2494-108">Ensuite, ajouter de nouvelles machines virtuelles à l’ensemble lorsque vous créez ces ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="c2494-108">Then, add new virtual machines to the set when you create those virtual machines.</span></span>
* <span data-ttu-id="c2494-109">[Option 2 : Ajouter une machine virtuelle existante à un groupe à haute disponibilité][Option 2: Add an existing virtual machine to an availability set].</span><span class="sxs-lookup"><span data-stu-id="c2494-109">[Option 2: Add an existing virtual machine to an availability set][Option 2: Add an existing virtual machine to an availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="c2494-110">Dans le modèle classique, les machines virtuelles que vous voulez placer dans le même groupe à haute disponibilité doivent appartenir au même service cloud.</span><span class="sxs-lookup"><span data-stu-id="c2494-110">In the classic model, virtual machines that you want to put in the same availability set must belong to the same cloud service.</span></span>
> 
> 

## <span data-ttu-id="c2494-111"><a id="createset"> </a>Option 1 : Créer simultanément une machine virtuelle et un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="c2494-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at the same time</span></span>
<span data-ttu-id="c2494-112">Pour cela, vous pouvez utiliser le portail Azure ou des commandes Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2494-112">You can use either the Azure portal or Azure PowerShell commands to do this.</span></span>

<span data-ttu-id="c2494-113">Pour utiliser le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="c2494-113">To use the Azure portal:</span></span>

1. <span data-ttu-id="c2494-114">Si ce n’est pas déjà fait, connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c2494-114">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c2494-115">Dans le menu hub, cliquez sur **+ Nouveau**, puis sur **Machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="c2494-115">On the hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="c2494-117">Sélectionner l’image de machine virtuelle Marketplace que vous voulez utiliser.</span><span class="sxs-lookup"><span data-stu-id="c2494-117">Select the Marketplace virtual machine image you wish to use.</span></span> <span data-ttu-id="c2494-118">Vous pouvez choisir de créer une machine virtuelle Linux ou Windows.</span><span class="sxs-lookup"><span data-stu-id="c2494-118">You can choose to create a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="c2494-119">Pour la machine virtuelle sélectionnée, vérifiez que le modèle de déploiement est défini sur **Classique**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="c2494-119">For the selected virtual machine, verify that the deployment model is set to **Classic** and then click **Create**</span></span>
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="c2494-121">Entrez le nom de la machine virtuelle, le nom d’utilisateur et le mot de passe (pour les machines Windows) ou la clé publique SSH (pour les machines Linux).</span><span class="sxs-lookup"><span data-stu-id="c2494-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="c2494-122">Choisissez une taille de machine virtuelle, puis cliquez sur **Sélectionner** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="c2494-122">Choose the VM size and then click **Select** to continue.</span></span>
7. <span data-ttu-id="c2494-123">Choisissez **Configuration facultative > Groupe à haute disponibilité**, puis sélectionnez le groupe à haute disponibilité auquel vous voulez ajouter la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c2494-123">Choose **Optional Configuration > Availability set**, and select the availability set you wish to add the virtual machine to.</span></span>
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="c2494-125">Passez en revue vos paramètres de configuration.</span><span class="sxs-lookup"><span data-stu-id="c2494-125">Review your configuration settings.</span></span> <span data-ttu-id="c2494-126">Une fois ces opérations effectuées, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="c2494-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="c2494-127">Pendant qu’Azure crée votre machine virtuelle, vous pouvez suivre la progression de cette opération dans le menu Hub, sous **Machines virtuelles** .</span><span class="sxs-lookup"><span data-stu-id="c2494-127">While Azure creates your virtual machine, you can track the progress under **Virtual Machines** in the hub menu.</span></span>

<span data-ttu-id="c2494-128">Pour plus d’informations sur l’utilisation des commandes Azure PowerShell pour créer une machine virtuelle Azure et l’ajouter à un groupe à haute disponibilité nouveau ou existant, consultez l’article [Utiliser Azure PowerShell pour créer et préconfigurer des machines virtuelles Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c2494-128">To use Azure PowerShell commands to create an Azure virtual machine and add it to a new or existing availability set, see [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="c2494-129"><a id="addmachine"> </a>Option 2 : Ajouter une machine virtuelle existante à un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="c2494-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine to an availability set</span></span>
<span data-ttu-id="c2494-130">Dans le portail Azure, vous pouvez ajouter des machines virtuelles classiques existantes à un groupe à haute disponibilité existant, ou en créer un pour ces machines.</span><span class="sxs-lookup"><span data-stu-id="c2494-130">In the Azure portal, you can add existing classic virtual machines to an existing availability set or create a new one for them.</span></span> <span data-ttu-id="c2494-131">(N’oubliez pas que les machines virtuelles dans un même groupe à haute disponibilité doivent appartenir au même service cloud). Les opérations à effectuer sont pratiquement identiques.</span><span class="sxs-lookup"><span data-stu-id="c2494-131">(Keep in mind that the virtual machines in the same availability set must belong to the same cloud service.) The steps are almost the same.</span></span> <span data-ttu-id="c2494-132">Avec Azure PowerShell, vous pouvez ajouter la machine virtuelle à un groupe à haute disponibilité existant.</span><span class="sxs-lookup"><span data-stu-id="c2494-132">With Azure PowerShell, you can add the virtual machine to an existing availability set.</span></span>

1. <span data-ttu-id="c2494-133">Si ce n’est pas déjà fait, connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c2494-133">If you have not already done so, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c2494-134">Dans le menu Hub, cliquez sur **Machines virtuelles (classiques)**.</span><span class="sxs-lookup"><span data-stu-id="c2494-134">On the Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="c2494-136">Dans la liste des machines virtuelles, sélectionnez le nom de la machine virtuelle que vous voulez ajouter au groupe.</span><span class="sxs-lookup"><span data-stu-id="c2494-136">From the list of virtual machines, select the name of the virtual machine that you want to add to the set.</span></span>
4. <span data-ttu-id="c2494-137">Choisissez **Groupe à haute disponibilité** dans les **Paramètres** de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c2494-137">Choose **Availability set** from the virtual machine **Settings**.</span></span>
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="c2494-139">Sélectionner le groupe à haute disponibilité auquel vous voulez ajouter la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c2494-139">Select the availability set you wish to add the virtual machine to.</span></span> <span data-ttu-id="c2494-140">La machine virtuelle doit appartenir au même service cloud que le groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="c2494-140">The virtual machine must belong to the same cloud service as the availability set.</span></span>
   
    ![Texte de remplacement d’image](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="c2494-142">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="c2494-142">Click **Save**.</span></span>

<span data-ttu-id="c2494-143">Pour utiliser les commandes Azure PowerShell, ouvrez une session Azure PowerShell de niveau administrateur et exécutez la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="c2494-143">To use Azure PowerShell commands, open an administrator-level Azure PowerShell session and run the following command.</span></span> <span data-ttu-id="c2494-144">Pour les espaces réservés (tels que &lt;VmCloudServiceName&gt;), remplacez tout ce qui se trouve entre guillemets, y compris les caractères < et >, par les noms adéquats.</span><span class="sxs-lookup"><span data-stu-id="c2494-144">For the placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="c2494-145">Il se peut que la machine virtuelle doive être redémarrée pour terminer son ajout au groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="c2494-145">The virtual machine might have to be restarted to finish adding it to the availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at the same time]: #createset
[Option 2: Add an existing virtual machine to an availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage the availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

