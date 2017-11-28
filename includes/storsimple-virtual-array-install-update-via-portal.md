<!--author=alkohli last changed: 11/07/16 -->

#### <a name="to-install-updates-via-the-azure-portal"></a><span data-ttu-id="1eba6-101">Pour installer des mises à jour par le biais du portail Azure</span><span class="sxs-lookup"><span data-stu-id="1eba6-101">To install updates via the Azure portal</span></span>

1. <span data-ttu-id="1eba6-102">Accédez à votre gestionnaire de périphériques StorSimple et sélectionnez **Périphériques**.</span><span class="sxs-lookup"><span data-stu-id="1eba6-102">Go to your StorSimple Device Manager and select **Devices**.</span></span> <span data-ttu-id="1eba6-103">Dans la liste des périphériques connectés à votre service, sélectionnez et cliquez sur le périphérique que vous souhaitez mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="1eba6-103">From the list of devices connected to your service, select and click the device you want to update.</span></span> 

    ![mettre à jour l'appareil](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate1m.png) 

2. <span data-ttu-id="1eba6-105">Dans le panneau **Paramètres**, cliquez sur **Mises à jour de l’appareil**.</span><span class="sxs-lookup"><span data-stu-id="1eba6-105">In the **Settings** blade, click **Device updates**.</span></span> 

    ![mettre à jour l'appareil](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate2m.png)  

3. <span data-ttu-id="1eba6-107">Un message s’affiche si des mises à jour logicielles sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="1eba6-107">You see a message if the software updates are available.</span></span> <span data-ttu-id="1eba6-108">Pour rechercher des mises à jour, vous pouvez également cliquer sur **Analyser**.</span><span class="sxs-lookup"><span data-stu-id="1eba6-108">To check for updates, you can also click **Scan**.</span></span>

    ![mettre à jour l'appareil](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate3m.png)

    <span data-ttu-id="1eba6-110">Un message s’affichera au début et à la fin de l’analyse.</span><span class="sxs-lookup"><span data-stu-id="1eba6-110">You will be notified when the scan starts and completes successfully.</span></span>

    ![mettre à jour l'appareil](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate5m.png)

4. <span data-ttu-id="1eba6-112">Une fois les mises à jour analysées, cliquez sur **Télécharger les mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="1eba6-112">Once the updates are scanned, click **Download updates**.</span></span> 

    ![mettre à jour l'appareil](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate6m.png)

5. <span data-ttu-id="1eba6-114">Dans le panneau **Nouvelles mises à jour**, un message indique que lorsque les mises à jour seront téléchargées, vous devrez confirmer l’installation.</span><span class="sxs-lookup"><span data-stu-id="1eba6-114">In the **New updates** blade, review the information that after the updates are downloaded, you need to confirm the installation.</span></span> <span data-ttu-id="1eba6-115">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1eba6-115">Click **OK**.</span></span>

    ![mettre à jour l'appareil](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate7m.png)

6. <span data-ttu-id="1eba6-117">Un message s’affichera au début et à la fin du téléchargement.</span><span class="sxs-lookup"><span data-stu-id="1eba6-117">You are notified when the upload starts and completes successfully.</span></span>

     ![mettre à jour l'appareil](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate8m.png)

5. <span data-ttu-id="1eba6-119">Dans le panneau **Mises à jour de l’appareil**, cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="1eba6-119">In the **Device updates** blade, click **Install**.</span></span>

     ![mettre à jour l'appareil](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate11m.png)   

6. <span data-ttu-id="1eba6-121">Dans le panneau **Nouvelles mises à jour**, vous êtes averti que la mise à jour peut perturber le fonctionnement de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="1eba6-121">In the **New updates** blade, you are warned that the update is disruptive.</span></span> <span data-ttu-id="1eba6-122">Dans la mesure où Virtual Array est un appareil à nœud unique, il redémarre après la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="1eba6-122">As virtual array is a single node device, the device restarts after it is updated.</span></span> <span data-ttu-id="1eba6-123">Cela perturbe les éventuelles E/S en cours.</span><span class="sxs-lookup"><span data-stu-id="1eba6-123">This disrupts any IO in progress.</span></span> <span data-ttu-id="1eba6-124">Cliquez sur **OK** pour installer les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="1eba6-124">Click **OK** to install the updates.</span></span> 

    ![mettre à jour l'appareil](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate12m.png) 

7. <span data-ttu-id="1eba6-126">Vous êtes averti lorsque le travail d’installation démarre.</span><span class="sxs-lookup"><span data-stu-id="1eba6-126">You are notified when the install job starts.</span></span> 

    ![mettre à jour l'appareil](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate13m.png)

8.  <span data-ttu-id="1eba6-128">Une fois l’installation terminée, cliquez sur le lien **Afficher le travail** dans le panneau **Mises à jour de l’appareil** pour suivre l’installation.</span><span class="sxs-lookup"><span data-stu-id="1eba6-128">After the install job completes successfully, click **View Job** link in the **Device updates** blade to monitor the installation.</span></span> 

    ![mettre à jour l'appareil](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate15m.png)

    <span data-ttu-id="1eba6-130">Vous accéderez au panneau **Installer les mises à jour**.</span><span class="sxs-lookup"><span data-stu-id="1eba6-130">This takes you to the **Install Updates** blade.</span></span> <span data-ttu-id="1eba6-131">Des informations détaillées sur le travail y sont indiquées.</span><span class="sxs-lookup"><span data-stu-id="1eba6-131">You can view detailed information about the job here.</span></span>

    ![mettre à jour l'appareil](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate16m.png)

9. <span data-ttu-id="1eba6-133">Une fois les mises à jour correctement installées, vous voyez un message vous l’indiquant dans le panneau Mises à jour de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="1eba6-133">After the updates are successfully installed, you see a message to this effect in the Device updates blade.</span></span> <span data-ttu-id="1eba6-134">La version du logiciel devient également **10.0.10288.0**.</span><span class="sxs-lookup"><span data-stu-id="1eba6-134">The software version also changes to **10.0.10288.0**.</span></span> 

    ![mettre à jour l'appareil](../includes/media/storsimple-virtual-array-install-update-via-portal/azupdate17m.png)