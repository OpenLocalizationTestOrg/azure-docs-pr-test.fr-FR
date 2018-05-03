<!--author=alkohli last changed: 9/17/15-->

#### <a name="to-complete-the-minimum-storsimple-device-setup"></a>Pour mener à bien la configuration minimale d’un appareil StorSimple
1. Dans la page **Appareils** , sélectionnez l’appareil, cliquez sur la flèche en regard du nom de l’appareil pour accéder à la page d’appareil spécifique. 
   
    ![Page Appareils avec le périphérique en ligne](./media/storsimple-complete-minimum-device-setup/HCS_DevicesPageM-include.png) 
2. Cliquez sur l’icône Démarrage rapide ![Icône Quick Start](./media/storsimple-complete-minimum-device-setup/HCS_QuickStartIcon-include.png) pour accéder à la page de démarrage rapide de l’appareil. Cliquez sur **Terminer la configuration de l’appareil** pour démarrer l’Assistant **Configurer l’appareil**.
   
    ![Page de démarrage rapide de l'appareil](./media/storsimple-complete-minimum-device-setup/Device_Quick_Start_page_1M.png)
3. Dans la page **Paramètres de base** , procédez comme suit :
   
   1. Entrez un **Nom convivial** pour votre appareil. Le nom de l’appareil par défaut reflète des informations telles que le modèle de l’appareil et son numéro de série. Vous pouvez attribuer un nom convivial allant jusqu'à 64 caractères pour gérer l’appareil.
   2. Définissez le **fuseau horaire** en fonction de l'emplacement géographique de l’appareil déployé. Votre appareil utilise ce fuseau horaire pour toutes les opérations planifiées.
   3. Sous **Paramètres DNS**, entrez une adresse pour votre **Serveur DNS secondaire**. Si vous utilisez le protocole IPv6, le champ est renseigné en fonction du préfixe IPv6 fourni dans l'interface Windows PowerShell. 
      Si le serveur DNS secondaire n'est pas configuré, vous ne pouvez pas enregistrer la configuration de votre appareil.
   4. Sous les interfaces iSCSI activées, activez au moins un réseau pour le protocole iSCSI. Vous devez activer au moins une interface réseau pour le cloud et posséder au moins une interface compatible avec le protocole iSCSI. Le réseau DATA 0 est automatiquement activé pour le cloud.
      
      ![Paramètres de base de la configuration minimale de l'appareil StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupBasicSettings1-include.png)
4. Cliquez sur l’icône en forme de flèche. ![Icône en forme de flèche StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
5. Dans la page **Interfaces réseau** , entrez les adresses IP fixes pour les contrôleurs 0 et 1. Si l’interface du réseau DATA 0 est configurée pour le protocole IPv4, les adresses IP fixes doivent être fournies au format IPv4. Si vous avez fourni un préfixe pour la configuration du protocole IPv6, ces champs sont automatiquement remplis par des adresses IP fixes.

    > [!NOTE] 
    > - Les adresses IP fixes des contrôleurs doivent être disponibles au sein du sous-réseau accessible par l'adresse IP de l’appareil.
    > - Les adresses IP fixes du contrôleur sont utilisées pour traiter les mises à jour de l’appareil. Par conséquent, les adresses IP fixes doivent pouvoir être acheminées et capables de se connecter à Internet.

    ![Interfaces réseau de la configuration minimale d’un appareil StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

1. Cliquez ensuite sur l'icône en forme de coche ![Icône en forme de coche StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).
   Vous revenez à la page **Démarrage rapide** de l'appareil.
   
   > [!NOTE]
   > Vous pouvez modifier tous les autres paramètres de l’appareil à tout moment en accédant à la page **Configurer** de l'appareil.
   > 
   > 

![Vidéo disponible](./media/storsimple-complete-minimum-device-setup/Video_icon.png)**Vidéo disponible**

Pour visionner une vidéo qui montre comment effectuer l’installation minimale de l’appareil, cliquez [ici](https://azure.microsoft.com/documentation/videos/minimum-storsimple-device-setup/).

