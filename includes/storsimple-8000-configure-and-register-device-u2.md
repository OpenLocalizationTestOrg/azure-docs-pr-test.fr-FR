<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="ce933-101">Appareil de hello tooconfigure et Registre</span><span class="sxs-lookup"><span data-stu-id="ce933-101">tooconfigure and register hello device</span></span>

1. <span data-ttu-id="ce933-102">Accéder à l’interface Windows PowerShell hello sur votre console série du périphérique StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ce933-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="ce933-103">Consultez [console série du périphérique toohello tooconnect utilisez PuTTY](#use-putty-to-connect-to-the-device-serial-console) pour obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="ce933-103">See [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="ce933-104">**Être procédure de hello toofollow vraiment exactement ou vous ne serez pas la console de hello tooaccess en mesure de.**</span><span class="sxs-lookup"><span data-stu-id="ce933-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>

2. <span data-ttu-id="ce933-105">Dans la session hello qui s’ouvre, appuyez sur **entrée** un temps tooget une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="ce933-105">In hello session that opens up, press **Enter** one time tooget a command prompt.</span></span>

3. <span data-ttu-id="ce933-106">Vous seront demandées toochoose hello langage que tooset pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="ce933-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="ce933-107">Spécifiez la langue de hello, puis appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="ce933-107">Specify hello language, and then press **Enter**.</span></span>

4. <span data-ttu-id="ce933-108">Dans le menu de console série hello qui s’affiche, sélectionnez l’option 1 trop**connecter avec un accès complet**.</span><span class="sxs-lookup"><span data-stu-id="ce933-108">In hello serial console menu that is presented, choose option 1 too**log in with full access**.</span></span>
     <span data-ttu-id="ce933-109">Complétez les paramètres de configuration réseau requise minimale de hello de tooconfigure étapes 5 à 12 pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="ce933-109">Complete steps 5-12 tooconfigure hello minimum required network settings for your device.</span></span> <span data-ttu-id="ce933-110">**Ces étapes de configuration doivent toobe effectuée sur le contrôleur actif de hello du périphérique de hello.**</span><span class="sxs-lookup"><span data-stu-id="ce933-110">**These configuration steps need toobe performed on hello active controller of hello device.**</span></span> <span data-ttu-id="ce933-111">menu de console série Hello indique l’état du contrôleur hello dans message de bannière hello.</span><span class="sxs-lookup"><span data-stu-id="ce933-111">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="ce933-112">Si vous n’êtes pas connecté toohello de contrôleur actif, vous déconnecter, puis connectez contrôleur actif de toohello.</span><span class="sxs-lookup"><span data-stu-id="ce933-112">If you are not connected toohello active controller, disconnect and then connect toohello active controller.</span></span>

5. <span data-ttu-id="ce933-113">À l’invite de commandes hello, tapez votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ce933-113">At hello command prompt, type your password.</span></span> <span data-ttu-id="ce933-114">mot de passe par défaut Hello est **Password1**.</span><span class="sxs-lookup"><span data-stu-id="ce933-114">hello default device password is **Password1**.</span></span>

6. <span data-ttu-id="ce933-115">Hello type commande suivante : `Invoke-HcsSetupWizard`.</span><span class="sxs-lookup"><span data-stu-id="ce933-115">Type hello following command: `Invoke-HcsSetupWizard`.</span></span>

7. <span data-ttu-id="ce933-116">Un Assistant d’installation s’affiche toohelp configurer les paramètres de réseau hello pour appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="ce933-116">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="ce933-117">Fournissez hello hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ce933-117">Supply hello hello following information:</span></span>
   
   * <span data-ttu-id="ce933-118">Adresse IP pour hello interface réseau DATA 0</span><span class="sxs-lookup"><span data-stu-id="ce933-118">IP address for hello DATA 0 network interface</span></span>
   * <span data-ttu-id="ce933-119">Masque de sous-réseau</span><span class="sxs-lookup"><span data-stu-id="ce933-119">Subnet mask</span></span>
   * <span data-ttu-id="ce933-120">Passerelle</span><span class="sxs-lookup"><span data-stu-id="ce933-120">Gateway</span></span>
   * <span data-ttu-id="ce933-121">Adresse IP du serveur DNS principal</span><span class="sxs-lookup"><span data-stu-id="ce933-121">IP address for Primary DNS server</span></span>

   <span data-ttu-id="ce933-122">Un exemple de sortie est présenté ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ce933-122">A sample output is presented below.</span></span>

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Active
        ---------------------------------------------------------------

        Your device needs toobe registered with hello Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' tooset up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like tooconfigure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    <span data-ttu-id="ce933-123">Bonjour précédant le résultat de l’exemple, vous pouvez voir que le système de hello est validation des paramètres de réseau après chaque étape dans le processus de hello.</span><span class="sxs-lookup"><span data-stu-id="ce933-123">In hello preceding sample output, you can see that hello system is validating network settings after each step in hello process.</span></span>

     > [!NOTE]
     > <span data-ttu-id="ce933-124">Vous avez peut-être toowait pendant quelques minutes pour le masque de sous-réseau hello et hello DNS paramètres toobe appliqué.</span><span class="sxs-lookup"><span data-stu-id="ce933-124">You may have toowait for a few minutes for hello subnet mask and hello DNS settings toobe applied.</span></span> <span data-ttu-id="ce933-125">Si vous obtenez un message d’erreur « Vérification hello réseau connectivité tooData 0 », vérifiez la connexion de réseau physique hello sur hello interface réseau DATA 0 de votre contrôleur actif.</span><span class="sxs-lookup"><span data-stu-id="ce933-125">If you get a "Check hello network connectivity tooData 0" error message, check hello physical network connection on hello DATA 0 network interface of your active controller.</span></span>

8. <span data-ttu-id="ce933-126">(Facultatif) Configurez votre serveur proxy web.</span><span class="sxs-lookup"><span data-stu-id="ce933-126">(Optional) configure your web proxy server.</span></span> <span data-ttu-id="ce933-127">Bien que la configuration du proxy web soit facultative, **si vous en utilisez un, vous pouvez uniquement le configurer ici**.</span><span class="sxs-lookup"><span data-stu-id="ce933-127">Although web proxy configuration is optional, **be aware that if you use a web proxy, you can only configure it here**.</span></span> <span data-ttu-id="ce933-128">Pour plus d’informations, consultez trop[configurer un proxy web pour votre appareil](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="ce933-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span></span>
9. <span data-ttu-id="ce933-129">Configurez un serveur NTP principal pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="ce933-129">Configure a Primary NTP server for your device.</span></span> <span data-ttu-id="ce933-130">Les serveurs NTP sont requis. En effet, votre appareil doit synchroniser les heures pour pouvoir s’authentifier auprès de vos fournisseurs de services cloud.</span><span class="sxs-lookup"><span data-stu-id="ce933-130">NTP servers are required, as your device must synchronize time so that it can authenticate with your cloud service providers.</span></span> <span data-ttu-id="ce933-131">Vérifiez que votre réseau permet toopass de trafic NTP à partir de votre toohello de centre de données Internet.</span><span class="sxs-lookup"><span data-stu-id="ce933-131">Ensure that your network allows NTP traffic toopass from your datacenter toohello Internet.</span></span> <span data-ttu-id="ce933-132">Si ce n’est pas possible, spécifiez un serveur NTP interne.</span><span class="sxs-lookup"><span data-stu-id="ce933-132">If this is not possible, specify an internal NTP server.</span></span>

    <span data-ttu-id="ce933-133">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="ce933-133">A sample output is shown below.</span></span>

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. <span data-ttu-id="ce933-134">Pour des raisons de sécurité, mot de passe administrateur hello appareil expire au bout de hello première session, et vous devrez toochange informatique maintenant.</span><span class="sxs-lookup"><span data-stu-id="ce933-134">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="ce933-135">Lorsque vous y êtes invité, fournissez un mot de passe administrateur de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="ce933-135">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="ce933-136">Un mot de passe administrateur d’appareil valide doit comprendre entre 8 et 15 caractères.</span><span class="sxs-lookup"><span data-stu-id="ce933-136">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="ce933-137">Hello mot de passe doit contenir 3 des éléments suivants de hello : caractères en minuscules, majuscules, numériques et spéciaux.</span><span class="sxs-lookup"><span data-stu-id="ce933-137">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. <span data-ttu-id="ce933-138">étape finale de Hello dans l’Assistant Installation de hello inscrit votre appareil avec hello service du Gestionnaire de périphériques StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ce933-138">hello final step in hello setup wizard registers your device with hello StorSimple Device Manager service.</span></span> <span data-ttu-id="ce933-139">Pour ce faire, vous devez hello clé d’inscription que vous avez obtenue à l’étape 2.</span><span class="sxs-lookup"><span data-stu-id="ce933-139">For this, you will need hello service registration key that you obtained in step 2.</span></span> <span data-ttu-id="ce933-140">Une fois que vous fournissez la clé d’inscription de hello, vous devrez peut-être toowait 2-3 minutes avant l’inscription de périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="ce933-140">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ce933-141">Vous pouvez appuyer sur Ctrl + C à n’importe quel Assistant Installation de temps tooexit hello.</span><span class="sxs-lookup"><span data-stu-id="ce933-141">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="ce933-142">Si vous avez entré tous les paramètres de réseau hello (adresse IP de Data 0, masque de sous-réseau et passerelle), les entrées sont conservées.</span><span class="sxs-lookup"><span data-stu-id="ce933-142">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    
    <span data-ttu-id="ce933-143">Voici un exemple de sortie obtenue.</span><span class="sxs-lookup"><span data-stu-id="ce933-143">A sample output is shown below.</span></span>

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. <span data-ttu-id="ce933-144">Après l’inscription d’appareil de hello, une clé de chiffrement de données de Service s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ce933-144">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="ce933-145">Copiez-la et enregistrez-la en lieu sûr.</span><span class="sxs-lookup"><span data-stu-id="ce933-145">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="ce933-146">**Cette clé sera requise avec hello service d’inscription tooregister clé des unités supplémentaires dans hello service du Gestionnaire de périphériques StorSimple.**</span><span class="sxs-lookup"><span data-stu-id="ce933-146">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Device Manager service.**</span></span> <span data-ttu-id="ce933-147">Consultez trop[sécurité StorSimple](../articles/storsimple/storsimple-security.md) pour plus d’informations sur cette clé.</span><span class="sxs-lookup"><span data-stu-id="ce933-147">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![Inscription de l’appareil StorSimple 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > <span data-ttu-id="ce933-149">texte hello de toocopy à partir de la fenêtre de console série hello, sélectionnez simplement le texte hello.</span><span class="sxs-lookup"><span data-stu-id="ce933-149">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="ce933-150">Vous devez maintenant être en mesure de toopaste dans le Presse-papiers de hello ou un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="ce933-150">You should then be able toopaste it in hello clipboard or any text editor.</span></span> <span data-ttu-id="ce933-151">N’utilisez pas de Ctrl + C toocopy hello clé de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="ce933-151">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="ce933-152">À l’aide de Ctrl + C Assitant vous tooexit hello le programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="ce933-152">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="ce933-153">Par conséquent, mot de passe administrateur hello périphérique ne sera pas modifié et l’appareil hello seront rétablis toohello un mot de passe par défaut.</span><span class="sxs-lookup"><span data-stu-id="ce933-153">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    
13. <span data-ttu-id="ce933-154">Quittez la console série hello.</span><span class="sxs-lookup"><span data-stu-id="ce933-154">Exit hello serial console.</span></span>
14. <span data-ttu-id="ce933-155">Retour toohello portail Azure et hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="ce933-155">Return toohello Azure portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="ce933-156">Atteindre le service du Gestionnaire de périphériques StorSimple tooyour.</span><span class="sxs-lookup"><span data-stu-id="ce933-156">Go tooyour StorSimple Device Manager service.</span></span>
    2. <span data-ttu-id="ce933-157">Cliquez sur **Appareils**.</span><span class="sxs-lookup"><span data-stu-id="ce933-157">Click **Devices**.</span></span>
    3. <span data-ttu-id="ce933-158">Bonjour tabulaires liste des périphériques, vérifiez que ce périphérique hello toohello service connecté en vérifiant hello état.</span><span class="sxs-lookup"><span data-stu-id="ce933-158">In hello tabular listing of devices, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="ce933-159">état du périphérique Hello doit être **prêt tooset des**.</span><span class="sxs-lookup"><span data-stu-id="ce933-159">hello device status should be **Ready tooset up**.</span></span>
       
        ![Page Appareils StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        <span data-ttu-id="ce933-161">Vous devrez peut-être trop toowait de quelques minutes pour hello appareil état toochange**prêt tooset des**.</span><span class="sxs-lookup"><span data-stu-id="ce933-161">You may need toowait for a couple of minutes for hello device status toochange too**Ready tooset up**.</span></span>
       
        <span data-ttu-id="ce933-162">Si les appareils hello n’apparaît pas dans cette liste, vous devez toomake que votre réseau de pare-feu a été configuré comme décrit dans [configuration réseau requise pour votre appareil StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="ce933-162">If hello device does not show up in this list, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span></span> <span data-ttu-id="ce933-163">Vérifiez que le port 9354 est ouvert aux communications sortantes comme il est utilisé par bus de service hello pour la communication de service sur l’appareil StorSimple le Gestionnaire de périphériques.</span><span class="sxs-lookup"><span data-stu-id="ce933-163">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Device Manager service-to-device communication.</span></span>

