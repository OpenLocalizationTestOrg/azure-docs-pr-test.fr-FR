


## <a name="attach-an-empty-disk"></a><span data-ttu-id="33eb6-101">Attacher un disque vide</span><span class="sxs-lookup"><span data-stu-id="33eb6-101">Attach an empty disk</span></span>
<span data-ttu-id="33eb6-102">Pour ajouter un disque de données, le plus simple consiste à attacher un disque vide, car Azure crée le fichier de disque dur virtuel (.vhd) pour vous et le stocke dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="33eb6-102">Attaching an empty disk is a simple way to add a data disk, because Azure creates the .vhd file for you and stores it in the storage account.</span></span>

1. <span data-ttu-id="33eb6-103">Cliquez sur **Machines virtuelles (Classic)**, puis sélectionnez la machine virtuelle appropriée.</span><span class="sxs-lookup"><span data-stu-id="33eb6-103">Click **Virtual Machines (classic)**, and then select the appropriate VM.</span></span>

2. <span data-ttu-id="33eb6-104">Dans le panneau Paramètres, cliquez sur **Disques**.</span><span class="sxs-lookup"><span data-stu-id="33eb6-104">In the Settings menu, click **Disks**.</span></span>

   ![Attacher un nouveau disque vide](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="33eb6-106">Dans la barre de commandes, cliquez sur **Attacher un nouveau disque**.</span><span class="sxs-lookup"><span data-stu-id="33eb6-106">On the command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="33eb6-107">La boîte de dialogue **Attacher un nouveau disque** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="33eb6-107">The **Attach new disk** dialog box appears.</span></span>

    ![Attacher un nouveau disque](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="33eb6-109">Renseignez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="33eb6-109">Fill in the following information:</span></span>
    - <span data-ttu-id="33eb6-110">Dans **Nom de fichier**, acceptez le nom par défaut ou tapez-en un autre pour le fichier .vhd.</span><span class="sxs-lookup"><span data-stu-id="33eb6-110">In **File Name**, accept the default name or type another one for the .vhd file.</span></span> <span data-ttu-id="33eb6-111">Le disque de données utilise un nom généré automatiquement, même si vous tapez un autre nom pour le fichier .vhd.</span><span class="sxs-lookup"><span data-stu-id="33eb6-111">The data disk uses an automatically generated name, even if you type another name for the .vhd file.</span></span>
    - <span data-ttu-id="33eb6-112">Sélectionnez le **Type** de disque de données.</span><span class="sxs-lookup"><span data-stu-id="33eb6-112">Select the **Type** of the data disk.</span></span> <span data-ttu-id="33eb6-113">Toutes les machines virtuelles prennent en charge des disques standard.</span><span class="sxs-lookup"><span data-stu-id="33eb6-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="33eb6-114">La plupart prennent également en charge les disques Premium.</span><span class="sxs-lookup"><span data-stu-id="33eb6-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="33eb6-115">Sélectionnez la **Taille (Go)** du disque de données.</span><span class="sxs-lookup"><span data-stu-id="33eb6-115">Select the **Size (GB)** of the data disk.</span></span>
    - <span data-ttu-id="33eb6-116">Dans le champ **Mise en cache de l’hôte**, sélectionnez Aucune ou En lecture seule.</span><span class="sxs-lookup"><span data-stu-id="33eb6-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="33eb6-117">Cliquez sur OK pour terminer.</span><span class="sxs-lookup"><span data-stu-id="33eb6-117">Click OK to finish.</span></span>

4. <span data-ttu-id="33eb6-118">Une fois créé et attaché, le disque de données est répertorié dans la section des disques de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="33eb6-118">After the data disk is created and attached, it's listed in the disks section of the VM.</span></span>

   ![Nouveau disque de données vide correctement attaché](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="33eb6-120">Après avoir ajouté un disque de données, vous devez vous connecter à la machine virtuelle et initialiser le disque pour pouvoir l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="33eb6-120">After you add a data disk, you need to log on to the VM and initialize the disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="33eb6-121">Association d'un disque existant</span><span class="sxs-lookup"><span data-stu-id="33eb6-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="33eb6-122">Pour attacher un disque existant, vous devez disposer d’un fichier .vhd dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="33eb6-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="33eb6-123">Utilisez l’applet de commande [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) pour télécharger le fichier .vhd dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="33eb6-123">Use the [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet to upload the .vhd file to the storage account.</span></span> <span data-ttu-id="33eb6-124">Après avoir créé et téléchargé le fichier .vhd, vous pouvez l'attacher à une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="33eb6-124">After you've created and uploaded the .vhd file, you can attach it to a VM.</span></span>

1. <span data-ttu-id="33eb6-125">Cliquez sur **Machines virtuelles (Classic)**, puis sélectionnez la machine virtuelle appropriée.</span><span class="sxs-lookup"><span data-stu-id="33eb6-125">Click **Virtual Machines (classic)**, and then select the appropriate virtual machine.</span></span>

2. <span data-ttu-id="33eb6-126">Dans le panneau Paramètres, cliquez sur **Disques**.</span><span class="sxs-lookup"><span data-stu-id="33eb6-126">In the Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="33eb6-127">Dans la barre de commandes, cliquez sur **Attacher un disque existant**.</span><span class="sxs-lookup"><span data-stu-id="33eb6-127">On the command bar, click **Attach existing**.</span></span>

    ![Attacher un disque de données](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="33eb6-129">Cliquez sur **Emplacement**.</span><span class="sxs-lookup"><span data-stu-id="33eb6-129">Click **Location**.</span></span> <span data-ttu-id="33eb6-130">Les comptes de stockage disponibles s’affichent.</span><span class="sxs-lookup"><span data-stu-id="33eb6-130">The available storage accounts display.</span></span> <span data-ttu-id="33eb6-131">Sélectionnez ensuite un compte de stockage approprié dans la liste.</span><span class="sxs-lookup"><span data-stu-id="33eb6-131">Next, select an appropriate storage account from those listed.</span></span>

    ![Fournir un compte de stockage de disques](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="33eb6-133">Un **compte de stockage** dispose d’un ou plusieurs conteneurs qui contiennent des lecteurs de disque (VHD).</span><span class="sxs-lookup"><span data-stu-id="33eb6-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="33eb6-134">Sélectionnez le conteneur approprié dans la liste.</span><span class="sxs-lookup"><span data-stu-id="33eb6-134">Select the appropriate container from those listed.</span></span>

    ![Fournir le conteneur de machines virtuelles windows](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="33eb6-136">Le panneau **Disques durs virtuels** répertorie les lecteurs de disque du conteneur.</span><span class="sxs-lookup"><span data-stu-id="33eb6-136">The **vhds** panel lists the disk drives held in the container.</span></span> <span data-ttu-id="33eb6-137">Cliquez sur l’un des disques, puis cliquez sur Sélectionner.</span><span class="sxs-lookup"><span data-stu-id="33eb6-137">Click one of the disks, and then click Select.</span></span>

    ![Fournir une image de disque pour les machines virtuelles windows](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="33eb6-139">Le panneau **Attacher un disque existant** s’affiche à nouveau, avec l’emplacement contenant le compte de stockage, le conteneur et le disque dur sélectionné (disque dur virtuel) à ajouter à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="33eb6-139">The **Attach existing disk** panel displays again, with the location containing the storage account, container, and selected hard disk (vhd) to add to the virtual machine.</span></span>

  <span data-ttu-id="33eb6-140">Définissez **Mise en cache de l’hôte** sur Aucune ou En lecture seule, puis cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="33eb6-140">Set **Host caching** to none or Read only, then click OK.</span></span>

    ![Disque de données correctement attaché](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
