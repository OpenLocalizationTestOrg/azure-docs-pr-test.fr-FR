<!--author=SharS last changed: 02/22/2016-->

### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="7e344-101">Appareil de hello tooconfigure et Registre</span><span class="sxs-lookup"><span data-stu-id="7e344-101">tooconfigure and register hello device</span></span>
1. <span data-ttu-id="7e344-102">Accéder à l’interface Windows PowerShell hello sur votre console série du périphérique StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7e344-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="7e344-103">Consultez [console série du périphérique toohello tooconnect utilisez PuTTY](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) pour obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="7e344-103">See [Use PuTTY tooconnect toohello device serial console](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="7e344-104">**Être procédure de hello toofollow vraiment exactement ou vous ne serez pas la console de hello tooaccess en mesure de.**</span><span class="sxs-lookup"><span data-stu-id="7e344-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>
2. <span data-ttu-id="7e344-105">Dans la session hello qui s’ouvre, appuyez sur entrée une fois tooget une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="7e344-105">In hello session that opens up, press Enter one time tooget a command prompt.</span></span>
3. <span data-ttu-id="7e344-106">Vous seront demandées toochoose hello langage que tooset pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="7e344-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="7e344-107">Spécifier la langue de hello, puis appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="7e344-107">Specify hello language, and then press Enter.</span></span>
   
    ![Configuration et inscription de l’appareil StorSimple 1](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="7e344-109">Dans le menu de console série hello qui s’affiche, choisissez l’option 1 toolog sur avec un accès complet.</span><span class="sxs-lookup"><span data-stu-id="7e344-109">In hello serial console menu that is presented, choose option 1 toolog on with full access.</span></span>
   
    ![Inscription de l’appareil StorSimple 2](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="7e344-111">Effectuer hello suivant les paramètres de procédure tooconfigure hello réseau minimaux requis pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="7e344-111">Perform hello following steps tooconfigure hello minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="7e344-112">Ces étapes de configuration doivent toobe effectuée sur le contrôleur actif de hello du périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="7e344-112">These configuration steps need toobe performed on hello active controller of hello device.</span></span> <span data-ttu-id="7e344-113">menu de console série Hello indique l’état du contrôleur hello dans message de bannière hello.</span><span class="sxs-lookup"><span data-stu-id="7e344-113">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="7e344-114">Si vous ne sont pas connecter contrôleur actif de toohello, se déconnecter, puis connectez contrôleur actif de toohello.</span><span class="sxs-lookup"><span data-stu-id="7e344-114">If you are not connect toohello active controller, disconnect and then connect toohello active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="7e344-115">À l’invite de commandes hello, tapez votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7e344-115">At hello command prompt, type your password.</span></span> <span data-ttu-id="7e344-116">mot de passe par défaut Hello est **Password1**.</span><span class="sxs-lookup"><span data-stu-id="7e344-116">hello default device password is **Password1**.</span></span>
   2. <span data-ttu-id="7e344-117">Tapez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7e344-117">Type hello following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="7e344-118">Un Assistant d’installation s’affiche toohelp configurer les paramètres de réseau hello pour appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="7e344-118">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="7e344-119">Fournissez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="7e344-119">Supply hello following information:</span></span>
      
      * <span data-ttu-id="7e344-120">Adresse IP de l’interface réseau DATA 0</span><span class="sxs-lookup"><span data-stu-id="7e344-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="7e344-121">Masque de sous-réseau</span><span class="sxs-lookup"><span data-stu-id="7e344-121">Subnet mask</span></span>
      * <span data-ttu-id="7e344-122">Passerelle</span><span class="sxs-lookup"><span data-stu-id="7e344-122">Gateway</span></span>
      * <span data-ttu-id="7e344-123">Adresse IP du serveur DNS principal</span><span class="sxs-lookup"><span data-stu-id="7e344-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="7e344-124">Adresse IP du serveur NTP principal</span><span class="sxs-lookup"><span data-stu-id="7e344-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="7e344-125">Vous avez peut-être toowait pendant quelques minutes pour le masque de sous-réseau hello et toobe de paramètres DNS appliqué.</span><span class="sxs-lookup"><span data-stu-id="7e344-125">You may have toowait for a few minutes for hello subnet mask and DNS settings toobe applied.</span></span>
      > 
      > 
   4. <span data-ttu-id="7e344-126">Configurez éventuellement votre serveur proxy web.</span><span class="sxs-lookup"><span data-stu-id="7e344-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="7e344-127">Bien que la configuration du proxy web soit facultative, si vous en utilisez un, vous pouvez uniquement le configurer ici.</span><span class="sxs-lookup"><span data-stu-id="7e344-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="7e344-128">Pour plus d’informations, consultez trop[configurer un proxy web pour votre appareil](../articles/storsimple/storsimple-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="7e344-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span>
      > 
      > 
6. <span data-ttu-id="7e344-129">Appuyez sur Ctrl + C Assistant d’installation tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="7e344-129">Press Ctrl + C tooexit hello setup wizard.</span></span>
7. <span data-ttu-id="7e344-130">Installez les mises à jour hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7e344-130">Install hello updates as follows:</span></span>
   
   1. <span data-ttu-id="7e344-131">Utilisez hello suivant tooset de l’applet de commande des adresses IP sur les deux contrôleurs hello :</span><span class="sxs-lookup"><span data-stu-id="7e344-131">Use hello following cmdlet tooset IPs on both hello controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="7e344-132">À l’invite de commandes hello, exécutez `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="7e344-132">At hello command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="7e344-133">Vous devez recevoir une notification indiquant que les mises à jour sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="7e344-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="7e344-134">Exécutez `Start-HcsUpdate`.</span><span class="sxs-lookup"><span data-stu-id="7e344-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="7e344-135">Vous pouvez exécuter cette commande sur n’importe quel nœud.</span><span class="sxs-lookup"><span data-stu-id="7e344-135">You can run this command on any node.</span></span> <span data-ttu-id="7e344-136">Les mises à jour seront appliquées sur le premier contrôleur de hello, hello contrôleur bascule et puis hello mises à jour seront appliquées sur hello autre contrôleur.</span><span class="sxs-lookup"><span data-stu-id="7e344-136">Updates will be applied on hello first controller, hello controller will fail over, and then hello updates will be applied on hello other controller.</span></span>
      
      <span data-ttu-id="7e344-137">Vous pouvez surveiller la progression hello de mise à jour hello en exécutant `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="7e344-137">You can monitor hello progress of hello update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="7e344-138">Hello résultat de l’exemple suivant illustre hello mise à jour en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7e344-138">hello following sample output shows hello update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      <span data-ttu-id="7e344-139">Hello suivant l’exemple de sortie indique que cette mise à jour hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="7e344-139">hello following sample output indicates that hello update is finished.</span></span>
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      <span data-ttu-id="7e344-140">Il peut prendre des heures too11 tooapply tous hello mises à jour, y compris hello mises à jour Windows.</span><span class="sxs-lookup"><span data-stu-id="7e344-140">It may take up too11 hours tooapply all hello updates, including hello Windows Updates.</span></span>
8. <span data-ttu-id="7e344-141">Exécutez hello suivant le portail de Microsoft Azure Government applet de commande toopoint hello appareils toohello (car elle pointe toohello portail classique Azure public par défaut).</span><span class="sxs-lookup"><span data-stu-id="7e344-141">Run hello following cmdlet toopoint hello device toohello Microsoft Azure Government portal (because it points toohello public Azure classic portal by default).</span></span> <span data-ttu-id="7e344-142">Les deux contrôleurs redémarrent.</span><span class="sxs-lookup"><span data-stu-id="7e344-142">This will restart both controllers.</span></span> <span data-ttu-id="7e344-143">Nous vous recommandons d’utiliser deux sessions PuTTY toosimultaneously connecter tooboth contrôleurs afin que vous puissiez voir quand chaque contrôleur est redémarré.</span><span class="sxs-lookup"><span data-stu-id="7e344-143">We recommend that you use two PuTTY sessions toosimultaneously connect tooboth controllers so that you can see when each controller is restarted.</span></span>
   
    `Set-CloudPlatform -AzureGovt_US`
   
   <span data-ttu-id="7e344-144">Un message de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7e344-144">You will see a confirmation message.</span></span> <span data-ttu-id="7e344-145">Accepter la valeur par défaut hello (**Y**).</span><span class="sxs-lookup"><span data-stu-id="7e344-145">Accept hello default (**Y**).</span></span>
9. <span data-ttu-id="7e344-146">Exécutez hello après l’installation de tooresume d’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="7e344-146">Run hello following cmdlet tooresume setup:</span></span>
   
    `Invoke-HcsSetupWizard`
   
    ![Reprise de l’Assistant Installation](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   <span data-ttu-id="7e344-148">Lorsque vous reprenez le programme d’installation, Assistant de hello sera la version de mise à jour 2 de hello.</span><span class="sxs-lookup"><span data-stu-id="7e344-148">When you resume setup, hello wizard will be hello Update 2 version.</span></span>
10. <span data-ttu-id="7e344-149">Acceptez les paramètres de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="7e344-149">Accept hello network settings.</span></span> <span data-ttu-id="7e344-150">Un message de validation apparaît lorsque vous acceptez un paramètre.</span><span class="sxs-lookup"><span data-stu-id="7e344-150">You will see a validation message after you accept each setting.</span></span>
11. <span data-ttu-id="7e344-151">Pour des raisons de sécurité, mot de passe administrateur hello appareil expire au bout de hello première session, et vous devrez toochange informatique maintenant.</span><span class="sxs-lookup"><span data-stu-id="7e344-151">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="7e344-152">Lorsque vous y êtes invité, fournissez un mot de passe administrateur de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="7e344-152">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="7e344-153">Un mot de passe administrateur d’appareil valide doit comprendre entre 8 et 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="7e344-153">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="7e344-154">Hello mot de passe doit contenir 3 des éléments suivants de hello : caractères en minuscules, majuscules, numériques et spéciaux.</span><span class="sxs-lookup"><span data-stu-id="7e344-154">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![Inscription de l’appareil StorSimple 5](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. <span data-ttu-id="7e344-156">étape finale de Hello dans l’Assistant Installation de hello inscrit votre appareil avec hello service StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="7e344-156">hello final step in hello setup wizard registers your device with hello StorSimple Manager service.</span></span> <span data-ttu-id="7e344-157">Pour ce faire, vous serez peut-être hello clé d’inscription de service que vous avez obtenue dans [étape 2 : clé d’inscription Get hello](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="7e344-157">For this, you will need hello service registration key that you obtained in [Step 2: Get hello service registration key](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="7e344-158">Une fois que vous fournissez la clé d’inscription de hello, vous devrez peut-être toowait 2-3 minutes avant l’inscription de périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="7e344-158">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="7e344-159">Vous pouvez appuyer sur Ctrl + C à n’importe quel Assistant Installation de temps tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="7e344-159">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="7e344-160">Si vous avez entré tous les paramètres de réseau hello (adresse IP de Data 0, masque de sous-réseau et passerelle), les entrées sont conservées.</span><span class="sxs-lookup"><span data-stu-id="7e344-160">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![Progression de l’inscription de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. <span data-ttu-id="7e344-162">Après l’inscription d’appareil de hello, une clé de chiffrement de données de Service s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7e344-162">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="7e344-163">Copiez-la et enregistrez-la en lieu sûr.</span><span class="sxs-lookup"><span data-stu-id="7e344-163">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="7e344-164">**Cette clé sera requise avec hello service d’inscription tooregister clé des unités supplémentaires dans hello service StorSimple Manager.**</span><span class="sxs-lookup"><span data-stu-id="7e344-164">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Manager service.**</span></span> <span data-ttu-id="7e344-165">Consultez trop[sécurité StorSimple](../articles/storsimple/storsimple-security.md) pour plus d’informations sur cette clé.</span><span class="sxs-lookup"><span data-stu-id="7e344-165">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Inscription de l’appareil StorSimple 7](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="7e344-167">texte hello de toocopy à partir de la fenêtre de console série hello, sélectionnez simplement le texte hello.</span><span class="sxs-lookup"><span data-stu-id="7e344-167">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="7e344-168">Vous devez maintenant être en mesure de toopaste dans le Presse-papiers de hello ou un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="7e344-168">You should then be able toopaste it in hello clipboard or any text editor.</span></span>
    > 
    > <span data-ttu-id="7e344-169">N’utilisez pas de Ctrl + C toocopy hello clé de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="7e344-169">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="7e344-170">À l’aide de Ctrl + C Assitant vous tooexit hello le programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="7e344-170">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="7e344-171">Par conséquent, mot de passe administrateur hello périphérique ne sera pas modifié et l’appareil hello seront rétablis toohello un mot de passe par défaut.</span><span class="sxs-lookup"><span data-stu-id="7e344-171">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    > 
    > 
14. <span data-ttu-id="7e344-172">Quittez la console série hello.</span><span class="sxs-lookup"><span data-stu-id="7e344-172">Exit hello serial console.</span></span>
15. <span data-ttu-id="7e344-173">Retournez toohello portail Azure du gouvernement et terminer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7e344-173">Return toohello Azure Government Portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="7e344-174">Double-cliquez sur votre hello tooaccess du service StorSimple Manager **Quick Start** page.</span><span class="sxs-lookup"><span data-stu-id="7e344-174">Double-click your StorSimple Manager service tooaccess hello **Quick Start** page.</span></span>
    2. <span data-ttu-id="7e344-175">Cliquez sur **Afficher les appareils connectés**.</span><span class="sxs-lookup"><span data-stu-id="7e344-175">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="7e344-176">Sur hello **périphériques** page, vérifiez que cet appareil hello toohello service connecté en vérifiant hello état.</span><span class="sxs-lookup"><span data-stu-id="7e344-176">On hello **Devices** page, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="7e344-177">état du périphérique Hello doit être **Online**.</span><span class="sxs-lookup"><span data-stu-id="7e344-177">hello device status should be **Online**.</span></span>
       
        ![Page Appareils StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        <span data-ttu-id="7e344-179">Si l’état du périphérique hello est **hors connexion**, attendez quelques minutes pour hello appareil toocome en ligne.</span><span class="sxs-lookup"><span data-stu-id="7e344-179">If hello device status is **Offline**, wait for a couple of minutes for hello device toocome online.</span></span>
       
        <span data-ttu-id="7e344-180">Si les appareils hello sont encore hors connexion après quelques minutes, vous devez toomake que votre réseau de pare-feu a été configuré comme décrit dans [configuration réseau requise pour votre appareil StorSimple](../articles/storsimple/storsimple-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="7e344-180">If hello device is still offline after a few minutes, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span>
       
        <span data-ttu-id="7e344-181">Vérifiez que le port 9354 est ouvert aux communications sortantes comme il est utilisé par bus de service hello pour la communication de Service-appareil StorSimple Manager.</span><span class="sxs-lookup"><span data-stu-id="7e344-181">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Manager Service-to-device communication.</span></span>

