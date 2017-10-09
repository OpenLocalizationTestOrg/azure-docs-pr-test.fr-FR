


## <a name="attach-an-empty-disk"></a><span data-ttu-id="7e73c-101">Attacher un disque vide</span><span class="sxs-lookup"><span data-stu-id="7e73c-101">Attach an empty disk</span></span>
<span data-ttu-id="7e73c-102">Attachement d’un disque vide est un tooadd facilement des données sur le disque, car Azure crée un fichier .vhd de hello pour vous et la stocke dans le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="7e73c-102">Attaching an empty disk is a simple way tooadd a data disk, because Azure creates hello .vhd file for you and stores it in hello storage account.</span></span>

1. <span data-ttu-id="7e73c-103">Cliquez sur **Machines virtuelles (classiques)**, et puis sélectionnez hello machine virtuelle appropriée.</span><span class="sxs-lookup"><span data-stu-id="7e73c-103">Click **Virtual Machines (classic)**, and then select hello appropriate VM.</span></span>

2. <span data-ttu-id="7e73c-104">Dans le menu Paramètres de hello, cliquez sur **disques**.</span><span class="sxs-lookup"><span data-stu-id="7e73c-104">In hello Settings menu, click **Disks**.</span></span>

   ![Attacher un nouveau disque vide](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="7e73c-106">Dans la barre de commandes hello, cliquez sur **attacher nouvelle**.</span><span class="sxs-lookup"><span data-stu-id="7e73c-106">On hello command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="7e73c-107">Hello **attacher un nouveau disque** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7e73c-107">hello **Attach new disk** dialog box appears.</span></span>

    ![Attacher un nouveau disque](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="7e73c-109">Renseignez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="7e73c-109">Fill in hello following information:</span></span>
    - <span data-ttu-id="7e73c-110">Dans **nom de fichier**, acceptez le nom par défaut de hello ou tapez-en un autre fichier .vhd de hello.</span><span class="sxs-lookup"><span data-stu-id="7e73c-110">In **File Name**, accept hello default name or type another one for hello .vhd file.</span></span> <span data-ttu-id="7e73c-111">disque de données Hello utilise un nom généré automatiquement, même si vous tapez un autre nom pour le fichier .vhd de hello.</span><span class="sxs-lookup"><span data-stu-id="7e73c-111">hello data disk uses an automatically generated name, even if you type another name for hello .vhd file.</span></span>
    - <span data-ttu-id="7e73c-112">Sélectionnez hello **Type** hello disque de données.</span><span class="sxs-lookup"><span data-stu-id="7e73c-112">Select hello **Type** of hello data disk.</span></span> <span data-ttu-id="7e73c-113">Toutes les machines virtuelles prennent en charge des disques standard.</span><span class="sxs-lookup"><span data-stu-id="7e73c-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="7e73c-114">La plupart prennent également en charge les disques Premium.</span><span class="sxs-lookup"><span data-stu-id="7e73c-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="7e73c-115">Sélectionnez hello **taille (Go)** hello disque de données.</span><span class="sxs-lookup"><span data-stu-id="7e73c-115">Select hello **Size (GB)** of hello data disk.</span></span>
    - <span data-ttu-id="7e73c-116">Dans le champ **Mise en cache de l’hôte**, sélectionnez Aucune ou En lecture seule.</span><span class="sxs-lookup"><span data-stu-id="7e73c-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="7e73c-117">Cliquez sur OK toofinish.</span><span class="sxs-lookup"><span data-stu-id="7e73c-117">Click OK toofinish.</span></span>

4. <span data-ttu-id="7e73c-118">Une fois le disque de données hello est créé et attaché, il est répertorié dans la section disques hello hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e73c-118">After hello data disk is created and attached, it's listed in hello disks section of hello VM.</span></span>

   ![Nouveau disque de données vide correctement attaché](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="7e73c-120">Après avoir ajouté un disque de données, vous devez toolog sur toohello VM et initialisez le disque de hello afin qu’il peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="7e73c-120">After you add a data disk, you need toolog on toohello VM and initialize hello disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="7e73c-121">Association d'un disque existant</span><span class="sxs-lookup"><span data-stu-id="7e73c-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="7e73c-122">Pour attacher un disque existant, vous devez disposer d’un fichier .vhd dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="7e73c-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="7e73c-123">Hello d’utilisation [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) compte de stockage toohello de fichier .vhd d’applet de commande tooupload hello.</span><span class="sxs-lookup"><span data-stu-id="7e73c-123">Use hello [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello .vhd file toohello storage account.</span></span> <span data-ttu-id="7e73c-124">Une fois que vous avez créé et téléchargé le fichier .vhd de hello, vous pouvez les attacher à tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7e73c-124">After you've created and uploaded hello .vhd file, you can attach it tooa VM.</span></span>

1. <span data-ttu-id="7e73c-125">Cliquez sur **Machines virtuelles (classiques)**, et puis sélectionnez hello machine virtuelle appropriée.</span><span class="sxs-lookup"><span data-stu-id="7e73c-125">Click **Virtual Machines (classic)**, and then select hello appropriate virtual machine.</span></span>

2. <span data-ttu-id="7e73c-126">Dans le menu Paramètres de hello, cliquez sur **disques**.</span><span class="sxs-lookup"><span data-stu-id="7e73c-126">In hello Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="7e73c-127">Dans la barre de commandes hello, cliquez sur **attacher existant**.</span><span class="sxs-lookup"><span data-stu-id="7e73c-127">On hello command bar, click **Attach existing**.</span></span>

    ![Attacher un disque de données](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="7e73c-129">Cliquez sur **Emplacement**.</span><span class="sxs-lookup"><span data-stu-id="7e73c-129">Click **Location**.</span></span> <span data-ttu-id="7e73c-130">affichent les comptes de stockage disponibles Hello.</span><span class="sxs-lookup"><span data-stu-id="7e73c-130">hello available storage accounts display.</span></span> <span data-ttu-id="7e73c-131">Sélectionnez ensuite un compte de stockage approprié dans la liste.</span><span class="sxs-lookup"><span data-stu-id="7e73c-131">Next, select an appropriate storage account from those listed.</span></span>

    ![Fournir un compte de stockage de disques](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="7e73c-133">Un **compte de stockage** dispose d’un ou plusieurs conteneurs qui contiennent des lecteurs de disque (VHD).</span><span class="sxs-lookup"><span data-stu-id="7e73c-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="7e73c-134">Sélectionnez le conteneur approprié de hello depuis la rédaction.</span><span class="sxs-lookup"><span data-stu-id="7e73c-134">Select hello appropriate container from those listed.</span></span>

    ![Fournir le conteneur de machines virtuelles windows](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="7e73c-136">Hello **disques durs virtuels** panneau répertorie les lecteurs de disque hello contenues dans le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="7e73c-136">hello **vhds** panel lists hello disk drives held in hello container.</span></span> <span data-ttu-id="7e73c-137">Cliquez sur un des disques de hello, puis cliquez sur Sélectionner.</span><span class="sxs-lookup"><span data-stu-id="7e73c-137">Click one of hello disks, and then click Select.</span></span>

    ![Fournir une image de disque pour les machines virtuelles windows](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="7e73c-139">Hello **attachement du disque existant** panneau affiche à nouveau, à l’emplacement de hello contenant le compte de stockage hello conteneur et la machine virtuelle de disque dur sélectionné (vhd) tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="7e73c-139">hello **Attach existing disk** panel displays again, with hello location containing hello storage account, container, and selected hard disk (vhd) tooadd toohello virtual machine.</span></span>

  <span data-ttu-id="7e73c-140">Définissez **héberger la mise en cache** toonone ou en lecture seule, puis cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="7e73c-140">Set **Host caching** toonone or Read only, then click OK.</span></span>

    ![Disque de données correctement attaché](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
