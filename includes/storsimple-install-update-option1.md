<!--author=SharS last changed: 03/17/2016-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="8e946-101">Pour télécharger des correctifs logiciels</span><span class="sxs-lookup"><span data-stu-id="8e946-101">To download hotfixes</span></span>
<span data-ttu-id="8e946-102">Procédez comme suit pour télécharger la mise à jour logicielle.</span><span class="sxs-lookup"><span data-stu-id="8e946-102">Perform the following steps to download the software update.</span></span>

1. <span data-ttu-id="8e946-103">Démarrez Internet Explorer et accédez à [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="8e946-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="8e946-104">Si vous utilisez le catalogue Microsoft Update pour la première fois sur cet ordinateur, cliquez sur **Installer** lorsque vous êtes invité à installer le module complémentaire Catalogue Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="8e946-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="8e946-105">![Installer le catalogue](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="8e946-105">![Install catalog](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="8e946-106">Dans la zone de recherche du Catalogue Microsoft Update, entrez le numéro KB (Base de connaissances) du correctif que vous souhaitez télécharger, par exemple **3063418**, puis cliquez sur **Rechercher**.</span><span class="sxs-lookup"><span data-stu-id="8e946-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3063418**, and then click **Search**.</span></span>
4. <span data-ttu-id="8e946-107">L'offre groupée **StorSimple Update 1.2 Appliance Update** s'affiche.</span><span class="sxs-lookup"><span data-stu-id="8e946-107">You will see the **StorSimple Update 1.2 Appliance Update** bundle.</span></span> <span data-ttu-id="8e946-108">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8e946-108">Click **Add**.</span></span> <span data-ttu-id="8e946-109">La mise à jour est ajoutée au panier.</span><span class="sxs-lookup"><span data-stu-id="8e946-109">The update will be added to the basket.</span></span>
5. <span data-ttu-id="8e946-110">Recherchez les correctifs supplémentaires répertoriés dans le tableau ci-dessus (**3043005** et **3063416**) et ajoutez-les au panier.</span><span class="sxs-lookup"><span data-stu-id="8e946-110">Search for any additional hotfixes listed in the table above (**3043005** and **3063416**), and add each the basket.</span></span>
6. <span data-ttu-id="8e946-111">Cliquez sur **Afficher le panier**.</span><span class="sxs-lookup"><span data-stu-id="8e946-111">Click **View Basket**.</span></span>
   
    ![Afficher le panier](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. <span data-ttu-id="8e946-113">Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="8e946-113">Click **Download**.</span></span> <span data-ttu-id="8e946-114">Spécifiez ou **recherchez** l’emplacement local où vous voulez effectuer les téléchargements.</span><span class="sxs-lookup"><span data-stu-id="8e946-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="8e946-115">Les mises à jour sont téléchargées à l’emplacement spécifié et placées dans un sous-dossier portant le même nom que la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="8e946-115">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="8e946-116">Ce dossier peut également être copié sur un partage réseau accessible à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="8e946-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="8e946-117">Les correctifs doivent être accessibles depuis les deux contrôleurs pour détecter les messages d’erreur potentiels à partir du contrôleur homologue.</span><span class="sxs-lookup"><span data-stu-id="8e946-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="8e946-118">Pour installer et vérifier les correctifs logiciels en mode Normal</span><span class="sxs-lookup"><span data-stu-id="8e946-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="8e946-119">Procédez comme suit pour installer et vérifier les correctifs logiciels en mode Normal.</span><span class="sxs-lookup"><span data-stu-id="8e946-119">Perform the following steps to install and verify the regular-mode hotfixes.</span></span> <span data-ttu-id="8e946-120">Si vous les avez déjà installés à l’aide du portail Azure, passez directement à [Installer et vérifier les correctifs en mode maintenance](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="8e946-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="8e946-121">Pour installer la mise à jour logicielle, accédez à l’interface Windows PowerShell sur la console série de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8e946-121">To install the software update, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="8e946-122">Suivez les instructions détaillées de la section [Utilisation de PuTTY pour se connecter à la console série de l’appareil](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="8e946-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="8e946-123">À l'invite de commandes, appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="8e946-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="8e946-124">Sélectionnez **Option 1** pour vous connecter à l’appareil avec un accès complet.</span><span class="sxs-lookup"><span data-stu-id="8e946-124">Select **Option 1** to log on to the device with full access.</span></span>
3. <span data-ttu-id="8e946-125">Pour installer le package de mise à jour, à l’invite de commandes, tapez :</span><span class="sxs-lookup"><span data-stu-id="8e946-125">To install the update package, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="8e946-126">Utilisez IP au lieu de DNS dans le chemin d'accès du partage dans la commande ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="8e946-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="8e946-127">Le paramètre Informations d’identification n’est utilisé que si vous accédez à un partage authentifié.</span><span class="sxs-lookup"><span data-stu-id="8e946-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="8e946-128">Nous vous recommandons d'utiliser le paramètre d'informations d'identification pour accéder aux partages.</span><span class="sxs-lookup"><span data-stu-id="8e946-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="8e946-129">Même les partages qui sont ouverts à « tout le monde » ne sont généralement pas ouverts aux utilisateurs non authentifiés.</span><span class="sxs-lookup"><span data-stu-id="8e946-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="8e946-130">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="8e946-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="8e946-131">Tapez **Y** lorsque vous êtes invité à confirmer l’installation du correctif.</span><span class="sxs-lookup"><span data-stu-id="8e946-131">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="8e946-132">Contrôlez la mise à jour à l'aide de l'applet de commande `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="8e946-132">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="8e946-133">L’exemple de sortie suivant indique que la mise à jour est en cours.</span><span class="sxs-lookup"><span data-stu-id="8e946-133">The following sample output shows the update in progress.</span></span> <span data-ttu-id="8e946-134">`RunInprogress` a la valeur `True` lorsque la mise à jour est en cours.</span><span class="sxs-lookup"><span data-stu-id="8e946-134">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="8e946-135">L’exemple de sortie suivant indique que la mise à jour est terminée.</span><span class="sxs-lookup"><span data-stu-id="8e946-135">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="8e946-136">`RunInProgress` a la valeur `False` lorsque la mise à jour est terminée.</span><span class="sxs-lookup"><span data-stu-id="8e946-136">The `RunInProgress` will be `False` when the update has completed.</span></span>

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="8e946-137">Parfois, l'applet de commande indique `False` lorsque la mise à jour est encore en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="8e946-137">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="8e946-138">Pour vous assurer que le correctif logiciel est terminé, patientez quelques minutes, exécutez à nouveau cette commande et vérifiez que `RunInProgress` est `False`.</span><span class="sxs-lookup"><span data-stu-id="8e946-138">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="8e946-139">Dans ce cas, le correctif est terminé.</span><span class="sxs-lookup"><span data-stu-id="8e946-139">If it is, then the hotfix has completed.</span></span>
   > 
   > 
6. <span data-ttu-id="8e946-140">Lorsque la mise à jour logicielle est terminée, vérifiez les versions des logiciels du système.</span><span class="sxs-lookup"><span data-stu-id="8e946-140">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="8e946-141">Tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8e946-141">Type the following command:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="8e946-142">Vous devez voir les versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="8e946-142">You should see the following versions:</span></span>
   
   * <span data-ttu-id="8e946-143">HcsSoftwareVersion : 6.3.9600.17584</span><span class="sxs-lookup"><span data-stu-id="8e946-143">HcsSoftwareVersion: 6.3.9600.17584</span></span>
   * <span data-ttu-id="8e946-144">CisAgentVersion : 1.0.9049.0</span><span class="sxs-lookup"><span data-stu-id="8e946-144">CisAgentVersion: 1.0.9049.0</span></span>
   * <span data-ttu-id="8e946-145">MdsAgentVersion : 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="8e946-145">MdsAgentVersion: 26.0.4696.1433</span></span>
     
     <span data-ttu-id="8e946-146">Si les numéros de version ne changent pas après la mise à jour, cela indique que le correctif n'a pas pu s'appliquer.</span><span class="sxs-lookup"><span data-stu-id="8e946-146">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="8e946-147">Dans ce cas, contactez le [Support Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) pour obtenir une assistance supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="8e946-147">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
7. <span data-ttu-id="8e946-148">Répétez les étapes 3 à 5 pour installer le correctif logiciel restant en mode Normal (KB3043005).</span><span class="sxs-lookup"><span data-stu-id="8e946-148">Repeat steps 3-5 to install the remaining regular-mode hotfix (KB3043005).</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="8e946-149">Pour installer et vérifier les correctifs logiciels en mode Maintenance</span><span class="sxs-lookup"><span data-stu-id="8e946-149">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="8e946-150">Utilisez l’article KB3063416 pour installer les mises à jour du microprogramme de disque.</span><span class="sxs-lookup"><span data-stu-id="8e946-150">Use KB3063416 to install disk firmware updates.</span></span> <span data-ttu-id="8e946-151">Ces mises à jour, qui entraînent des perturbations, nécessitent environ 30 à 45 minutes.</span><span class="sxs-lookup"><span data-stu-id="8e946-151">These are disruptive updates and take around 30-45 minutes to complete.</span></span> <span data-ttu-id="8e946-152">Vous pouvez choisir de les installer dans une fenêtre de maintenance planifiée en vous connectant à la console série du périphérique.</span><span class="sxs-lookup"><span data-stu-id="8e946-152">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="8e946-153">Pour installer les mises à jour du microprogramme de disque, suivez les instructions ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8e946-153">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="8e946-154">Mettez l’appareil en mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="8e946-154">Place the device in Maintenance mode.</span></span> <span data-ttu-id="8e946-155">Notez que vous ne devez pas utiliser l’accès distant Windows PowerShell quand vous vous connectez à un appareil en mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="8e946-155">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="8e946-156">Vous devez exécuter cette applet de commande sur le contrôleur de l’appareil si vous êtes connecté par le biais de la console série de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="8e946-156">You will need to run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="8e946-157">Entrez :</span><span class="sxs-lookup"><span data-stu-id="8e946-157">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="8e946-158">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="8e946-158">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="8e946-159">Les deux contrôleurs redémarrent alors en mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="8e946-159">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="8e946-160">Pour installer la mise à jour du microprogramme de disque, tapez :</span><span class="sxs-lookup"><span data-stu-id="8e946-160">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="8e946-161">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="8e946-161">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="8e946-162">Surveillez la progression de l’installation à l’aide de la commande `Get-HcsUpdateStatus` .</span><span class="sxs-lookup"><span data-stu-id="8e946-162">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="8e946-163">La mise à jour est terminée quand `RunInProgress` passe à `False`.</span><span class="sxs-lookup"><span data-stu-id="8e946-163">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="8e946-164">Une fois l’installation terminée, le contrôleur sur lequel le correctif logiciel en mode Maintenance a été installé est redémarré.</span><span class="sxs-lookup"><span data-stu-id="8e946-164">After the installation is complete, the controller on which the maintenance mode hotfix was installed will be rebooted.</span></span> <span data-ttu-id="8e946-165">Connectez-vous avec l’option 1 (accès total) et vérifiez la version du microprogramme de disque.</span><span class="sxs-lookup"><span data-stu-id="8e946-165">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="8e946-166">Entrez :</span><span class="sxs-lookup"><span data-stu-id="8e946-166">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="8e946-167">Les versions attendues du microprogramme de disque sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="8e946-167">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   <span data-ttu-id="8e946-168">Exécutez la commande `Get-HcsFirmwareVersion` sur le deuxième contrôleur pour vérifier que la version du logiciel a été mise à jour.</span><span class="sxs-lookup"><span data-stu-id="8e946-168">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="8e946-169">Vous pouvez à présent quitter le mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="8e946-169">You can then exit the maintenance mode.</span></span> <span data-ttu-id="8e946-170">Tapez la commande suivante pour chaque contrôleur d’appareil :</span><span class="sxs-lookup"><span data-stu-id="8e946-170">Type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="8e946-171">Les contrôleurs redémarrent quand vous quittez le mode Maintenance.</span><span class="sxs-lookup"><span data-stu-id="8e946-171">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="8e946-172">Une fois que les mises à jour du microprogramme de disque ont été appliquées avec succès et que l’appareil a quitté le mode Maintenance, revenez au portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="8e946-172">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="8e946-173">Remarque : il se peut que le portail n’affiche pas les mises à jour installées en mode Maintenance pendant 24 heures.</span><span class="sxs-lookup"><span data-stu-id="8e946-173">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

