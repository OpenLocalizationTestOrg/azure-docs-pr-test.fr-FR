<!--author=alkohli last changed: 08/21/17-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="f3370-101">correctifs logiciels toodownload</span><span class="sxs-lookup"><span data-stu-id="f3370-101">toodownload hotfixes</span></span>

<span data-ttu-id="f3370-102">Effectuer hello suivant étapes toodownload hello mise à jour à partir de hello catalogue Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="f3370-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="f3370-103">Démarrez Internet Explorer et accédez trop[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f3370-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="f3370-104">S’il s’agit de votre première utilisation hello catalogue Microsoft Update sur cet ordinateur, cliquez sur **installer** lorsque tooinstall demandée hello module complémentaire du catalogue Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="f3370-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

    ![Installer le catalogue](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="f3370-106">Dans la zone de recherche hello Hello catalogue Microsoft Update, entrez le nombre de Base de connaissances (KB) hello de hello correctif souhaité toodownload, par exemple **4037264**, puis cliquez sur **recherche**.</span><span class="sxs-lookup"><span data-stu-id="f3370-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **4037264**, and then click **Search**.</span></span>
   
    <span data-ttu-id="f3370-107">Hello correctif liste s’affiche, par exemple, **Cumulative 5.0 de mise à jour logicielle offre groupée pour StorSimple 8000 Series**.</span><span class="sxs-lookup"><span data-stu-id="f3370-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 5.0 for StorSimple 8000 Series**.</span></span>
   
    ![Rechercher dans le catalogue](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. <span data-ttu-id="f3370-109">Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="f3370-109">Click **Download**.</span></span> <span data-ttu-id="f3370-110">Spécifiez ou **Parcourir** tooa local emplacement souhaité hello télécharge tooappear.</span><span class="sxs-lookup"><span data-stu-id="f3370-110">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="f3370-111">Cliquez sur les fichiers hello toodownload toohello spécifié l’emplacement et le dossier.</span><span class="sxs-lookup"><span data-stu-id="f3370-111">Click hello files toodownload toohello specified location and folder.</span></span> <span data-ttu-id="f3370-112">dossier de Hello peut également être tooa copié partage réseau accessible à partir de l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="f3370-112">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
5. <span data-ttu-id="f3370-113">Recherche de tous les correctifs supplémentaires répertoriées dans le tableau hello ci-dessus (**4037266**), et hello de téléchargement correspondant de fichiers des dossiers spécifiques toohello comme indiqué dans le tableau précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="f3370-113">Search for any additional hotfixes listed in hello table above (**4037266**), and download hello corresponding files toohello specific folders as listed in hello preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="f3370-114">les correctifs logiciels Hello doivent être accessibles depuis les deux toodetect contrôleurs toute erreur potentielle de messages à partir du contrôleur homologue de hello.</span><span class="sxs-lookup"><span data-stu-id="f3370-114">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
>
> <span data-ttu-id="f3370-115">les correctifs logiciels Hello doivent être copiés dans des dossiers distincts 3.</span><span class="sxs-lookup"><span data-stu-id="f3370-115">hello hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="f3370-116">Par exemple, la mise à jour de l’agent de logiciel/Cis/MDS hello périphérique peut être copié dans _FirstOrderUpdate_ hello de dossier, tous les autres mises à jour sans interruption de service peuvent être copiées à hello _SecondOrderUpdate_ dossier, et mises à jour du mode maintenance copiés dans _ThirdOrderUpdate_ dossier.</span><span class="sxs-lookup"><span data-stu-id="f3370-116">For example, hello device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all hello other non-disruptive updates could be copied in hello _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="f3370-117">tooinstall et vérifiez les correctifs en mode normal</span><span class="sxs-lookup"><span data-stu-id="f3370-117">tooinstall and verify regular mode hotfixes</span></span>

<span data-ttu-id="f3370-118">Effectuer hello suivant les étapes tooinstall et vérifier les correctifs en mode normal.</span><span class="sxs-lookup"><span data-stu-id="f3370-118">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="f3370-119">Si vous avez déjà installé à l’aide de hello portail Azure, passez directement trop[installer et vérifier les correctifs en mode de maintenance](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="f3370-119">If you already installed them using hello Azure portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="f3370-120">correctifs logiciels hello tooinstall, interface de Windows PowerShell hello accès sur votre console série du périphérique StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f3370-120">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="f3370-121">Suivez hello des instructions dans [console série d’utilisation PuTTy tooconnect toohello](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="f3370-121">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="f3370-122">Appuyez sur l’invite de commande hello, **entrée**.</span><span class="sxs-lookup"><span data-stu-id="f3370-122">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="f3370-123">Sélectionnez **Option 1** toolog sur l’appareil toohello avec un accès complet.</span><span class="sxs-lookup"><span data-stu-id="f3370-123">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="f3370-124">Nous vous recommandons d’installer hello correctif sur le contrôleur passif de hello tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="f3370-124">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="f3370-125">correctif de hello tooinstall, à hello invite de commandes, tapez :</span><span class="sxs-lookup"><span data-stu-id="f3370-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="f3370-126">Utilisez IP plutôt que DNS dans le chemin d’accès de partage Bonjour au-dessus de commande.</span><span class="sxs-lookup"><span data-stu-id="f3370-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="f3370-127">paramètre des informations d’identification de Hello est utilisé uniquement si vous accédez à un partage authentifié.</span><span class="sxs-lookup"><span data-stu-id="f3370-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="f3370-128">Nous vous recommandons d’utiliser les partages de tooaccess paramètre hello d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="f3370-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="f3370-129">Même les partages qui sont ouverts trop « tout le monde » est généralement pas ouvrir toounauthenticated utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f3370-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
4. <span data-ttu-id="f3370-130">Fournissez le mot de passe hello lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="f3370-130">Supply hello password when prompted.</span></span> <span data-ttu-id="f3370-131">Vous trouverez ci-dessous un exemple de sortie pour l’installation des mises à jour de commande premier hello.</span><span class="sxs-lookup"><span data-stu-id="f3370-131">A sample output for installing hello first order updates is shown below.</span></span> <span data-ttu-id="f3370-132">Hello première commande mise à jour, vous devez toopoint toohello un fichier spécifique.</span><span class="sxs-lookup"><span data-stu-id="f3370-132">For hello first order update, you need toopoint toohello specific file.</span></span>

    >[!NOTE] 
    > <span data-ttu-id="f3370-133">Vous devez installer hello _HcsSoftwareUpdate.exe_ premier.</span><span class="sxs-lookup"><span data-stu-id="f3370-133">You should install hello _HcsSoftwareUpdate.exe_ first.</span></span> <span data-ttu-id="f3370-134">Une fois l’installation terminée, installez le fichier _CisMdsAgentUpdate.exe_.</span><span class="sxs-lookup"><span data-stu-id="f3370-134">After this install has completed, then install _CisMdsAgentUpdate.exe_.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. <span data-ttu-id="f3370-135">Type **Y** lorsque tooconfirm demandée hello installation du correctif logiciel.</span><span class="sxs-lookup"><span data-stu-id="f3370-135">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
6. <span data-ttu-id="f3370-136">Surveiller les mises à jour hello à l’aide de hello `Get-HcsUpdateStatus` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f3370-136">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="f3370-137">mise à jour Hello terminera tout d’abord sur le contrôleur passif de hello.</span><span class="sxs-lookup"><span data-stu-id="f3370-137">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="f3370-138">Une fois que le contrôleur passif de hello est mise à jour, il y aura un basculement et mise à jour hello puis appliqué sur hello autre contrôleur.</span><span class="sxs-lookup"><span data-stu-id="f3370-138">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="f3370-139">mise à jour Hello est terminée lorsque les deux contrôleurs hello sont mis à jour.</span><span class="sxs-lookup"><span data-stu-id="f3370-139">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="f3370-140">Hello résultat de l’exemple suivant illustre hello mise à jour en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f3370-140">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="f3370-141">Hello `RunInprogress` est `True` lorsque la mise à jour hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f3370-141">hello `RunInprogress` is `True` when hello update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="f3370-142">Hello suivant l’exemple de sortie indique que cette mise à jour hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="f3370-142">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="f3370-143">Hello `RunInProgress` est `False` lorsque la mise à jour hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="f3370-143">hello `RunInProgress` is `False` when hello update is complete.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="f3370-144">Hello occasionnellement, les rapports de l’applet de commande `False` lorsque la mise à jour hello est toujours en cours.</span><span class="sxs-lookup"><span data-stu-id="f3370-144">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="f3370-145">tooensure qui hello correctif est terminée, patientez quelques minutes, réexécutez cette commande et vérifiez que hello `RunInProgress` est `False`.</span><span class="sxs-lookup"><span data-stu-id="f3370-145">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="f3370-146">S’il s’agit, hello correctif est terminée.</span><span class="sxs-lookup"><span data-stu-id="f3370-146">If it is, then hello hotfix has completed.</span></span>

7. <span data-ttu-id="f3370-147">Une fois la mise à jour logicielle de hello est terminée, vérifiez les versions des logiciels système hello.</span><span class="sxs-lookup"><span data-stu-id="f3370-147">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="f3370-148">Entrez :</span><span class="sxs-lookup"><span data-stu-id="f3370-148">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="f3370-149">Vous devez voir hello versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="f3370-149">You should see hello following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    <span data-ttu-id="f3370-150">Si le numéro de version hello ne change pas après avoir appliqué la mise à jour hello, il indique ce correctif hello a échoué tooapply.</span><span class="sxs-lookup"><span data-stu-id="f3370-150">If hello version number does not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="f3370-151">Dans ce cas, contactez le [Support Microsoft](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) pour obtenir une assistance supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="f3370-151">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="f3370-152">Vous devez redémarrer le contrôleur actif de hello via hello `Restart-HcsController` applet de commande avant l’application hello prochaine mise à jour.</span><span class="sxs-lookup"><span data-stu-id="f3370-152">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello next update.</span></span>
     
8. <span data-ttu-id="f3370-153">Répétez les étapes 3 à 6 tooinstall hello _CisMDSAgentupdate.exe_ agent téléchargé tooyour _FirstOrderUpdate_ dossier.</span><span class="sxs-lookup"><span data-stu-id="f3370-153">Repeat steps 3-6 tooinstall hello _CisMDSAgentupdate.exe_ agent downloaded tooyour _FirstOrderUpdate_ folder.</span></span>
8. <span data-ttu-id="f3370-154">Répétez les étapes 3 à 6 tooinstall hello deuxième mises à jour.</span><span class="sxs-lookup"><span data-stu-id="f3370-154">Repeat steps 3-6 tooinstall hello second order updates.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="f3370-155">Deuxième mise à jour de l’ordre, plusieurs mises à jour peuvent être installés en exécutant simplement les hello `Start-HcsHotfix cmdlet` et pointant vers le dossier toohello où se trouvent le deuxième mises à jour.</span><span class="sxs-lookup"><span data-stu-id="f3370-155">For second order updates, multiple updates can be installed by just running hello `Start-HcsHotfix cmdlet` and pointing toohello folder where second order updates are located.</span></span> <span data-ttu-id="f3370-156">applet de commande Hello s’exécute toutes les mises à jour de hello disponibles dans le dossier de hello.</span><span class="sxs-lookup"><span data-stu-id="f3370-156">hello cmdlet will execute all hello updates available in hello folder.</span></span> <span data-ttu-id="f3370-157">Si une mise à jour est déjà installé, la logique de mise à jour hello détectera qu’et pas appliquer cette mise à jour.</span><span class="sxs-lookup"><span data-stu-id="f3370-157">If an update is already installed, hello update logic will detect that and not apply that update.</span></span>

    <span data-ttu-id="f3370-158">Une fois que tous les correctifs hello sont installés, utilisez hello `Get-HcsSystem` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f3370-158">After all hello hotfixes are installed, use hello `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="f3370-159">les versions Hello doivent être :</span><span class="sxs-lookup"><span data-stu-id="f3370-159">hello versions should be:</span></span>
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="f3370-160">tooinstall et vérifiez les correctifs en mode de maintenance</span><span class="sxs-lookup"><span data-stu-id="f3370-160">tooinstall and verify maintenance mode hotfixes</span></span>

<span data-ttu-id="f3370-161">Utilisez les mises à jour du microprogramme KB4037263 tooinstall disque.</span><span class="sxs-lookup"><span data-stu-id="f3370-161">Use KB4037263 tooinstall disk firmware updates.</span></span> <span data-ttu-id="f3370-162">Ces mises à jour et prennent environ 30 minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f3370-162">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="f3370-163">Vous pouvez choisir tooinstall dans une fenêtre de maintenance planifiée par la console série du périphérique toohello connexion.</span><span class="sxs-lookup"><span data-stu-id="f3370-163">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

> [!NOTE] 
> <span data-ttu-id="f3370-164">Si le microprogramme du disque est déjà à jour, vous n’aurez pas tooinstall ces mises à jour.</span><span class="sxs-lookup"><span data-stu-id="f3370-164">If your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="f3370-165">Exécutez hello `Get-HcsUpdateAvailability` applet de commande hello appareil console série toocheck si les mises à jour sont disponibles et hello si des mises à jour sont perturbateur (mode de maintenance) ou sans interruption de service (mode standard) des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="f3370-165">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="f3370-166">tooinstall hello disque mises à jour, suivez les instructions de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f3370-166">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="f3370-167">Placez l’appareil de hello en mode de maintenance hello.</span><span class="sxs-lookup"><span data-stu-id="f3370-167">Place hello device in hello maintenance mode.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="f3370-168">N’utilisez pas la communication à distance de Windows PowerShell lors de la connexion du périphérique tooa en mode maintenance.</span><span class="sxs-lookup"><span data-stu-id="f3370-168">Do not use Windows PowerShell remoting when connecting tooa device in maintenance mode.</span></span> <span data-ttu-id="f3370-169">Au lieu de cela, exécutez cette applet de commande sur le contrôleur de l’appareil hello lorsqu’il est connecté via la console série du périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="f3370-169">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span>

    <span data-ttu-id="f3370-170">contrôleur de hello tooplace en mode maintenance, tapez :</span><span class="sxs-lookup"><span data-stu-id="f3370-170">tooplace hello controller in maintenance mode, type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="f3370-171">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="f3370-171">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="f3370-172">Les deux contrôleurs hello puis redémarrez en mode de maintenance.</span><span class="sxs-lookup"><span data-stu-id="f3370-172">Both hello controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="f3370-173">tooinstall hello disque microprogramme mise à jour, type :</span><span class="sxs-lookup"><span data-stu-id="f3370-173">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="f3370-174">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="f3370-174">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="f3370-175">À l’aide de moniteur hello install progression `Get-HcsUpdateStatus` commande.</span><span class="sxs-lookup"><span data-stu-id="f3370-175">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="f3370-176">Hello mise à jour est terminée lorsque hello `RunInProgress` change également`False`.</span><span class="sxs-lookup"><span data-stu-id="f3370-176">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="f3370-177">Après que l’installation de hello est terminée, le contrôleur hello sur quel hello correctif en mode de maintenance a été installé redémarre.</span><span class="sxs-lookup"><span data-stu-id="f3370-177">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="f3370-178">Connectez-vous en tant qu’option 1 avec un accès complet et vérifier la version du microprogramme du disque hello.</span><span class="sxs-lookup"><span data-stu-id="f3370-178">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="f3370-179">Entrez :</span><span class="sxs-lookup"><span data-stu-id="f3370-179">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="f3370-180">Hello attendu sont des versions du microprogramme de disque :</span><span class="sxs-lookup"><span data-stu-id="f3370-180">hello expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   <span data-ttu-id="f3370-181">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="f3370-181">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17845
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
           ActiveBIOS:0.45.0010
              BackupBIOS:0.45.0006
              MainCPLD:17.0.000b
              ActiveBMCRoot:2.0.001F
              BackupBMCRoot:2.0.001F
              BMCBoot:2.0.0002
              LsiFirmware:20.00.04.00
              LsiBios:07.37.00.00
              Battery1Firmware:06.2C
              Battery2Firmware:06.2C
              DomFirmware:X231600
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0x9134777A
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x19
              CanisterVPDCRC:0x142F7DC2
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:1.00|1.05
              PCM1VPDStructure:0x05
              PCM1VPDCRC:0x41BEF99C
              PCM2Firmware:1.00|1.05
              PCM2VPDStructure:0x05
              PCM2VPDCRC:0x41BEF99C

           EbodFirmware
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0xB23150F8
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x14
              CanisterVPDCRC:0xBAA55828
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:3.11
              PCM1VPDStructure:0x03
              PCM1VPDCRC:0x6B58AD13
              PCM2Firmware:3.11
              PCM2VPDStructure:0x03
              PCM2VPDCRC:0x6B58AD13

           DisksFirmware
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
   
    <span data-ttu-id="f3370-182">Exécutez hello `Get-HcsFirmwareVersion` commande hello deuxième contrôleur tooverify qui hello version du logiciel a été mis à jour.</span><span class="sxs-lookup"><span data-stu-id="f3370-182">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="f3370-183">Vous pouvez ensuite quitter le mode de maintenance de hello.</span><span class="sxs-lookup"><span data-stu-id="f3370-183">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="f3370-184">Par conséquent, toodo de type hello commande pour chaque contrôleur de périphérique suivante :</span><span class="sxs-lookup"><span data-stu-id="f3370-184">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="f3370-185">contrôleurs de Hello redémarrer lorsque vous quittez le mode maintenance.</span><span class="sxs-lookup"><span data-stu-id="f3370-185">hello controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="f3370-186">Une fois que du microprogramme du disque hello mises à jour sont correctement appliquées et appareil de hello a quitté le mode de maintenance, retour toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f3370-186">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure portal.</span></span> <span data-ttu-id="f3370-187">Notez que ce portail hello peut ne pas affiche que vous avez installé des mises à jour du mode de maintenance hello pendant 24 heures.</span><span class="sxs-lookup"><span data-stu-id="f3370-187">Note that hello portal might not show that you installed hello maintenance mode updates for 24 hours.</span></span>

