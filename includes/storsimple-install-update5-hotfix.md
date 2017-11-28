<!--author=alkohli last changed: 08/21/17-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="76be9-101">Pour télécharger des correctifs logiciels</span><span class="sxs-lookup"><span data-stu-id="76be9-101">To download hotfixes</span></span>

<span data-ttu-id="76be9-102">Procédez comme suit pour télécharger la mise à jour logicielle à partir du Catalogue Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="76be9-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="76be9-103">Démarrez Internet Explorer et accédez à [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="76be9-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="76be9-104">Si vous utilisez le catalogue Microsoft Update pour la première fois sur cet ordinateur, cliquez sur **Installer** lorsque vous êtes invité à installer le module complémentaire Catalogue Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="76be9-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

    ![Installer le catalogue](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="76be9-106">Dans la zone de recherche du Catalogue Microsoft Update, entrez le numéro KB (Base de connaissances) du correctif logiciel que vous souhaitez télécharger, par exemple **4037264**, puis cliquez sur **Rechercher**.</span><span class="sxs-lookup"><span data-stu-id="76be9-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **4037264**, and then click **Search**.</span></span>
   
    <span data-ttu-id="76be9-107">La liste des correctifs s’affiche, par exemple **Ensemble de logiciels Update 5.0 pour StorSimple série 8000**.</span><span class="sxs-lookup"><span data-stu-id="76be9-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 5.0 for StorSimple 8000 Series**.</span></span>
   
    ![Rechercher dans le catalogue](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. <span data-ttu-id="76be9-109">Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="76be9-109">Click **Download**.</span></span> <span data-ttu-id="76be9-110">Spécifiez ou **recherchez** l'emplacement local où vous voulez effectuer les téléchargements.</span><span class="sxs-lookup"><span data-stu-id="76be9-110">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="76be9-111">Cliquez sur les fichiers à télécharger vers l’emplacement et le dossier spécifiés.</span><span class="sxs-lookup"><span data-stu-id="76be9-111">Click the files to download to the specified location and folder.</span></span> <span data-ttu-id="76be9-112">Ce dossier peut également être copié sur un partage réseau accessible à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="76be9-112">The folder can also be copied to a network share that is reachable from the device.</span></span>
5. <span data-ttu-id="76be9-113">Recherchez les correctifs logiciels supplémentaires répertoriés dans le tableau ci-dessus (**4037266**) et téléchargez les fichiers correspondants vers les dossiers spécifiques répertoriés dans le tableau précédent.</span><span class="sxs-lookup"><span data-stu-id="76be9-113">Search for any additional hotfixes listed in the table above (**4037266**), and download the corresponding files to the specific folders as listed in the preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="76be9-114">Les correctifs doivent être accessibles depuis les deux contrôleurs pour détecter les messages d’erreur potentiels à partir du contrôleur homologue.</span><span class="sxs-lookup"><span data-stu-id="76be9-114">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
>
> <span data-ttu-id="76be9-115">Les correctifs doivent être copiés dans trois dossiers séparés.</span><span class="sxs-lookup"><span data-stu-id="76be9-115">The hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="76be9-116">Par exemple, la mise à jour de l’agent MDS/Cis/du logiciel de l’appareil peut être copiée dans le dossier _FirstOrderUpdate_, tandis que toutes les autres mises à jour non perturbatrices peuvent être copiées dans le dossier _SecondOrderUpdate_ et les mises à jour du mode maintenance dans le dossier _ThirdOrderUpdate_.</span><span class="sxs-lookup"><span data-stu-id="76be9-116">For example, the device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all the other non-disruptive updates could be copied in the _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="76be9-117">Pour installer et vérifier les correctifs logiciels en mode Normal</span><span class="sxs-lookup"><span data-stu-id="76be9-117">To install and verify regular mode hotfixes</span></span>

<span data-ttu-id="76be9-118">Procédez comme suit pour installer et vérifier les correctifs logiciels en mode Normal.</span><span class="sxs-lookup"><span data-stu-id="76be9-118">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="76be9-119">Si vous les avez déjà installés à l’aide du portail Azure, passez directement à [Installer et vérifier les correctifs en mode maintenance](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="76be9-119">If you already installed them using the Azure portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="76be9-120">Pour installer les correctifs logiciels, accédez à l’interface Windows PowerShell sur la console série de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="76be9-120">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="76be9-121">Suivez les instructions détaillées de la section [Utilisation de PuTTY pour se connecter à la console série de l’appareil](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="76be9-121">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="76be9-122">À l'invite de commandes, appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="76be9-122">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="76be9-123">Sélectionnez **Option 1** pour vous connecter à l’appareil avec un accès complet.</span><span class="sxs-lookup"><span data-stu-id="76be9-123">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="76be9-124">Nous vous recommandons d’installer le correctif d’abord sur le contrôleur passif.</span><span class="sxs-lookup"><span data-stu-id="76be9-124">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="76be9-125">Pour installer le correctif logiciel, tapez ce qui suit à l’invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="76be9-125">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="76be9-126">Utilisez IP au lieu de DNS dans le chemin d'accès du partage dans la commande ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="76be9-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="76be9-127">Le paramètre Informations d’identification n’est utilisé que si vous accédez à un partage authentifié.</span><span class="sxs-lookup"><span data-stu-id="76be9-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="76be9-128">Nous vous recommandons d'utiliser le paramètre d'informations d'identification pour accéder aux partages.</span><span class="sxs-lookup"><span data-stu-id="76be9-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="76be9-129">Même les partages qui sont ouverts à « tout le monde » ne sont généralement pas ouverts aux utilisateurs non authentifiés.</span><span class="sxs-lookup"><span data-stu-id="76be9-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
4. <span data-ttu-id="76be9-130">Indiquez le mot de passe lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="76be9-130">Supply the password when prompted.</span></span> <span data-ttu-id="76be9-131">Vous trouverez ci-dessous un exemple de sortie pour l’installation des mises à jour prioritaires.</span><span class="sxs-lookup"><span data-stu-id="76be9-131">A sample output for installing the first order updates is shown below.</span></span> <span data-ttu-id="76be9-132">Pour la première mise à jour de commande, vous devez pointer vers le fichier spécifique.</span><span class="sxs-lookup"><span data-stu-id="76be9-132">For the first order update, you need to point to the specific file.</span></span>

    >[!NOTE] 
    > <span data-ttu-id="76be9-133">Vous devez d’abord installer le fichier _HcsSoftwareUpdate.exe_.</span><span class="sxs-lookup"><span data-stu-id="76be9-133">You should install the _HcsSoftwareUpdate.exe_ first.</span></span> <span data-ttu-id="76be9-134">Une fois l’installation terminée, installez le fichier _CisMdsAgentUpdate.exe_.</span><span class="sxs-lookup"><span data-stu-id="76be9-134">After this install has completed, then install _CisMdsAgentUpdate.exe_.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. <span data-ttu-id="76be9-135">Tapez **Y** lorsque vous êtes invité à confirmer l’installation du correctif.</span><span class="sxs-lookup"><span data-stu-id="76be9-135">Type **Y** when prompted to confirm the hotfix installation.</span></span>
6. <span data-ttu-id="76be9-136">Contrôlez la mise à jour à l'aide de l'applet de commande `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="76be9-136">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="76be9-137">La mise à jour se termine d’abord sur le contrôleur passif.</span><span class="sxs-lookup"><span data-stu-id="76be9-137">The update will first complete on the passive controller.</span></span> <span data-ttu-id="76be9-138">Une fois le contrôleur passif mis à jour, un basculement se produit et la mise à jour est ensuite appliquée à l’autre contrôleur.</span><span class="sxs-lookup"><span data-stu-id="76be9-138">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="76be9-139">La mise à jour est terminée lorsque les deux contrôleurs sont mis à jour.</span><span class="sxs-lookup"><span data-stu-id="76be9-139">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="76be9-140">L’exemple de sortie suivant indique que la mise à jour est en cours.</span><span class="sxs-lookup"><span data-stu-id="76be9-140">The following sample output shows the update in progress.</span></span> <span data-ttu-id="76be9-141">`RunInprogress` a la valeur `True` lorsque la mise à jour est en cours.</span><span class="sxs-lookup"><span data-stu-id="76be9-141">The `RunInprogress` is `True` when the update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="76be9-142">L’exemple de sortie suivant indique que la mise à jour est terminée.</span><span class="sxs-lookup"><span data-stu-id="76be9-142">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="76be9-143">`RunInProgress` a la valeur `False` lorsque la mise à jour est terminée.</span><span class="sxs-lookup"><span data-stu-id="76be9-143">The `RunInProgress` is `False` when the update is complete.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="76be9-144">Parfois, l'applet de commande indique `False` lorsque la mise à jour est encore en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="76be9-144">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="76be9-145">Pour vous assurer que le correctif logiciel est terminé, patientez quelques minutes, exécutez à nouveau cette commande et vérifiez que `RunInProgress` est `False`.</span><span class="sxs-lookup"><span data-stu-id="76be9-145">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="76be9-146">Dans ce cas, le correctif est terminé.</span><span class="sxs-lookup"><span data-stu-id="76be9-146">If it is, then the hotfix has completed.</span></span>

7. <span data-ttu-id="76be9-147">Lorsque la mise à jour logicielle est terminée, vérifiez les versions des logiciels du système.</span><span class="sxs-lookup"><span data-stu-id="76be9-147">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="76be9-148">Entrez :</span><span class="sxs-lookup"><span data-stu-id="76be9-148">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="76be9-149">Vous devez voir les versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="76be9-149">You should see the following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    <span data-ttu-id="76be9-150">Si le numéro de version ne change pas après la mise à jour, cela indique que le correctif n’a pas pu s’appliquer.</span><span class="sxs-lookup"><span data-stu-id="76be9-150">If the version number does not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="76be9-151">Dans ce cas, contactez le [Support Microsoft](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) pour obtenir une assistance supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="76be9-151">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="76be9-152">Vous devez redémarrer le contrôleur actif via la cmdlet `Restart-HcsController` avant d’appliquer la prochaine mise à jour.</span><span class="sxs-lookup"><span data-stu-id="76be9-152">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the next update.</span></span>
     
8. <span data-ttu-id="76be9-153">Répétez les étapes 3 à 6 pour installer l’agent _CisMDSAgentupdate.exe_ téléchargé vers votre dossier _FirstOrderUpdate_.</span><span class="sxs-lookup"><span data-stu-id="76be9-153">Repeat steps 3-6 to install the _CisMDSAgentupdate.exe_ agent downloaded to your _FirstOrderUpdate_ folder.</span></span>
8. <span data-ttu-id="76be9-154">Répétez les étapes 3 à 6 pour installer les mises à jour de deuxième priorité.</span><span class="sxs-lookup"><span data-stu-id="76be9-154">Repeat steps 3-6 to install the second order updates.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="76be9-155">Pour les mises à jour de la deuxième commande, il est possible d’installer plusieurs mises à jour en exécutant simplement `Start-HcsHotfix cmdlet` et en désignant le dossier où se trouvent les mises à jour de deuxième priorité.</span><span class="sxs-lookup"><span data-stu-id="76be9-155">For second order updates, multiple updates can be installed by just running the `Start-HcsHotfix cmdlet` and pointing to the folder where second order updates are located.</span></span> <span data-ttu-id="76be9-156">L’applet de commande exécute alors toutes les mises à jour disponibles dans le dossier.</span><span class="sxs-lookup"><span data-stu-id="76be9-156">The cmdlet will execute all the updates available in the folder.</span></span> <span data-ttu-id="76be9-157">La logique de mise à jour détecte les éventuelles mises à jour déjà installées et ne les applique pas.</span><span class="sxs-lookup"><span data-stu-id="76be9-157">If an update is already installed, the update logic will detect that and not apply that update.</span></span>

    <span data-ttu-id="76be9-158">Une fois tous les correctifs installés, utilisez l’applet de commande `Get-HcsSystem`.</span><span class="sxs-lookup"><span data-stu-id="76be9-158">After all the hotfixes are installed, use the `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="76be9-159">Les versions doivent être les suivantes :</span><span class="sxs-lookup"><span data-stu-id="76be9-159">The versions should be:</span></span>
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="76be9-160">Pour installer et vérifier les correctifs logiciels en mode Maintenance</span><span class="sxs-lookup"><span data-stu-id="76be9-160">To install and verify maintenance mode hotfixes</span></span>

<span data-ttu-id="76be9-161">Utilisez l’article KB4037263 pour installer les mises à jour du microprogramme de disque.</span><span class="sxs-lookup"><span data-stu-id="76be9-161">Use KB4037263 to install disk firmware updates.</span></span> <span data-ttu-id="76be9-162">Ces mises à jour, qui entraînent des perturbations, nécessitent environ 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="76be9-162">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="76be9-163">Vous pouvez choisir de les installer dans une fenêtre de maintenance planifiée en vous connectant à la console série du périphérique.</span><span class="sxs-lookup"><span data-stu-id="76be9-163">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

> [!NOTE] 
> <span data-ttu-id="76be9-164">Si votre microprogramme de disque est déjà à jour, vous n’aurez pas à installer ces mises à jour.</span><span class="sxs-lookup"><span data-stu-id="76be9-164">If your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="76be9-165">Exécutez l’applet de commande `Get-HcsUpdateAvailability` à partir de la console série de l’appareil pour vérifier si des mises à jour sont disponibles et si elles risquent de provoquer une interruption de service (mode maintenance) ou non (mode normal).</span><span class="sxs-lookup"><span data-stu-id="76be9-165">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="76be9-166">Pour installer les mises à jour du microprogramme de disque, suivez les instructions ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="76be9-166">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="76be9-167">Mettez l’appareil en mode maintenance.</span><span class="sxs-lookup"><span data-stu-id="76be9-167">Place the device in the maintenance mode.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="76be9-168">N’utilisez pas l’accès distant Windows PowerShell quand vous vous connectez à un appareil en mode maintenance.</span><span class="sxs-lookup"><span data-stu-id="76be9-168">Do not use Windows PowerShell remoting when connecting to a device in maintenance mode.</span></span> <span data-ttu-id="76be9-169">À la place, exécutez cette applet de commande sur le contrôleur de l’appareil si vous êtes connecté par le biais de la console série de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="76be9-169">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span>

    <span data-ttu-id="76be9-170">Pour mettre le contrôleur en mode maintenance, tapez :</span><span class="sxs-lookup"><span data-stu-id="76be9-170">To place the controller in maintenance mode, type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="76be9-171">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="76be9-171">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="76be9-172">Les deux contrôleurs redémarrent alors en mode maintenance.</span><span class="sxs-lookup"><span data-stu-id="76be9-172">Both the controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="76be9-173">Pour installer la mise à jour du microprogramme de disque, tapez :</span><span class="sxs-lookup"><span data-stu-id="76be9-173">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="76be9-174">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="76be9-174">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="76be9-175">Surveillez la progression de l’installation à l’aide de la commande `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="76be9-175">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="76be9-176">La mise à jour est terminée quand `RunInProgress` passe à `False`.</span><span class="sxs-lookup"><span data-stu-id="76be9-176">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="76be9-177">Une fois l’installation terminée, le contrôleur sur lequel le correctif logiciel en mode Maintenance a été installé redémarre.</span><span class="sxs-lookup"><span data-stu-id="76be9-177">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="76be9-178">Connectez-vous avec l’option 1 (accès total) et vérifiez la version du microprogramme de disque.</span><span class="sxs-lookup"><span data-stu-id="76be9-178">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="76be9-179">Entrez :</span><span class="sxs-lookup"><span data-stu-id="76be9-179">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="76be9-180">Les versions attendues du microprogramme de disque sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="76be9-180">The expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   <span data-ttu-id="76be9-181">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="76be9-181">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17845
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
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
   
    <span data-ttu-id="76be9-182">Exécutez la commande `Get-HcsFirmwareVersion` sur le deuxième contrôleur pour vérifier que la version du logiciel a été mise à jour.</span><span class="sxs-lookup"><span data-stu-id="76be9-182">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="76be9-183">Vous pouvez à présent quitter le mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="76be9-183">You can then exit the maintenance mode.</span></span> <span data-ttu-id="76be9-184">Pour ce faire, tapez la commande suivante pour chaque contrôleur d’appareil :</span><span class="sxs-lookup"><span data-stu-id="76be9-184">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="76be9-185">Les contrôleurs redémarrent quand vous quittez le mode maintenance.</span><span class="sxs-lookup"><span data-stu-id="76be9-185">The controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="76be9-186">Une fois que les mises à jour du microprogramme de disque ont été appliquées avec succès et que l’appareil a quitté le mode maintenance, revenez au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="76be9-186">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure portal.</span></span> <span data-ttu-id="76be9-187">Remarque : il se peut que le portail n’affiche pas les mises à jour installées en mode maintenance pendant 24 heures.</span><span class="sxs-lookup"><span data-stu-id="76be9-187">Note that the portal might not show that you installed the maintenance mode updates for 24 hours.</span></span>

