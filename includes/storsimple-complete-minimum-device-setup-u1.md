<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>installation du périphérique StorSimple minimale toocomplete hello
1. Sélectionnez le périphérique de hello et cliquez sur **Quick Start**. Cliquez sur **terminer l’installation de l’appareil** Assistant de périphérique toostart hello configurer.
2. Dans l’Assistant de périphérique hello configurer **les paramètres de base** boîte de dialogue zone, hello suivant :
   
   1. Entrez un **Nom convivial** pour votre appareil. nom de périphérique par défaut Hello reflète les informations telles que le modèle d’appareil hello et numéro de série. Vous pouvez affecter un nom convivial des too64 caractères toomanage votre appareil.
   2. Ensemble hello **fuseau horaire** basés sur l’emplacement géographique de hello dans le hello appareil est en cours de déploiement. Votre appareil utilise ce fuseau horaire pour toutes les opérations planifiées.
   3. Sous **Paramètres DNS**, entrez une adresse pour votre **Serveur DNS secondaire**. Si vous utilisez IPv6, champ de hello est rempli en fonction de hello du préfixe IPv6 indiqué dans l’interface Windows PowerShell hello. 
      Si le serveur DNS secondaire de hello n’est pas configuré, vous ne serez pas autorisé toosave votre configuration de l’appareil.
   4. Sous les interfaces iSCSI activées, activez au moins un réseau pour le protocole iSCSI. Au moins une interface réseau doit toobe activé pour le cloud et une interface toobe compatible iSCSI. Le réseau DATA 0 est automatiquement activé pour le cloud.
      
      ![Paramètres de base de la configuration minimale de l'appareil StorSimple](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupBasicSettings1-include.png)
3. Cliquez sur icône de flèche hello. ![Icône en forme de flèche StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
4. Bonjour **Interfaces réseau** boîte de dialogue zone, fournissent des hello des adresses IP pour le contrôleur 0 et 1. **les adresses IP fixé des contrôleurs de Hello besoin toobe libre des adresses IP de sous-réseau hello accessible par l’adresse IP du périphérique hello.** Si hello DATA 0, l’interface a été configurée pour IPv4, hello fixe IP adresses besoin toobe prévue hello format IPv4. Si vous avez indiqué un préfixe pour la configuration IPv6, adresses IP fixé de hello contiendra automatiquement dans ces champs.

    ![Interfaces réseau de la configuration minimale d’un appareil StorSimple](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

    Hello fixe d’adresses IP pour le contrôleur de hello sont utilisées pour traiter les périphériques de toohello hello mises à jour, et par conséquent hello adresses IP fixé doit être routables et capables de tooconnect toohello Internet. Vous pouvez vérifier que votre contrôleur fixe des adresses IP sont routables à l’aide de hello [Test-HcsmConnection] [ Test] applet de commande. Hello affiche fixé de contrôleur des adresses IP est routé toohello Internet et peut accéder à l’exemple suivant hello serveurs Microsoft Update. 

     ![Test-HcsmConnection indiquant les adresses IP routables](./media/storsimple-complete-minimum-device-setup-u1/Test-HcsmConnectionOutputRegisteredDevice.png)

1. Cliquez sur une icône de coche hello ![StorSimple coche](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).
   Vous revenez toohello périphérique **Quick Start** page.
   
   > [!NOTE]
   > Vous pouvez modifier hello tous les autres paramètres de l’appareil à tout moment en accédant à hello **configurer** page.
   > 
   > 

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx