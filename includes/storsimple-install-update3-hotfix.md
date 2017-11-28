<!--author=alkohli last changed: 09/01/16-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="8e185-101">Pour télécharger des correctifs logiciels</span><span class="sxs-lookup"><span data-stu-id="8e185-101">To download hotfixes</span></span>
<span data-ttu-id="8e185-102">Procédez comme suit pour télécharger la mise à jour logicielle à partir du Catalogue Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="8e185-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="8e185-103">Démarrez Internet Explorer et accédez à [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="8e185-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="8e185-104">Si vous utilisez le catalogue Microsoft Update pour la première fois sur cet ordinateur, cliquez sur **Installer** lorsque vous êtes invité à installer le module complémentaire Catalogue Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="8e185-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="8e185-105">![Installer le catalogue](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="8e185-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="8e185-106">Dans la zone de recherche du Catalogue Microsoft Update, entrez le numéro KB (Base de connaissances) du correctif logiciel que vous souhaitez télécharger, par exemple **3186843**, puis cliquez sur **Rechercher**.</span><span class="sxs-lookup"><span data-stu-id="8e185-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3186843**, and then click **Search**.</span></span>
   
    <span data-ttu-id="8e185-107">La liste des correctifs s’affiche, par exemple **Ensemble de logiciels Update 3.0 pour StorSimple série 8000**.</span><span class="sxs-lookup"><span data-stu-id="8e185-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 3.0 for StorSimple 8000 Series**.</span></span>
   
    ![Rechercher dans le catalogue](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="8e185-109">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="8e185-109">Click **Add**.</span></span> <span data-ttu-id="8e185-110">La mise à jour est ajoutée au panier.</span><span class="sxs-lookup"><span data-stu-id="8e185-110">The update is added to the basket.</span></span>
5. <span data-ttu-id="8e185-111">Recherchez les correctifs supplémentaires répertoriés dans le tableau ci-dessus (**3186859**) et ajoutez-les au panier.</span><span class="sxs-lookup"><span data-stu-id="8e185-111">Search for any additional hotfixes listed in the table above (**3186859**), and add each to the basket.</span></span>
6. <span data-ttu-id="8e185-112">Cliquez sur **Afficher le panier**.</span><span class="sxs-lookup"><span data-stu-id="8e185-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="8e185-113">Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="8e185-113">Click **Download**.</span></span> <span data-ttu-id="8e185-114">Spécifiez ou **recherchez** l'emplacement local où vous voulez effectuer les téléchargements.</span><span class="sxs-lookup"><span data-stu-id="8e185-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="8e185-115">Les mises à jour sont téléchargées à l’emplacement spécifié et placées dans un sous-dossier portant le même nom que la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="8e185-115">The updates are downloaded to the specified location and placed in a sub-folder with the same name as the update.</span></span> <span data-ttu-id="8e185-116">Ce dossier peut également être copié sur un partage réseau accessible à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="8e185-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="8e185-117">Les correctifs doivent être accessibles depuis les deux contrôleurs pour détecter les messages d’erreur potentiels à partir du contrôleur homologue.</span><span class="sxs-lookup"><span data-stu-id="8e185-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="8e185-118">Pour installer et vérifier les correctifs logiciels en mode Normal</span><span class="sxs-lookup"><span data-stu-id="8e185-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="8e185-119">Procédez comme suit pour installer et vérifier les correctifs logiciels en mode Normal.</span><span class="sxs-lookup"><span data-stu-id="8e185-119">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="8e185-120">Si vous les avez déjà installés à l’aide du portail Azure, passez directement à [Installer et vérifier les correctifs en mode maintenance](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="8e185-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="8e185-121">Pour installer les correctifs logiciels, accédez à l’interface Windows PowerShell sur la console série de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8e185-121">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="8e185-122">Suivez les instructions détaillées de la section [Utilisation de PuTTY pour se connecter à la console série de l’appareil](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="8e185-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="8e185-123">À l'invite de commandes, appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="8e185-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="8e185-124">Sélectionnez **Option 1** pour vous connecter à l’appareil avec un accès complet.</span><span class="sxs-lookup"><span data-stu-id="8e185-124">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="8e185-125">Nous vous recommandons d’installer le correctif d’abord sur le contrôleur passif.</span><span class="sxs-lookup"><span data-stu-id="8e185-125">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="8e185-126">Pour installer le correctif logiciel, tapez ce qui suit à l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="8e185-126">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="8e185-127">Utilisez IP au lieu de DNS dans le chemin d'accès du partage dans la commande ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8e185-127">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="8e185-128">Le paramètre Informations d’identification n’est utilisé que si vous accédez à un partage authentifié.</span><span class="sxs-lookup"><span data-stu-id="8e185-128">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="8e185-129">Nous vous recommandons d'utiliser le paramètre d'informations d'identification pour accéder aux partages.</span><span class="sxs-lookup"><span data-stu-id="8e185-129">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="8e185-130">Même les partages qui sont ouverts à « tout le monde » ne sont généralement pas ouverts aux utilisateurs non authentifiés.</span><span class="sxs-lookup"><span data-stu-id="8e185-130">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="8e185-131">Indiquez le mot de passe lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="8e185-131">Supply the password when prompted.</span></span>
   
    <span data-ttu-id="8e185-132">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="8e185-132">A sample output is shown below.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \hcsmdssoftwareupdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. <span data-ttu-id="8e185-133">Tapez **Y** lorsque vous êtes invité à confirmer l’installation du correctif.</span><span class="sxs-lookup"><span data-stu-id="8e185-133">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="8e185-134">Contrôlez la mise à jour à l'aide de l'applet de commande `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="8e185-134">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="8e185-135">La mise à jour se termine d’abord sur le contrôleur passif.</span><span class="sxs-lookup"><span data-stu-id="8e185-135">The update will first complete on the passive controller.</span></span> <span data-ttu-id="8e185-136">Une fois le contrôleur passif mis à jour, un basculement se produit et la mise à jour est ensuite appliquée à l’autre contrôleur.</span><span class="sxs-lookup"><span data-stu-id="8e185-136">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="8e185-137">La mise à jour est terminée lorsque les deux contrôleurs sont mis à jour.</span><span class="sxs-lookup"><span data-stu-id="8e185-137">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="8e185-138">L’exemple de sortie suivant indique que la mise à jour est en cours.</span><span class="sxs-lookup"><span data-stu-id="8e185-138">The following sample output shows the update in progress.</span></span> <span data-ttu-id="8e185-139">`RunInprogress` a la valeur `True` lorsque la mise à jour est en cours.</span><span class="sxs-lookup"><span data-stu-id="8e185-139">The `RunInprogress` will be `True` when the update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 8/29/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="8e185-140">L’exemple de sortie suivant indique que la mise à jour est terminée.</span><span class="sxs-lookup"><span data-stu-id="8e185-140">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="8e185-141">`RunInProgress` a la valeur `False` lorsque la mise à jour est terminée.</span><span class="sxs-lookup"><span data-stu-id="8e185-141">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 8/30/2016 9:15:55 AM
    LastUpdateTimestamp : 8/30/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE] 
    > <span data-ttu-id="8e185-142">Parfois, l'applet de commande indique `False` lorsque la mise à jour est encore en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="8e185-142">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="8e185-143">Pour vous assurer que le correctif logiciel est terminé, patientez quelques minutes, exécutez à nouveau cette commande et vérifiez que `RunInProgress` est `False`.</span><span class="sxs-lookup"><span data-stu-id="8e185-143">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="8e185-144">Dans ce cas, le correctif est terminé.</span><span class="sxs-lookup"><span data-stu-id="8e185-144">If it is, then the hotfix has completed.</span></span>

1. <span data-ttu-id="8e185-145">Lorsque la mise à jour logicielle est terminée, vérifiez les versions des logiciels du système.</span><span class="sxs-lookup"><span data-stu-id="8e185-145">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="8e185-146">Entrez :</span><span class="sxs-lookup"><span data-stu-id="8e185-146">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="8e185-147">Vous devez voir les versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="8e185-147">You should see the following versions:</span></span>
   
   * `HcsSoftwareVersion: 6.3.9600.17759`
   * `CisAgentVersion:  1.0.9343.0`
   * `MdsAgentVersion: 30.0.4698.16`
     
     <span data-ttu-id="8e185-148">Si les numéros de version ne changent pas après la mise à jour, cela indique que le correctif n'a pas pu s'appliquer.</span><span class="sxs-lookup"><span data-stu-id="8e185-148">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="8e185-149">Dans ce cas, contactez le [Support Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) pour obtenir une assistance supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="8e185-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="8e185-150">Vous devez redémarrer le contrôleur actif via l’applet de commande `Restart-HcsController` avant d’appliquer les autres mises à jour.</span><span class="sxs-lookup"><span data-stu-id="8e185-150">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the remaining updates.</span></span> 
     > 
     > 
2. <span data-ttu-id="8e185-151">Répétez les étapes 3 à 5 pour installer le correctif du microprogramme et du pilote LSI **KB3186859**.</span><span class="sxs-lookup"><span data-stu-id="8e185-151">Repeat steps 3-5 to install the LSI driver and firmware hotfix **KB3186859**.</span></span> <span data-ttu-id="8e185-152">Une fois le correctif installé, utilisez l’applet de commande `Get-HcsSystem` .</span><span class="sxs-lookup"><span data-stu-id="8e185-152">After the hotfix is installed, use the `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="8e185-153">La version LSI doit être :</span><span class="sxs-lookup"><span data-stu-id="8e185-153">The LSI version should be:</span></span>
   
   * `Lsisas2Version: 2.0.78.00`
3. <span data-ttu-id="8e185-154">Répétez les étapes 3 à 5 pour installer la mise à jour Storport et Spaceport **KB3121261**.</span><span class="sxs-lookup"><span data-stu-id="8e185-154">Repeat steps 3-5 to install the Storport and Spaceport update **KB3121261**.</span></span>
4. <span data-ttu-id="8e185-155">Si vous effectuez la mise à jour à partir d’Update 2 ou d’une version antérieure, vous devrez également télécharger :</span><span class="sxs-lookup"><span data-stu-id="8e185-155">If you are updating from Update 2 or earlier version, you will also need to download:</span></span>
   
   * <span data-ttu-id="8e185-156">Correctif iSCSI avec KB3146621</span><span class="sxs-lookup"><span data-stu-id="8e185-156">iSCSI fix using KB3146621</span></span>
   * <span data-ttu-id="8e185-157">Correctif WMI avec KB3103616</span><span class="sxs-lookup"><span data-stu-id="8e185-157">WMI fix using KB3103616</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="8e185-158">Pour installer et vérifier les correctifs logiciels en mode Maintenance</span><span class="sxs-lookup"><span data-stu-id="8e185-158">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="8e185-159">Utilisez l’article KB3121899 pour installer les mises à jour du microprogramme de disque.</span><span class="sxs-lookup"><span data-stu-id="8e185-159">Use KB3121899 to install disk firmware updates.</span></span> <span data-ttu-id="8e185-160">Ces mises à jour, qui entraînent des perturbations, nécessitent environ 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="8e185-160">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="8e185-161">Vous pouvez choisir de les installer dans une fenêtre de maintenance planifiée en vous connectant à la console série du périphérique.</span><span class="sxs-lookup"><span data-stu-id="8e185-161">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="8e185-162">Notez que si votre microprogramme de disque est déjà à jour, vous n’aurez pas à installer ces mises à jour.</span><span class="sxs-lookup"><span data-stu-id="8e185-162">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="8e185-163">Exécutez l’applet de commande `Get-HcsUpdateAvailability` à partir de la console série de l’appareil pour vérifier si des mises à jour sont disponibles et si elles risquent de provoquer une interruption de service (mode maintenance) ou non (mode normal).</span><span class="sxs-lookup"><span data-stu-id="8e185-163">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="8e185-164">Pour installer les mises à jour du microprogramme de disque, suivez les instructions ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8e185-164">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="8e185-165">Mettez l’appareil en mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="8e185-165">Place the device in the Maintenance mode.</span></span> <span data-ttu-id="8e185-166">Notez que vous ne devez pas utiliser l’accès distant Windows PowerShell quand vous vous connectez à un appareil en mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="8e185-166">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="8e185-167">À la place, exécutez cette applet de commande sur le contrôleur de l’appareil si vous êtes connecté par le biais de la console série de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="8e185-167">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="8e185-168">Entrez :</span><span class="sxs-lookup"><span data-stu-id="8e185-168">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="8e185-169">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="8e185-169">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="8e185-170">Les deux contrôleurs redémarrent alors en mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="8e185-170">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="8e185-171">Pour installer la mise à jour du microprogramme de disque, tapez :</span><span class="sxs-lookup"><span data-stu-id="8e185-171">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="8e185-172">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="8e185-172">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="8e185-173">Surveillez la progression de l’installation à l’aide de la commande `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="8e185-173">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="8e185-174">La mise à jour est terminée quand `RunInProgress` passe à `False`.</span><span class="sxs-lookup"><span data-stu-id="8e185-174">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="8e185-175">Une fois l’installation terminée, le contrôleur sur lequel le correctif logiciel en mode Maintenance a été installé redémarre.</span><span class="sxs-lookup"><span data-stu-id="8e185-175">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="8e185-176">Connectez-vous avec l’option 1 (accès total) et vérifiez la version du microprogramme de disque.</span><span class="sxs-lookup"><span data-stu-id="8e185-176">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="8e185-177">Entrez :</span><span class="sxs-lookup"><span data-stu-id="8e185-177">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="8e185-178">Les versions attendues du microprogramme de disque sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="8e185-178">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="8e185-179">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="8e185-179">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
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
   
    <span data-ttu-id="8e185-180">Exécutez la commande `Get-HcsFirmwareVersion` sur le deuxième contrôleur pour vérifier que la version du logiciel a été mise à jour.</span><span class="sxs-lookup"><span data-stu-id="8e185-180">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="8e185-181">Vous pouvez à présent quitter le mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="8e185-181">You can then exit the maintenance mode.</span></span> <span data-ttu-id="8e185-182">Pour ce faire, tapez la commande suivante pour chaque contrôleur d’appareil :</span><span class="sxs-lookup"><span data-stu-id="8e185-182">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="8e185-183">Les contrôleurs redémarrent quand vous quittez le mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="8e185-183">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="8e185-184">Une fois que les mises à jour du microprogramme de disque ont été appliquées avec succès et que l’appareil a quitté le mode Maintenance, revenez au portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="8e185-184">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="8e185-185">Remarque : il se peut que le portail n’affiche pas les mises à jour installées en mode Maintenance pendant 24 heures.</span><span class="sxs-lookup"><span data-stu-id="8e185-185">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

