<!--author=alkohli last changed: 09/01/16-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="ab4b3-101">correctifs logiciels toodownload</span><span class="sxs-lookup"><span data-stu-id="ab4b3-101">toodownload hotfixes</span></span>
<span data-ttu-id="ab4b3-102">Effectuer hello suivant étapes toodownload hello mise à jour à partir de hello catalogue Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="ab4b3-103">Démarrez Internet Explorer et accédez trop[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ab4b3-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="ab4b3-104">S’il s’agit de votre première utilisation hello catalogue Microsoft Update sur cet ordinateur, cliquez sur **installer** lorsque tooinstall demandée hello module complémentaire du catalogue Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="ab4b3-105">![Installer le catalogue](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="ab4b3-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="ab4b3-106">Dans la zone de recherche hello Hello catalogue Microsoft Update, entrez le nombre de Base de connaissances (KB) hello de hello correctif souhaité toodownload, par exemple **3186843**, puis cliquez sur **recherche**.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3186843**, and then click **Search**.</span></span>
   
    <span data-ttu-id="ab4b3-107">Hello correctif liste s’affiche, par exemple, **Cumulative 3.0 mise à jour offre groupée du logiciel pour StorSimple 8000 Series**.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 3.0 for StorSimple 8000 Series**.</span></span>
   
    ![Rechercher dans le catalogue](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="ab4b3-109">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-109">Click **Add**.</span></span> <span data-ttu-id="ab4b3-110">mise à jour Hello est ajouté toohello du panier d’achat.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-110">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="ab4b3-111">Recherche de tous les correctifs supplémentaires répertoriées dans le tableau hello ci-dessus (**3186859**) et ajoutez chaque panier toohello.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-111">Search for any additional hotfixes listed in hello table above (**3186859**), and add each toohello basket.</span></span>
6. <span data-ttu-id="ab4b3-112">Cliquez sur **Afficher le panier**.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="ab4b3-113">Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-113">Click **Download**.</span></span> <span data-ttu-id="ab4b3-114">Spécifiez ou **Parcourir** tooa local emplacement souhaité hello télécharge tooappear.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="ab4b3-115">Hello mises à jour sont téléchargées toohello l’emplacement spécifié et placé dans un sous-dossier avec hello même nom en tant que mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-115">hello updates are downloaded toohello specified location and placed in a sub-folder with hello same name as hello update.</span></span> <span data-ttu-id="ab4b3-116">dossier de Hello peut également être tooa copié partage réseau accessible à partir de l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="ab4b3-117">les correctifs logiciels Hello doivent être accessibles depuis les deux toodetect contrôleurs toute erreur potentielle de messages à partir du contrôleur homologue de hello.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="ab4b3-118">tooinstall et vérifiez les correctifs en mode normal</span><span class="sxs-lookup"><span data-stu-id="ab4b3-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="ab4b3-119">Effectuer hello suivant les étapes tooinstall et vérifier les correctifs en mode normal.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-119">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="ab4b3-120">Si vous avez déjà installé à l’aide de hello portail Azure, passez directement trop[installer et vérifier les correctifs en mode de maintenance](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="ab4b3-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="ab4b3-121">correctifs logiciels hello tooinstall, interface de Windows PowerShell hello accès sur votre console série du périphérique StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-121">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="ab4b3-122">Suivez hello des instructions dans [console série d’utilisation PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="ab4b3-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="ab4b3-123">Appuyez sur l’invite de commande hello, **entrée**.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="ab4b3-124">Sélectionnez **Option 1** toolog sur l’appareil toohello avec un accès complet.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-124">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="ab4b3-125">Nous vous recommandons d’installer hello correctif sur le contrôleur passif de hello tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-125">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="ab4b3-126">correctif de hello tooinstall, à hello invite de commandes, tapez :</span><span class="sxs-lookup"><span data-stu-id="ab4b3-126">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="ab4b3-127">Utilisez IP plutôt que DNS dans le chemin d’accès de partage Bonjour au-dessus de commande.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-127">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="ab4b3-128">paramètre des informations d’identification de Hello est utilisé uniquement si vous accédez à un partage authentifié.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-128">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="ab4b3-129">Nous vous recommandons d’utiliser les partages de tooaccess paramètre hello d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-129">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="ab4b3-130">Même les partages qui sont ouverts trop « tout le monde » est généralement pas ouvrir toounauthenticated utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-130">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="ab4b3-131">Fournissez le mot de passe hello lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-131">Supply hello password when prompted.</span></span>
   
    <span data-ttu-id="ab4b3-132">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-132">A sample output is shown below.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \hcsmdssoftwareupdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. <span data-ttu-id="ab4b3-133">Type **Y** lorsque tooconfirm demandée hello installation du correctif logiciel.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-133">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
5. <span data-ttu-id="ab4b3-134">Surveiller les mises à jour hello à l’aide de hello `Get-HcsUpdateStatus` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-134">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="ab4b3-135">mise à jour Hello terminera tout d’abord sur le contrôleur passif de hello.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-135">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="ab4b3-136">Une fois que le contrôleur passif de hello est mise à jour, il y aura un basculement et mise à jour hello puis appliqué sur hello autre contrôleur.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-136">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="ab4b3-137">mise à jour Hello est terminée lorsque les deux contrôleurs hello sont mis à jour.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-137">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="ab4b3-138">Hello résultat de l’exemple suivant illustre hello mise à jour en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-138">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="ab4b3-139">Hello `RunInprogress` sera `True` lorsque la mise à jour hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-139">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 8/29/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="ab4b3-140">Hello suivant l’exemple de sortie indique que cette mise à jour hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-140">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="ab4b3-141">Hello `RunInProgress` sera `False` lorsque la mise à jour hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-141">hello `RunInProgress` will be `False` when hello update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 8/30/2016 9:15:55 AM
    LastUpdateTimestamp : 8/30/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE] 
    > <span data-ttu-id="ab4b3-142">Hello occasionnellement, les rapports de l’applet de commande `False` lorsque la mise à jour hello est toujours en cours.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-142">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="ab4b3-143">tooensure qui hello correctif est terminée, patientez quelques minutes, réexécutez cette commande et vérifiez que hello `RunInProgress` est `False`.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-143">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="ab4b3-144">S’il s’agit, hello correctif est terminée.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-144">If it is, then hello hotfix has completed.</span></span>

1. <span data-ttu-id="ab4b3-145">Une fois la mise à jour logicielle de hello est terminée, vérifiez les versions des logiciels système hello.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-145">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="ab4b3-146">Entrez :</span><span class="sxs-lookup"><span data-stu-id="ab4b3-146">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="ab4b3-147">Vous devez voir hello versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="ab4b3-147">You should see hello following versions:</span></span>
   
   * `HcsSoftwareVersion: 6.3.9600.17759`
   * `CisAgentVersion:  1.0.9343.0`
   * `MdsAgentVersion: 30.0.4698.16`
     
     <span data-ttu-id="ab4b3-148">Si les numéros de version hello ne changent pas après avoir appliqué la mise à jour hello, il indique ce correctif hello a échoué tooapply.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-148">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="ab4b3-149">Dans ce cas, contactez le [Support Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) pour obtenir une assistance supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="ab4b3-150">Vous devez redémarrer le contrôleur actif de hello via hello `Restart-HcsController` applet de commande avant l’application hello mises à jour restantes.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-150">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello remaining updates.</span></span> 
     > 
     > 
2. <span data-ttu-id="ab4b3-151">Répétez les étapes 3 à 5 pilote de hello LSI tooinstall et correctif logiciel de microprogramme **KB3186859**.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-151">Repeat steps 3-5 tooinstall hello LSI driver and firmware hotfix **KB3186859**.</span></span> <span data-ttu-id="ab4b3-152">Après l’installation du correctif hello, utilisez hello `Get-HcsSystem` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-152">After hello hotfix is installed, use hello `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="ab4b3-153">version de Hello LSI doit être :</span><span class="sxs-lookup"><span data-stu-id="ab4b3-153">hello LSI version should be:</span></span>
   
   * `Lsisas2Version: 2.0.78.00`
3. <span data-ttu-id="ab4b3-154">Répétez les étapes 3 à 5 tooinstall hello Storport et mise à jour Spaceport **KB3121261**.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-154">Repeat steps 3-5 tooinstall hello Storport and Spaceport update **KB3121261**.</span></span>
4. <span data-ttu-id="ab4b3-155">Si vous mettez à jour à partir de la mise à jour 2 ou version antérieure, vous devez également toodownload :</span><span class="sxs-lookup"><span data-stu-id="ab4b3-155">If you are updating from Update 2 or earlier version, you will also need toodownload:</span></span>
   
   * <span data-ttu-id="ab4b3-156">Correctif iSCSI avec KB3146621</span><span class="sxs-lookup"><span data-stu-id="ab4b3-156">iSCSI fix using KB3146621</span></span>
   * <span data-ttu-id="ab4b3-157">Correctif WMI avec KB3103616</span><span class="sxs-lookup"><span data-stu-id="ab4b3-157">WMI fix using KB3103616</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="ab4b3-158">tooinstall et vérifiez les correctifs en mode de maintenance</span><span class="sxs-lookup"><span data-stu-id="ab4b3-158">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="ab4b3-159">Utilisez les mises à jour du microprogramme KB3121899 tooinstall disque.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-159">Use KB3121899 tooinstall disk firmware updates.</span></span> <span data-ttu-id="ab4b3-160">Ces mises à jour et prennent environ 30 minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-160">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="ab4b3-161">Vous pouvez choisir tooinstall dans une fenêtre de maintenance planifiée par la console série du périphérique toohello connexion.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-161">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="ab4b3-162">Notez que si le microprogramme du disque est déjà à jour, vous n’aurez pas tooinstall ces mises à jour.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-162">Note that if your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="ab4b3-163">Exécutez hello `Get-HcsUpdateAvailability` applet de commande hello appareil console série toocheck si les mises à jour sont disponibles et hello si des mises à jour sont perturbateur (mode de maintenance) ou sans interruption de service (mode standard) des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-163">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="ab4b3-164">tooinstall hello disque mises à jour, suivez les instructions de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-164">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="ab4b3-165">Placez l’appareil de hello en mode de Maintenance hello.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-165">Place hello device in hello Maintenance mode.</span></span> <span data-ttu-id="ab4b3-166">Notez que vous ne devez pas utiliser la communication à distance de Windows PowerShell lors de la connexion du périphérique tooa en mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-166">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="ab4b3-167">Au lieu de cela, exécutez cette applet de commande sur le contrôleur de l’appareil hello lorsqu’il est connecté via la console série du périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-167">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="ab4b3-168">Entrez :</span><span class="sxs-lookup"><span data-stu-id="ab4b3-168">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="ab4b3-169">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-169">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="ab4b3-170">Les deux contrôleurs hello puis redémarrez en mode de Maintenance.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-170">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="ab4b3-171">tooinstall hello disque microprogramme mise à jour, type :</span><span class="sxs-lookup"><span data-stu-id="ab4b3-171">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="ab4b3-172">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-172">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="ab4b3-173">À l’aide de moniteur hello install progression `Get-HcsUpdateStatus` commande.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-173">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="ab4b3-174">Hello mise à jour est terminée lorsque hello `RunInProgress` change également`False`.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-174">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="ab4b3-175">Après que l’installation de hello est terminée, le contrôleur hello sur quel hello correctif en mode de maintenance a été installé redémarre.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-175">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="ab4b3-176">Connectez-vous en tant qu’option 1 avec un accès complet et vérifier la version du microprogramme du disque hello.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-176">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="ab4b3-177">Entrez :</span><span class="sxs-lookup"><span data-stu-id="ab4b3-177">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="ab4b3-178">Hello attendu sont des versions du microprogramme de disque :</span><span class="sxs-lookup"><span data-stu-id="ab4b3-178">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="ab4b3-179">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-179">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
         ActiveBIOS:0.45.0006
         BackupBIOS:0.45.0008
         MainCPLD:17.0.0005
         ActiveBMCRoot:2.0.000E
         BackupBMCRoot:2.0.000E
         BMCBoot:2.0.0001
         LsiFirmware:19.00.00.00
         LsiBios:07.37.00.00
         Battery1Firmware:06.29
         Battery2Firmware:06.29
         DomFirmware:X231600
         CanisterFirmware:3.5.0.32
         CanisterBootloader:5.03
         CanisterConfigCRC:0xD1B030A4
         CanisterVPDStructure:0x06
         CanisterGEMCPLD:0x17
         CanisterVPDCRC:0xEE3504B4
         MidplaneVPDStructure:0x0C
         MidplaneVPDCRC:0xA6BD4F64
         MidplaneCPLD:0x10
         PCM1Firmware:1.00|1.05
         PCM1VPDStructure:0x05
         PCM1VPDCRC:0x41BEF99C
         PCM2Firmware:1.00|1.05
         PCM2VPDStructure:0x05
         PCM2VPDCRC:0x41BEF99C
   
         DisksFirmware
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
   
    <span data-ttu-id="ab4b3-180">Exécutez hello `Get-HcsFirmwareVersion` commande hello deuxième contrôleur tooverify qui hello version du logiciel a été mis à jour.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-180">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="ab4b3-181">Vous pouvez ensuite quitter le mode de maintenance de hello.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-181">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="ab4b3-182">Par conséquent, toodo de type hello commande pour chaque contrôleur de périphérique suivante :</span><span class="sxs-lookup"><span data-stu-id="ab4b3-182">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="ab4b3-183">contrôleurs de Hello redémarrer lorsque vous quittez le mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-183">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="ab4b3-184">Une fois que du microprogramme du disque hello mises à jour sont correctement appliquées et les appareils hello sont sortie du mode de maintenance, retour toohello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-184">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="ab4b3-185">Notez que ce portail hello peut ne pas affiche que vous avez installé des mises à jour du mode de Maintenance hello pendant 24 heures.</span><span class="sxs-lookup"><span data-stu-id="ab4b3-185">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>

