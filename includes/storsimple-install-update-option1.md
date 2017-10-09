<!--author=SharS last changed: 03/17/2016-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="0638e-101">correctifs logiciels toodownload</span><span class="sxs-lookup"><span data-stu-id="0638e-101">toodownload hotfixes</span></span>
<span data-ttu-id="0638e-102">Effectuer hello étapes toodownload hello logiciel mise à jour suivante.</span><span class="sxs-lookup"><span data-stu-id="0638e-102">Perform hello following steps toodownload hello software update.</span></span>

1. <span data-ttu-id="0638e-103">Démarrez Internet Explorer et accédez trop[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="0638e-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="0638e-104">S’il s’agit de votre première utilisation hello catalogue Microsoft Update sur cet ordinateur, cliquez sur **installer** lorsque tooinstall demandée hello module complémentaire du catalogue Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="0638e-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="0638e-105">![Installer le catalogue](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="0638e-105">![Install catalog](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="0638e-106">Dans la zone de recherche hello Hello catalogue Microsoft Update, entrez le nombre de Base de connaissances (KB) hello de hello correctif souhaité toodownload, par exemple **3063418**, puis cliquez sur **recherche**.</span><span class="sxs-lookup"><span data-stu-id="0638e-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3063418**, and then click **Search**.</span></span>
4. <span data-ttu-id="0638e-107">Vous verrez hello **StorSimple Appliance 1.2 jour** offre groupée.</span><span class="sxs-lookup"><span data-stu-id="0638e-107">You will see hello **StorSimple Update 1.2 Appliance Update** bundle.</span></span> <span data-ttu-id="0638e-108">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="0638e-108">Click **Add**.</span></span> <span data-ttu-id="0638e-109">mise à jour Hello sera ajouté toohello du panier d’achat.</span><span class="sxs-lookup"><span data-stu-id="0638e-109">hello update will be added toohello basket.</span></span>
5. <span data-ttu-id="0638e-110">Recherche de tous les correctifs supplémentaires répertoriées dans le tableau hello ci-dessus (**3043005** et **3063416**) et ajoutez chaque panier hello.</span><span class="sxs-lookup"><span data-stu-id="0638e-110">Search for any additional hotfixes listed in hello table above (**3043005** and **3063416**), and add each hello basket.</span></span>
6. <span data-ttu-id="0638e-111">Cliquez sur **Afficher le panier**.</span><span class="sxs-lookup"><span data-stu-id="0638e-111">Click **View Basket**.</span></span>
   
    ![Afficher le panier](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. <span data-ttu-id="0638e-113">Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="0638e-113">Click **Download**.</span></span> <span data-ttu-id="0638e-114">Spécifiez ou **Parcourir** tooa local emplacement souhaité hello télécharge tooappear.</span><span class="sxs-lookup"><span data-stu-id="0638e-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="0638e-115">Hello mises à jour sont téléchargées toohello l’emplacement spécifié et placé dans un sous-dossier portant le même nom qu’une mise à jour hello de hello.</span><span class="sxs-lookup"><span data-stu-id="0638e-115">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="0638e-116">dossier de Hello peut également être tooa copié partage réseau accessible à partir de l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="0638e-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="0638e-117">les correctifs logiciels Hello doivent être accessibles depuis les deux toodetect contrôleurs toute erreur potentielle de messages à partir du contrôleur homologue de hello.</span><span class="sxs-lookup"><span data-stu-id="0638e-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="0638e-118">tooinstall et vérifiez les correctifs en mode normal</span><span class="sxs-lookup"><span data-stu-id="0638e-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="0638e-119">Effectuer hello suivant les étapes tooinstall et vérifier les correctifs en mode normal hello.</span><span class="sxs-lookup"><span data-stu-id="0638e-119">Perform hello following steps tooinstall and verify hello regular-mode hotfixes.</span></span> <span data-ttu-id="0638e-120">Si vous avez déjà installé à l’aide de hello portail Azure, passez directement trop[installer et vérifier les correctifs en mode de maintenance](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="0638e-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="0638e-121">mettre à jour de logiciels de hello tooinstall, interface de Windows PowerShell hello accès sur votre console série du périphérique StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0638e-121">tooinstall hello software update, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="0638e-122">Suivez hello des instructions dans [console série d’utilisation PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="0638e-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="0638e-123">Appuyez sur l’invite de commande hello, **entrée**.</span><span class="sxs-lookup"><span data-stu-id="0638e-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="0638e-124">Sélectionnez **Option 1** toolog sur l’appareil toohello avec un accès complet.</span><span class="sxs-lookup"><span data-stu-id="0638e-124">Select **Option 1** toolog on toohello device with full access.</span></span>
3. <span data-ttu-id="0638e-125">packages de mise à jour hello tooinstall, à hello invite de commandes, tapez :</span><span class="sxs-lookup"><span data-stu-id="0638e-125">tooinstall hello update package, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="0638e-126">Utilisez IP plutôt que DNS dans le chemin d’accès de partage Bonjour au-dessus de commande.</span><span class="sxs-lookup"><span data-stu-id="0638e-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="0638e-127">paramètre des informations d’identification de Hello est utilisé uniquement si vous accédez à un partage authentifié.</span><span class="sxs-lookup"><span data-stu-id="0638e-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="0638e-128">Nous vous recommandons d’utiliser les partages de tooaccess paramètre hello d’informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="0638e-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="0638e-129">Même les partages qui sont ouverts trop « tout le monde » est généralement pas ouvrir toounauthenticated utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0638e-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="0638e-130">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="0638e-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="0638e-131">Type **Y** lorsque tooconfirm demandée hello installation du correctif logiciel.</span><span class="sxs-lookup"><span data-stu-id="0638e-131">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
5. <span data-ttu-id="0638e-132">Surveiller les mises à jour hello à l’aide de hello `Get-HcsUpdateStatus` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="0638e-132">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="0638e-133">Hello résultat de l’exemple suivant illustre hello mise à jour en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0638e-133">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="0638e-134">Hello `RunInprogress` sera `True` lorsque la mise à jour hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0638e-134">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="0638e-135">Hello suivant l’exemple de sortie indique que cette mise à jour hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="0638e-135">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="0638e-136">Hello `RunInProgress` sera `False` lorsque la mise à jour hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="0638e-136">hello `RunInProgress` will be `False` when hello update has completed.</span></span>

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="0638e-137">Hello occasionnellement, les rapports de l’applet de commande `False` lorsque la mise à jour hello est toujours en cours.</span><span class="sxs-lookup"><span data-stu-id="0638e-137">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="0638e-138">tooensure qui hello correctif est terminée, patientez quelques minutes, réexécutez cette commande et vérifiez que hello `RunInProgress` est `False`.</span><span class="sxs-lookup"><span data-stu-id="0638e-138">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="0638e-139">S’il s’agit, hello correctif est terminée.</span><span class="sxs-lookup"><span data-stu-id="0638e-139">If it is, then hello hotfix has completed.</span></span>
   > 
   > 
6. <span data-ttu-id="0638e-140">Une fois la mise à jour logicielle de hello est terminée, vérifiez les versions des logiciels système hello.</span><span class="sxs-lookup"><span data-stu-id="0638e-140">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="0638e-141">Tapez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0638e-141">Type hello following command:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="0638e-142">Vous devez voir hello versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="0638e-142">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="0638e-143">HcsSoftwareVersion : 6.3.9600.17584</span><span class="sxs-lookup"><span data-stu-id="0638e-143">HcsSoftwareVersion: 6.3.9600.17584</span></span>
   * <span data-ttu-id="0638e-144">CisAgentVersion : 1.0.9049.0</span><span class="sxs-lookup"><span data-stu-id="0638e-144">CisAgentVersion: 1.0.9049.0</span></span>
   * <span data-ttu-id="0638e-145">MdsAgentVersion : 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="0638e-145">MdsAgentVersion: 26.0.4696.1433</span></span>
     
     <span data-ttu-id="0638e-146">Si les numéros de version hello ne changent pas après avoir appliqué la mise à jour hello, il indique ce correctif hello a échoué tooapply.</span><span class="sxs-lookup"><span data-stu-id="0638e-146">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="0638e-147">Dans ce cas, contactez le [Support Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) pour obtenir une assistance supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="0638e-147">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
7. <span data-ttu-id="0638e-148">Répétez les étapes 3 à 5 hello de tooinstall restant le correctif en mode normal (KB3043005).</span><span class="sxs-lookup"><span data-stu-id="0638e-148">Repeat steps 3-5 tooinstall hello remaining regular-mode hotfix (KB3043005).</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="0638e-149">tooinstall et vérifiez les correctifs en mode de maintenance</span><span class="sxs-lookup"><span data-stu-id="0638e-149">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="0638e-150">Utilisez les mises à jour du microprogramme KB3063416 tooinstall disque.</span><span class="sxs-lookup"><span data-stu-id="0638e-150">Use KB3063416 tooinstall disk firmware updates.</span></span> <span data-ttu-id="0638e-151">Ces mises à jour et prennent autour de toocomplete de 30 à 45 minutes.</span><span class="sxs-lookup"><span data-stu-id="0638e-151">These are disruptive updates and take around 30-45 minutes toocomplete.</span></span> <span data-ttu-id="0638e-152">Vous pouvez choisir tooinstall dans une fenêtre de maintenance planifiée par la console série du périphérique toohello connexion.</span><span class="sxs-lookup"><span data-stu-id="0638e-152">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="0638e-153">tooinstall hello disque mises à jour, suivez les instructions de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0638e-153">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="0638e-154">Placez l’appareil de hello en mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="0638e-154">Place hello device in Maintenance mode.</span></span> <span data-ttu-id="0638e-155">Notez que vous ne devez pas utiliser la communication à distance de Windows PowerShell lors de la connexion du périphérique tooa en mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="0638e-155">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="0638e-156">Vous devez toorun cette applet de commande sur le contrôleur de l’appareil hello lorsqu’il est connecté via la console série du périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="0638e-156">You will need toorun this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="0638e-157">Entrez :</span><span class="sxs-lookup"><span data-stu-id="0638e-157">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="0638e-158">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="0638e-158">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="0638e-159">Les deux contrôleurs hello puis redémarrez en mode de Maintenance.</span><span class="sxs-lookup"><span data-stu-id="0638e-159">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="0638e-160">tooinstall hello disque microprogramme mise à jour, type :</span><span class="sxs-lookup"><span data-stu-id="0638e-160">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="0638e-161">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="0638e-161">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="0638e-162">À l’aide de moniteur hello install progression `Get-HcsUpdateStatus` commande.</span><span class="sxs-lookup"><span data-stu-id="0638e-162">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="0638e-163">Hello mise à jour est terminée lorsque hello `RunInProgress` change également`False`.</span><span class="sxs-lookup"><span data-stu-id="0638e-163">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="0638e-164">Une fois l’installation de hello est terminée, contrôleur hello sur lequel le correctif en mode de maintenance hello a été installé sera redémarré.</span><span class="sxs-lookup"><span data-stu-id="0638e-164">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed will be rebooted.</span></span> <span data-ttu-id="0638e-165">Connectez-vous en tant qu’option 1 avec un accès complet et vérifier la version du microprogramme du disque hello.</span><span class="sxs-lookup"><span data-stu-id="0638e-165">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="0638e-166">Entrez :</span><span class="sxs-lookup"><span data-stu-id="0638e-166">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="0638e-167">Hello attendu sont des versions du microprogramme de disque :</span><span class="sxs-lookup"><span data-stu-id="0638e-167">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   <span data-ttu-id="0638e-168">Exécutez hello `Get-HcsFirmwareVersion` commande hello deuxième contrôleur tooverify qui hello version du logiciel a été mis à jour.</span><span class="sxs-lookup"><span data-stu-id="0638e-168">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="0638e-169">Vous pouvez ensuite quitter le mode de maintenance de hello.</span><span class="sxs-lookup"><span data-stu-id="0638e-169">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="0638e-170">Tapez hello commande pour chaque contrôleur de périphérique suivante :</span><span class="sxs-lookup"><span data-stu-id="0638e-170">Type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="0638e-171">contrôleurs de Hello redémarrer lorsque vous quittez le mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="0638e-171">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="0638e-172">Une fois que du microprogramme du disque hello mises à jour sont correctement appliquées et les appareils hello sont sortie du mode de maintenance, retour toohello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="0638e-172">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="0638e-173">Notez que ce portail hello peut ne pas affiche que vous avez installé des mises à jour du mode de Maintenance hello pendant 24 heures.</span><span class="sxs-lookup"><span data-stu-id="0638e-173">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>

