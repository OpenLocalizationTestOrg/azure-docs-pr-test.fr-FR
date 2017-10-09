<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>installation du périphérique StorSimple minimale toocomplete hello
1. Bonjour **périphériques** page, l’appareil de hello sélectionnez, cliquez sur la flèche vers hello par rapport à la page de hello appareil nom toogo toohello périphérique spécifique. 
   
    ![Page Appareils avec le périphérique en ligne](./media/storsimple-complete-minimum-device-setup/HCS_DevicesPageM-include.png) 
2. Cliquez sur icône de démarrage rapide ![icône de démarrage rapide](./media/storsimple-complete-minimum-device-setup/HCS_QuickStartIcon-include.png) tooaccess hello page démarrage rapide du périphérique. Cliquez sur **terminer l’installation de l’appareil** toostart hello **configurer le périphérique** Assistant.
   
    ![Page de démarrage rapide de l'appareil](./media/storsimple-complete-minimum-device-setup/Device_Quick_Start_page_1M.png)
3. Sur hello **les paramètres de base** page, procédez comme hello suivant :
   
   1. Entrez un **Nom convivial** pour votre appareil. nom de périphérique par défaut Hello reflète les informations telles que le modèle d’appareil hello et numéro de série. Vous pouvez affecter un nom convivial des too64 caractères toomanage votre appareil.
   2. Ensemble hello **fuseau horaire** basés sur l’emplacement géographique de hello dans le hello appareil est en cours de déploiement. Votre appareil utilise ce fuseau horaire pour toutes les opérations planifiées.
   3. Sous **Paramètres DNS**, entrez une adresse pour votre **Serveur DNS secondaire**. Si vous utilisez IPv6, champ de hello est rempli en fonction de hello du préfixe IPv6 indiqué dans l’interface Windows PowerShell hello. 
      Si le serveur DNS secondaire de hello n’est pas configuré, vous ne serez pas autorisé toosave votre configuration de l’appareil.
   4. Sous les interfaces iSCSI activées, activez au moins un réseau pour le protocole iSCSI. Au moins une interface réseau doit toobe activé pour le cloud et une interface toobe compatible iSCSI. Le réseau DATA 0 est automatiquement activé pour le cloud.
      
      ![Paramètres de base de la configuration minimale de l'appareil StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupBasicSettings1-include.png)
4. Cliquez sur icône de flèche hello. ![Icône en forme de flèche StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
5. Sur hello **Interfaces réseau** , fournissez hello fixe des adresses IP pour le contrôleur 0 et 1. Si hello DATA 0, l’interface a été configurée pour IPv4, hello fixe IP adresses besoin toobe prévue hello format IPv4. Si vous avez indiqué un préfixe pour la configuration IPv6, adresses IP fixé de hello contiendra automatiquement dans ces champs.

    > [!NOTE] 
    > - les adresses IP fixé des contrôleurs de Hello besoin toobe libre des adresses IP de sous-réseau hello accessible par l’adresse IP du périphérique hello.
    > - Hello fixe d’adresses IP pour le contrôleur de hello sont utilisées pour traiter les périphériques de toohello hello mises à jour, et par conséquent hello adresses IP fixé doit être routables et capables de tooconnect toohello Internet.

    ![Interfaces réseau de la configuration minimale d’un appareil StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

1. Cliquez sur une icône de coche hello ![StorSimple coche](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).
   Vous revenez toohello périphérique **Quick Start** page.
   
   > [!NOTE]
   > Vous pouvez modifier hello tous les autres paramètres de l’appareil à tout moment en accédant à hello **configurer** page.
   > 
   > 

![Vidéo disponible](./media/storsimple-complete-minimum-device-setup/Video_icon.png)**Vidéo disponible**

toowatch une vidéo qui montre comment toocomplete hello d’installation minimale de l’appareil, cliquez sur [ici](https://azure.microsoft.com/documentation/videos/minimum-storsimple-device-setup/).

