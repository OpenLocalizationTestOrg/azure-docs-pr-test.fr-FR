<!--author=alkohli last changed: 01/12/17-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>installation du périphérique StorSimple minimale toocomplete hello

   > [!NOTE]
   > Impossible de modifier le nom de l’appareil hello une fois que le programme d’installation minimale de l’appareil de hello est terminé.
   
1. À partir de la liste tabulaire des appareils de hello hello **périphériques** panneau, sélectionnez et cliquez sur votre appareil. Appareil de Hello est dans un **prêt tooset des** état. Hello **configurer le périphérique** panneau s’ouvre.

     ![Interfaces réseau de la configuration minimale d’un appareil StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig1.png)

2. Bonjour **configurer le périphérique** panneau :
   
   1. Entrez un **Nom convivial** pour votre appareil. nom de périphérique par défaut Hello reflète les informations telles que le modèle d’appareil hello et numéro de série. Vous pouvez affecter un nom convivial des too64 caractères toomanage votre appareil.
   2. Ensemble hello **fuseau horaire** basés sur l’emplacement géographique de hello dans le hello appareil est en cours de déploiement. Votre appareil utilise ce fuseau horaire pour toutes les opérations planifiées.
   3. Sous hello **DATA 0 paramètres**:

       1. Votre DATA 0 interface réseau montre comme activé avec hello les paramètres (IP, sous-réseau, passerelle) configurés via l’Assistant d’installation hello réseau. DATA 0 est également automatiquement activé pour le cloud, ainsi que pour l’iSCSI.

       2. Fournissent des hello des adresses IP pour le contrôleur 0 et 1. **les adresses IP fixé des contrôleurs de Hello besoin toobe libre des adresses IP de sous-réseau hello accessible par l’adresse IP du périphérique hello.** Si hello DATA 0, l’interface a été configurée pour IPv4, hello fixe IP adresses besoin toobe prévue hello format IPv4. Si vous avez indiqué un préfixe pour la configuration IPv6, hello des adresses IP fixes sont remplis automatiquement dans ces champs.

            ![Interfaces réseau de la configuration minimale d’un appareil StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig2.png)

            Hello fixe d’adresses IP pour le contrôleur de hello sont utilisées pour la maintenance des appareils de toohello hello mises à jour. Par conséquent, hello adresses IP fixé doit être routables et capables de tooconnect toohello Internet. Vous pouvez vérifier que votre contrôleur fixe des adresses IP sont routables à l’aide de hello [Test-HcsmConnection] [ Test] applet de commande. Hello affiche fixé de contrôleur des adresses IP est routé toohello Internet et peut accéder à l’exemple suivant hello serveurs Microsoft Update.

            ![Test-HcsmConnection indiquant les adresses IP routables](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig3.png)

1. Cliquez sur **OK**. configuration de l’appareil Hello démarre. Lors de la configuration de l’appareil hello est terminée, vous êtes averti. Hello trop de modifications d’état de périphérique**Online** Bonjour **périphériques** panneau.

    ![Interfaces réseau de la configuration minimale d’un appareil StorSimple](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig4.png)

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx
