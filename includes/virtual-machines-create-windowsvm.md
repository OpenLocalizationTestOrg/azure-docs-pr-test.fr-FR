1. <span data-ttu-id="46409-101">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="46409-101">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="46409-102">À partir de l’angle supérieur gauche, cliquez sur **Nouveau > Compute > Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="46409-102">Starting in the upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span></span>

    ![Accéder aux images de machines virtuelles Azure sur le portail](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. <span data-ttu-id="46409-104">Dans le centre de données Windows Server 2016 Datacenter, sélectionnez le modèle de déploiement Classic.</span><span class="sxs-lookup"><span data-stu-id="46409-104">On the Windows Server 2016 Datacenter, select the Classic deployment model.</span></span> <span data-ttu-id="46409-105">Cliquez sur Créer.</span><span class="sxs-lookup"><span data-stu-id="46409-105">Click Create.</span></span>

    ![Capture d’écran affichant les images de machines virtuelles Azure disponibles dans le portail](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a><span data-ttu-id="46409-107">1. Panneau Informations de base</span><span class="sxs-lookup"><span data-stu-id="46409-107">1. Basics blade</span></span>

<span data-ttu-id="46409-108">Le panneau Informations de base demande les informations d’administration de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="46409-108">The Basics blade requests administrative information for the virtual machine.</span></span>

1. <span data-ttu-id="46409-109">Entrez le **Nom** de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="46409-109">Enter a **Name** for the virtual machine.</span></span> <span data-ttu-id="46409-110">Dans l’exemple, le nom de la machine virtuelle est _HeroVM_.</span><span class="sxs-lookup"><span data-stu-id="46409-110">In the example, _HeroVM_ is the name of the virtual machine.</span></span> <span data-ttu-id="46409-111">Le nom doit comporter 1 à 15 caractères et il ne peut pas contenir de caractères spéciaux.</span><span class="sxs-lookup"><span data-stu-id="46409-111">The name must be 1-15 characters long and it cannot contain special characters.</span></span>

2. <span data-ttu-id="46409-112">Entrez un **Nom d’utilisateur** et un **Mot de passe** fort qui servent à créer un compte local sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="46409-112">Enter a **User name** and a strong **Password** that are used to create a local account on the VM.</span></span> <span data-ttu-id="46409-113">Le compte local est utilisé pour se connecter à la machine virtuelle et la gérer.</span><span class="sxs-lookup"><span data-stu-id="46409-113">The local account is used to sign in to and manage the VM.</span></span> <span data-ttu-id="46409-114">Dans l’exemple, le nom d’utilisateur est _azureuser_.</span><span class="sxs-lookup"><span data-stu-id="46409-114">In the example, _azureuser_ is the user name.</span></span>

 <span data-ttu-id="46409-115">Le mot de passe doit compter 8 à 123 caractères et répondre à trois des quatre conditions suivantes : un caractère minuscule, un caractère majuscule, un chiffre et un caractère spécial.</span><span class="sxs-lookup"><span data-stu-id="46409-115">The password must be 8-123 characters long and meet three out of the four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="46409-116">En savoir plus sur les [conditions requises pour les noms d’utilisateur et les mots de passe](../articles/virtual-machines/windows/faq.md).</span><span class="sxs-lookup"><span data-stu-id="46409-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span></span>

3. <span data-ttu-id="46409-117">**L’Abonnement** est facultatif.</span><span class="sxs-lookup"><span data-stu-id="46409-117">The **Subscription** is optional.</span></span> <span data-ttu-id="46409-118">Le paramètre le plus courant est « Paiement à l’utilisation ».</span><span class="sxs-lookup"><span data-stu-id="46409-118">One common setting is "Pay-As-You-Go".</span></span>

4. <span data-ttu-id="46409-119">Sélectionnez un **groupe de ressources** existant ou tapez le nom d’un nouveau groupe.</span><span class="sxs-lookup"><span data-stu-id="46409-119">Select an existing **Resource group** or type the name for a new one.</span></span> <span data-ttu-id="46409-120">Dans l’exemple, le nom du groupe de ressources est _HeroVMRG_.</span><span class="sxs-lookup"><span data-stu-id="46409-120">In the example, _HeroVMRG_ is the name of the resource group.</span></span>

5. <span data-ttu-id="46409-121">Sélectionnez **l’Emplacement** du centre de données Azure où vous souhaitez exécuter la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="46409-121">Select an Azure datacenter **Location** where you want the VM to run.</span></span> <span data-ttu-id="46409-122">Dans l’exemple, l’emplacement est **États-Unis de l’Est**.</span><span class="sxs-lookup"><span data-stu-id="46409-122">In the example, **East US** is the location.</span></span>

6. <span data-ttu-id="46409-123">Lorsque vous avez terminé, cliquez sur **Suivant** pour passer au panneau suivant.</span><span class="sxs-lookup"><span data-stu-id="46409-123">When you are done, click **Next** to continue to the next blade.</span></span>

    ![Capture d’écran affichant les paramètres dans le panneau Informations de base pour la configuration d’une machine virtuelle Azure](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a><span data-ttu-id="46409-125">2. Panneau Taille</span><span class="sxs-lookup"><span data-stu-id="46409-125">2. Size blade</span></span>

<span data-ttu-id="46409-126">Le panneau Taille identifie les informations de configuration de la machine virtuelle et liste les différentes options, notamment le système d’exploitation, le nombre de processeurs, le type de stockage disque et les coûts d’utilisation mensuels estimés.</span><span class="sxs-lookup"><span data-stu-id="46409-126">The Size blade identifies the configuration details of the VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span></span>  

<span data-ttu-id="46409-127">Choisissez une taille de machine virtuelle, puis cliquez sur **Sélectionner** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="46409-127">Choose a VM size, and then click **Select** to continue.</span></span> <span data-ttu-id="46409-128">Dans l’exemple, la taille de machine virtuelle est _DS1_\__V2 Standard_.</span><span class="sxs-lookup"><span data-stu-id="46409-128">In this example, _DS1_\__V2 Standard_ is the VM size.</span></span>

  ![Capture d’écran du panneau Taille affichant les tailles de machine virtuelle Azure que vous pouvez sélectionner](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a><span data-ttu-id="46409-130">3. Panneau Paramètres</span><span class="sxs-lookup"><span data-stu-id="46409-130">3. Settings blade</span></span>

<span data-ttu-id="46409-131">Le panneau Paramètres demande des options de stockage et de réseau.</span><span class="sxs-lookup"><span data-stu-id="46409-131">The Settings blade requests storage and network options.</span></span> <span data-ttu-id="46409-132">Vous pouvez accepter les paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="46409-132">You can accept the default settings.</span></span> <span data-ttu-id="46409-133">Azure crée les entrées appropriées si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="46409-133">Azure creates appropriate entries where necessary.</span></span>

<span data-ttu-id="46409-134">Si vous avez sélectionné une taille de machine virtuelle qui le prend en charge, vous pouvez essayer le Stockage Premium Azure en sélectionnant Premium (SSD) sous Type de disque.</span><span class="sxs-lookup"><span data-stu-id="46409-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span></span>

<span data-ttu-id="46409-135">Une fois les modifications terminées, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="46409-135">When you're done making changes, click **OK**.</span></span>

## <a name="4-summary-blade"></a><span data-ttu-id="46409-136">4. Panneau Résumé</span><span class="sxs-lookup"><span data-stu-id="46409-136">4. Summary blade</span></span>

<span data-ttu-id="46409-137">Le panneau Résumé liste les paramètres spécifiés dans les panneaux précédents.</span><span class="sxs-lookup"><span data-stu-id="46409-137">The Summary blade lists the settings specified in the previous blades.</span></span> <span data-ttu-id="46409-138">Cliquez sur **OK** lorsque vous êtes prêt à créer l’image.</span><span class="sxs-lookup"><span data-stu-id="46409-138">Click **OK** when you're ready to make the image.</span></span>

 ![Rapport du panneau Résumé donnant les paramètres spécifiés de la machine virtuelle](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

<span data-ttu-id="46409-140">Une fois la machine virtuelle créée, le portail la liste sous **Toutes les ressources**, et affiche une vignette de la machine virtuelle sur le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="46409-140">After the virtual machine is created, the portal lists the new virtual machine under **All resources**, and displays a tile of the virtual machine on the dashboard.</span></span> <span data-ttu-id="46409-141">Le service cloud et le compte de stockage correspondants sont également créés et listés.</span><span class="sxs-lookup"><span data-stu-id="46409-141">The corresponding cloud service and storage account also are created and listed.</span></span> <span data-ttu-id="46409-142">La machine virtuelle et le service cloud sont démarrés automatiquement et leur statut est répertorié comme **En cours d'exécution**.</span><span class="sxs-lookup"><span data-stu-id="46409-142">Both the virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

 ![Configurer l’agent de machine virtuelle et les points de terminaison de la machine virtuelle](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
