<!--author=alkohli last changed: 12/01/15-->


#### <a name="tooconfigure-and-register-hello-device"></a>Appareil de hello tooconfigure et Registre
1. Accéder à l’interface Windows PowerShell hello sur votre console série du périphérique StorSimple. Consultez [console série du périphérique toohello tooconnect utilisez PuTTY](#use-putty-to-connect-to-the-device-serial-console) pour obtenir des instructions. **Être procédure de hello toofollow vraiment exactement ou vous ne serez pas la console de hello tooaccess en mesure de.**
2. Dans la session hello qui s’ouvre, appuyez sur entrée une fois tooget une invite de commandes. 
3. Vous seront demandées toochoose hello langage que tooset pour votre appareil. Spécifier la langue de hello, puis appuyez sur ENTRÉE. 
   
    ![Configuration et inscription de l’appareil StorSimple 1](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice1-include.png)
4. Dans le menu de console série hello qui s’affiche, choisissez l’option 1 toolog sur avec un accès complet. 
   
    ![Inscription de l’appareil StorSimple 2](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice2-include.png)
   
     Complétez les paramètres de configuration réseau requise minimale de hello de tooconfigure étapes 5 à 12 pour votre appareil. **Ces étapes de configuration doivent toobe effectuée sur le contrôleur actif de hello du périphérique de hello.** menu de console série Hello indique l’état du contrôleur hello dans message de bannière hello. Si vous n’êtes pas connecté toohello de contrôleur actif, vous déconnecter, puis connectez contrôleur actif de toohello.
5. À l’invite de commandes hello, tapez votre mot de passe. mot de passe par défaut Hello est **Password1**.
6. Tapez hello de commande suivante :
   
     `Invoke-HcsSetupWizard` 
7. Un Assistant d’installation s’affiche toohelp configurer les paramètres de réseau hello pour appareil de hello. Fournissez hello hello informations suivantes : 
   
   * Adresse IP pour hello interface réseau DATA 0
   * Masque de sous-réseau
   * Passerelle
   * Adresse IP du serveur DNS principal
   * Adresse IP du serveur NTP principal
     
     > [!NOTE]
     > Vous avez peut-être toowait pendant quelques minutes pour le masque de sous-réseau hello et hello DNS paramètres toobe appliqué. Si vous obtenez un « hello appareil n’est pas prêt. » message d’erreur, vérifiez hello réseau physique la connexion sur hello interface réseau DATA 0 de votre contrôleur actif.
     > 
     > 
8. (Facultatif) Configurez votre serveur proxy web. Bien que la configuration du proxy web soit facultative, **si vous en utilisez un, vous pouvez uniquement le configurer ici**. Pour plus d’informations, consultez trop[configurer un proxy web pour votre appareil](../articles/storsimple/storsimple-configure-web-proxy.md). Si vous rencontrez des problèmes au cours de cette étape, consultez les conseils tootroubleshooting pour [erreurs lors de la configuration de proxy web](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-the-optional-web-proxy-settings).

     > [!NOTE]
     > Vous pouvez appuyer sur Ctrl + C à n’importe quel Assistant Installation de temps tooexit hello. Tous les paramètres que vous avez appliqués avant l’émission de cette commande sont conservés.

1. Pour des raisons de sécurité, mot de passe administrateur hello appareil expire au bout de hello première session, et vous devrez toochange pour les sessions suivantes. Lorsque vous y êtes invité, fournissez un mot de passe administrateur de l’appareil. Un mot de passe administrateur d’appareil valide doit comprendre entre 8 et 15 caractères. mot de passe Hello doit contenir une combinaison de caractères en minuscules, majuscules, des chiffres et des caractères spéciaux.
2. Hello Gestionnaire d’instantanés StorSimple mot de passe est également défini ici. Vous utilisez ce mot de passe lorsque vous authentifiez un appareil avec votre hôte Windows en exécutant le gestionnaire d’instantanés StorSimple. Lorsque vous y êtes invité, fournissez un mot de passe 14 too15 caractères. Hello mot de passe doit contenir une combinaison de trois des éléments suivants de hello : caractères en minuscules, majuscules, numériques et spéciaux. 
   
   ![Inscription de l’appareil StorSimple 4](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice4-include.png)
   
   Vous pouvez réinitialiser un mot de passe de gestionnaire d’instantanés StorSimple à partir de l’interface du service Gestionnaire StorSimple hello hello. Pour des instructions détaillées, consultez trop[modifier les mots de passe hello StorSimple à l’aide de hello transmet au service StorSimple Manager](../articles/storsimple/storsimple-change-passwords.md).
   
   tootroubleshoot toute pendant cette étape, consultez les conseils tootroubleshooting pour [erreurs liées toopasswords](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-related-to-device-administrator-and-storsimple-snapshot-manager-passwords).
3. étape finale de Hello dans l’Assistant Installation de hello inscrit votre appareil avec hello service StorSimple Manager. Pour ce faire, vous devez hello clé d’inscription que vous avez obtenue à l’étape 2. Une fois que vous fournissez la clé d’inscription de hello, vous devrez peut-être toowait 2-3 minutes avant l’inscription de périphérique de hello.
   
   tootroubleshoot les échecs d’inscription de périphériques possible, consultez trop[erreurs lors de l’inscription de périphérique](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-device-registration). Pour plus de résolution des problèmes, vous pouvez également faire référence trop[exemple de dépannage pas à pas](../articles/storsimple/storsimple-troubleshoot-deployment.md#step-by-step-storsimple-troubleshooting-example).
4. Après l’inscription d’appareil de hello, une clé de chiffrement de données de Service s’affiche. Copiez-la et enregistrez-la en lieu sûr.
   
   > [!WARNING]
   > Cette clé sera requise avec hello service d’inscription tooregister clé des unités supplémentaires dans hello service StorSimple Manager. Consultez trop[sécurité StorSimple](../articles/storsimple/storsimple-security.md) pour plus d’informations sur cette clé.
   > 
   > 
   
    ![Inscription de l’appareil StorSimple 6](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice6-include.png)
   
    texte hello de toocopy à partir de la fenêtre de console série hello, sélectionnez simplement le texte hello. Vous devez maintenant être en mesure de toopaste dans le Presse-papiers de hello ou un éditeur de texte. N’utilisez pas de Ctrl + C toocopy hello clé de chiffrement. À l’aide de Ctrl + C Assitant vous tooexit hello le programme d’installation. Par conséquent, mot de passe administrateur de périphérique hello et le mot de passe de gestionnaire d’instantanés StorSimple hello ne seront pas modifiés et l’appareil hello seront rétablis toohello des mots de passe par défaut.
5. Quittez la console série hello.
6. Retour toohello portail Azure classic et hello complète comme suit :
   
   1. Double-cliquez sur votre hello tooaccess du service StorSimple Manager **Quick Start** page.
   2. Cliquez sur **Afficher les appareils connectés**.
   3. Sur hello **périphériques** page, vérifiez que cet appareil hello toohello service connecté en vérifiant hello état. état du périphérique Hello doit être **Online**. Si l’état du périphérique hello est **hors connexion**, attendez quelques minutes pour hello appareil toocome en ligne.
   
   ![Page Appareils StorSimple](./media/storsimple-configure-and-register-device/HCS_DevicesPageM-include.png) 
   
   > [!IMPORTANT]
   > Une fois l’appareil de hello en ligne, branchez les câbles de réseau hello que vous avez été déconnecté de début hello de cette étape.
   > 
   > 

Une fois le périphérique de hello est enregistré correctement et n’intervient pas en ligne, vous pouvez exécuter hello `Test-HcsmConnection -Verbose` tooensure qui hello connectivité réseau n’est pas sain. Pourquoi d’utilisation détaillées de cette applet de commande, accédez à trop[référence d’applet de commande pour Test-HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx).

![Vidéo disponible](./media/storsimple-configure-and-register-device/Video_icon.png)**Vidéo disponible**

toowatch une vidéo qui montre comment tooconfigure et inscrire votre appareil via Windows PowerShell pour StorSimple, cliquez sur [ici](https://azure.microsoft.com/documentation/videos/initialize-the-storsimple-appliance/).

