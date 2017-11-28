<!--author=SharS last changed: 02/22/16-->

### <a name="to-configure-and-register-the-device"></a><span data-ttu-id="b08a0-101">Configuration et inscription de l’appareil</span><span class="sxs-lookup"><span data-stu-id="b08a0-101">To configure and register the device</span></span>
1. <span data-ttu-id="b08a0-102">Accédez à l’interface Windows PowerShell sur la console série de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b08a0-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="b08a0-103">Consultez la page [Utilisation de PuTTY pour se connecter à la console en série de l’appareil](#use-putty-to-connect-to-the-device-serial-console) pour obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="b08a0-103">See [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="b08a0-104">**Veillez à suivre la procédure pas à pas, sans quoi vous ne pourrez pas accéder à la console.**</span><span class="sxs-lookup"><span data-stu-id="b08a0-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span></span>
2. <span data-ttu-id="b08a0-105">Dans la session qui s’ouvre, appuyez une fois sur Entrée pour lancer une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="b08a0-105">In the session that opens up, press Enter one time to get a command prompt.</span></span> 
3. <span data-ttu-id="b08a0-106">Vous devez choisir la langue que vous souhaitez définir pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="b08a0-106">You will be prompted to choose the language that you would like to set for your device.</span></span> <span data-ttu-id="b08a0-107">Spécifiez la langue, puis appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="b08a0-107">Specify the language, and then press Enter.</span></span> 
   
    ![Configuration et inscription de l’appareil StorSimple 1](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="b08a0-109">Dans le menu de console en série qui s’affiche, choisissez l’option 1 pour ouvrir une session offrant un accès complet.</span><span class="sxs-lookup"><span data-stu-id="b08a0-109">In the serial console menu that is presented, choose option 1 to log on with full access.</span></span> 
   
    ![Inscription de l’appareil StorSimple 2](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="b08a0-111">Procédez comme suit pour configurer les paramètres réseau minimum requis pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="b08a0-111">Perform the following steps to configure the minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="b08a0-112">Ces étapes de configuration doivent être effectuées sur le contrôleur actif de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="b08a0-112">These configuration steps need to be performed on the active controller of the device.</span></span> <span data-ttu-id="b08a0-113">Le menu de la console en série indique l’état du contrôleur dans le message de bannière.</span><span class="sxs-lookup"><span data-stu-id="b08a0-113">The serial console menu indicates the controller state in the banner message.</span></span> <span data-ttu-id="b08a0-114">Si vous n’êtes pas connecté au contrôleur actif, déconnectez-vous, puis connectez-vous à ce contrôleur.</span><span class="sxs-lookup"><span data-stu-id="b08a0-114">If you are not connect to the active controller, disconnect and then connect to the active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="b08a0-115">À l’invite de commandes, tapez votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="b08a0-115">At the command prompt, type your password.</span></span> <span data-ttu-id="b08a0-116">Le mot de passe par défaut de l’appareil est **Password1**.</span><span class="sxs-lookup"><span data-stu-id="b08a0-116">The default device password is **Password1**.</span></span>
   2. <span data-ttu-id="b08a0-117">Tapez la commande suivante : </span><span class="sxs-lookup"><span data-stu-id="b08a0-117">Type the following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="b08a0-118">Un Assistant Installation s’affiche pour vous aider à configurer les paramètres réseau de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="b08a0-118">A setup wizard will appear to help you configure the network settings for the device.</span></span> <span data-ttu-id="b08a0-119">Fournissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b08a0-119">Supply the following information:</span></span> 
      
      * <span data-ttu-id="b08a0-120">Adresse IP de l’interface réseau DATA 0</span><span class="sxs-lookup"><span data-stu-id="b08a0-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="b08a0-121">Masque de sous-réseau</span><span class="sxs-lookup"><span data-stu-id="b08a0-121">Subnet mask</span></span>
      * <span data-ttu-id="b08a0-122">Passerelle</span><span class="sxs-lookup"><span data-stu-id="b08a0-122">Gateway</span></span>
      * <span data-ttu-id="b08a0-123">Adresse IP du serveur DNS principal</span><span class="sxs-lookup"><span data-stu-id="b08a0-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="b08a0-124">Adresse IP du serveur NTP principal</span><span class="sxs-lookup"><span data-stu-id="b08a0-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="b08a0-125">Vous devrez peut-être attendre quelques minutes que les paramètres de masque de sous-réseau et de DNS soient appliqués.</span><span class="sxs-lookup"><span data-stu-id="b08a0-125">You may have to wait for a few minutes for the subnet mask and DNS settings to be applied.</span></span> 
      > 
      > 
   4. <span data-ttu-id="b08a0-126">Configurez éventuellement votre serveur proxy web.</span><span class="sxs-lookup"><span data-stu-id="b08a0-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="b08a0-127">Bien que la configuration du proxy web soit facultative, si vous en utilisez un, vous pouvez uniquement le configurer ici.</span><span class="sxs-lookup"><span data-stu-id="b08a0-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="b08a0-128">Pour plus d’informations, consultez la section [Configuration du proxy web pour votre appareil](../articles/storsimple/storsimple-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="b08a0-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span> 
      > 
      > 
6. <span data-ttu-id="b08a0-129">Appuyez sur Ctrl+C pour quitter l’Assistant Installation.</span><span class="sxs-lookup"><span data-stu-id="b08a0-129">Press Ctrl + C to exit the setup wizard.</span></span>
7. <span data-ttu-id="b08a0-130">Installez les mises à jour comme suit :</span><span class="sxs-lookup"><span data-stu-id="b08a0-130">Install the updates as follows:</span></span>
   
   1. <span data-ttu-id="b08a0-131">Pour définir les adresses IP sur les deux contrôleurs, utilisez l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b08a0-131">Use the following cmdlet to set IPs on both the controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="b08a0-132">À l’invite de commandes, exécutez `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="b08a0-132">At the command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="b08a0-133">Vous devez recevoir une notification indiquant que les mises à jour sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="b08a0-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="b08a0-134">Exécutez `Start-HcsUpdate`.</span><span class="sxs-lookup"><span data-stu-id="b08a0-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="b08a0-135">Vous pouvez exécuter cette commande sur n’importe quel nœud.</span><span class="sxs-lookup"><span data-stu-id="b08a0-135">You can run this command on any node.</span></span> <span data-ttu-id="b08a0-136">Les mises à jour sont appliquées sur le premier contrôleur, le contrôleur bascule, puis les mises à jour sont appliquées à l’autre contrôleur.</span><span class="sxs-lookup"><span data-stu-id="b08a0-136">Updates will be applied on the first controller, the controller will fail over, and then the updates will be applied on the other controller.</span></span>
      
      <span data-ttu-id="b08a0-137">Pour surveiller la progression de la mise à jour, exécutez `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="b08a0-137">You can monitor the progress of the update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="b08a0-138">L’exemple de sortie suivant indique que la mise à jour est en cours.</span><span class="sxs-lookup"><span data-stu-id="b08a0-138">The following sample output shows the update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   : 
      ````
      
      <span data-ttu-id="b08a0-139">L’exemple de sortie suivant indique que la mise à jour est terminée.</span><span class="sxs-lookup"><span data-stu-id="b08a0-139">The following sample output indicates that the update is finished.</span></span>
      
      ````
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      
      ````
      
      <span data-ttu-id="b08a0-140">L’application de toutes les mises à jour, y compris Windows Updates, peut prendre jusqu’à 11 heures.</span><span class="sxs-lookup"><span data-stu-id="b08a0-140">It may take up to 11 hours to apply all the updates, including the Windows Updates.</span></span>

8. <span data-ttu-id="b08a0-141">Une fois toutes les mises à jour installées, exécutez l’applet de commande suivante pour confirmer que les mises à jour logicielles ont été appliquées correctement :</span><span class="sxs-lookup"><span data-stu-id="b08a0-141">After all the updates are successfully installed, run the following cmdlet to confirm that the software updates were applied correctly:</span></span>
   
     `Get-HcsSystem`
   
    <span data-ttu-id="b08a0-142">Vous devez voir les versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="b08a0-142">You should see the following versions:</span></span>
   
   * <span data-ttu-id="b08a0-143">HcsSoftwareVersion : 6.3.9600.17491</span><span class="sxs-lookup"><span data-stu-id="b08a0-143">HcsSoftwareVersion: 6.3.9600.17491</span></span>
   * <span data-ttu-id="b08a0-144">CisAgentVersion : 1.0.9037.0</span><span class="sxs-lookup"><span data-stu-id="b08a0-144">CisAgentVersion: 1.0.9037.0</span></span>
   * <span data-ttu-id="b08a0-145">MdsAgentVersion : 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="b08a0-145">MdsAgentVersion: 26.0.4696.1433</span></span>
9. <span data-ttu-id="b08a0-146">Exécutez l’applet de commande suivante pour confirmer que la mise à jour du microprogramme a été appliquée correctement :</span><span class="sxs-lookup"><span data-stu-id="b08a0-146">Run the following cmdlet to confirm that the firmware update was applied correctly:</span></span>
   
    <span data-ttu-id="b08a0-147">`Start-HcsFirmwareCheck`.</span><span class="sxs-lookup"><span data-stu-id="b08a0-147">`Start-HcsFirmwareCheck`.</span></span>
   
     <span data-ttu-id="b08a0-148">L’état du microprogramme doit être **À jour**.</span><span class="sxs-lookup"><span data-stu-id="b08a0-148">The firmware status should be **UpToDate**.</span></span>
10. <span data-ttu-id="b08a0-149">Exécutez l’applet de commande suivante pour faire pointer l’appareil vers le portail Microsoft Azure Government (il pointe en effet vers le portail Azure Classic par défaut).</span><span class="sxs-lookup"><span data-stu-id="b08a0-149">Run the following cmdlet to point the device to the Microsoft Azure Government portal (because it points to the public Azure classic portal by default).</span></span> <span data-ttu-id="b08a0-150">Les deux contrôleurs redémarrent.</span><span class="sxs-lookup"><span data-stu-id="b08a0-150">This will restart both controllers.</span></span> <span data-ttu-id="b08a0-151">Nous vous recommandons d’utiliser deux sessions PuTTY pour vous connecter simultanément aux deux contrôleurs afin de voir quand chacun d’eux est redémarré.</span><span class="sxs-lookup"><span data-stu-id="b08a0-151">We recommend that you use two PuTTY sessions to simultaneously connect to both controllers so that you can see when each controller is restarted.</span></span>
    
     `Set-CloudPlatform -AzureGovt_US`
    
    <span data-ttu-id="b08a0-152">Un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b08a0-152">You will see a confirmation message.</span></span> <span data-ttu-id="b08a0-153">Acceptez la valeur par défaut (**Y**).</span><span class="sxs-lookup"><span data-stu-id="b08a0-153">Accept the default (**Y**).</span></span>
11. <span data-ttu-id="b08a0-154">Exécutez l’applet de commande suivante pour reprendre l’installation :</span><span class="sxs-lookup"><span data-stu-id="b08a0-154">Run the following cmdlet to resume setup:</span></span>
    
     `Invoke-HcsSetupWizard`
    
     ![Reprise de l’Assistant Installation](./media/storsimple-configure-and-register-device-gov/HCS_ResumeSetup-gov-include.png)
    
    <span data-ttu-id="b08a0-156">Lorsque vous reprenez l’installation, l’Assistant a la version Update 1 (qui correspond à la version 17469).</span><span class="sxs-lookup"><span data-stu-id="b08a0-156">When you resume setup, the wizard will be the Update 1 version (which corresponds to version 17469).</span></span> 
12. <span data-ttu-id="b08a0-157">Acceptez les paramètres réseau.</span><span class="sxs-lookup"><span data-stu-id="b08a0-157">Accept the network settings.</span></span> <span data-ttu-id="b08a0-158">Un message de validation apparaît lorsque vous acceptez un paramètre.</span><span class="sxs-lookup"><span data-stu-id="b08a0-158">You will see a validation message after you accept each setting.</span></span>
13. <span data-ttu-id="b08a0-159">Pour des raisons de sécurité, le mot de passe administrateur de l’appareil expire après la première session, et vous devez le modifier maintenant.</span><span class="sxs-lookup"><span data-stu-id="b08a0-159">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span></span> <span data-ttu-id="b08a0-160">Lorsque vous y êtes invité, fournissez un mot de passe administrateur de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="b08a0-160">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="b08a0-161">Un mot de passe administrateur d’appareil valide doit comprendre entre 8 et 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="b08a0-161">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="b08a0-162">Le mot de passe doit contenir trois des éléments suivants : caractères en minuscules, en majuscules, numériques et spéciaux.</span><span class="sxs-lookup"><span data-stu-id="b08a0-162">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![Inscription de l’appareil StorSimple 5](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice5_gov-include.png)
14. <span data-ttu-id="b08a0-164">La dernière étape de l’Assistant Installation inscrit votre appareil auprès du service StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="b08a0-164">The final step in the setup wizard registers your device with the StorSimple Manager service.</span></span> <span data-ttu-id="b08a0-165">Pour cela, vous avez besoin de la clé d’inscription de service que vous avez obtenue à [l’étape 2 : obtention de la clé d’inscription](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="b08a0-165">For this, you will need the service registration key that you obtained in [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="b08a0-166">Après avoir entré la clé d’inscription, vous devrez peut-être attendre 2 à 3 minutes avant que l’appareil ne soit inscrit.</span><span class="sxs-lookup"><span data-stu-id="b08a0-166">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b08a0-167">Vous pouvez appuyer sur Ctrl + C à tout moment pour quitter l’Assistant Installation.</span><span class="sxs-lookup"><span data-stu-id="b08a0-167">You can press Ctrl + C at any time to exit the setup wizard.</span></span> <span data-ttu-id="b08a0-168">Si vous avez entré tous les paramètres réseau (adresse IP pour Data 0, masque de sous-réseau et passerelle), vos entrées sont conservées.</span><span class="sxs-lookup"><span data-stu-id="b08a0-168">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![Progression de l’inscription de StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_RegistrationProgress-gov-include.png)
15. <span data-ttu-id="b08a0-170">Une fois l’appareil inscrit, une clé de chiffrement de données de service s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b08a0-170">After the device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="b08a0-171">Copiez-la et enregistrez-la en lieu sûr.</span><span class="sxs-lookup"><span data-stu-id="b08a0-171">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="b08a0-172">**Cette clé et la clé d’enregistrement de service sont requises pour l’inscription d’appareils supplémentaires avec le service StorSimple Manager.**</span><span class="sxs-lookup"><span data-stu-id="b08a0-172">**This key will be required with the service registration key to register additional devices with the StorSimple Manager service.**</span></span> <span data-ttu-id="b08a0-173">Reportez-vous à la section [Sécurité StorSimple](../articles/storsimple/storsimple-security.md) pour plus d’informations sur cette clé.</span><span class="sxs-lookup"><span data-stu-id="b08a0-173">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Inscription de l’appareil StorSimple 7](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="b08a0-175">Pour copier le texte à partir de la fenêtre de console de série, sélectionnez-le simplement.</span><span class="sxs-lookup"><span data-stu-id="b08a0-175">To copy the text from the serial console window, simply select the text.</span></span> <span data-ttu-id="b08a0-176">Vous devez ensuite pouvoir le coller dans le Presse-papiers ou dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="b08a0-176">You should then be able to paste it in the clipboard or any text editor.</span></span> 
    > 
    > <span data-ttu-id="b08a0-177">N’utilisez PAS Ctrl + C pour copier la clé de chiffrement de données de service.</span><span class="sxs-lookup"><span data-stu-id="b08a0-177">DO NOT use Ctrl + C to copy the service data encryption key.</span></span> <span data-ttu-id="b08a0-178">Cette combinaison de touches ferme l’Assistant Installation.</span><span class="sxs-lookup"><span data-stu-id="b08a0-178">Using Ctrl + C will cause you to exit the setup wizard.</span></span> <span data-ttu-id="b08a0-179">Par conséquent, le mot de passe administrateur de l’appareil n’est pas modifié et l’appareil rétablit le mot de passe par défaut.</span><span class="sxs-lookup"><span data-stu-id="b08a0-179">As a result, the device administrator password will not be changed and the device will revert to the default password.</span></span>
    > 
    > 
16. <span data-ttu-id="b08a0-180">Quittez la console en série.</span><span class="sxs-lookup"><span data-stu-id="b08a0-180">Exit the serial console.</span></span>
17. <span data-ttu-id="b08a0-181">Revenez au portail Azure Government et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b08a0-181">Return to the Azure Government Portal, and complete the following steps:</span></span>
    
    1. <span data-ttu-id="b08a0-182">Double-cliquez sur le service StorSimple Manager pour accéder à la page **Démarrage rapide** .</span><span class="sxs-lookup"><span data-stu-id="b08a0-182">Double-click your StorSimple Manager service to access the **Quick Start** page.</span></span>
    2. <span data-ttu-id="b08a0-183">Cliquez sur **Afficher les appareils connectés**.</span><span class="sxs-lookup"><span data-stu-id="b08a0-183">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="b08a0-184">Sur la page **Appareils** , vérifiez que l’appareil s’est bien connecté au service en vérifiant son état.</span><span class="sxs-lookup"><span data-stu-id="b08a0-184">On the **Devices** page, verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="b08a0-185">L’état de l’appareil doit être **En ligne**.</span><span class="sxs-lookup"><span data-stu-id="b08a0-185">The device status should be **Online**.</span></span>
       
        ![Page Appareils StorSimple](./media/storsimple-configure-and-register-device-gov/HCS_DeviceOnline-gov-include.png) 
       
        <span data-ttu-id="b08a0-187">Si l’état de l’appareil est **Hors ligne**, attendez quelques minutes qu’il soit en ligne.</span><span class="sxs-lookup"><span data-stu-id="b08a0-187">If the device status is **Offline**, wait for a couple of minutes for the device to come online.</span></span> 
       
        <span data-ttu-id="b08a0-188">Si l’appareil est toujours déconnecté après quelques minutes, vous devez vous assurer que votre réseau de pare-feu a été configuré comme décrit dans [Configuration réseau requise pour votre appareil StorSimple](../articles/storsimple/storsimple-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="b08a0-188">If the device is still offline after a few minutes, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span> 
       
        <span data-ttu-id="b08a0-189">Vérifiez que le port 9354 est ouvert pour la communication sortante, car le Service Bus l’utilise pour la communication entre le service StorSimple Manager et l’appareil.</span><span class="sxs-lookup"><span data-stu-id="b08a0-189">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Manager service-to-device communication.</span></span>

