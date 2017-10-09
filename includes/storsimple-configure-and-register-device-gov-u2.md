<!--author=SharS last changed: 02/22/2016-->

### <a name="tooconfigure-and-register-hello-device"></a>Appareil de hello tooconfigure et Registre
1. Accéder à l’interface Windows PowerShell hello sur votre console série du périphérique StorSimple. Consultez [console série du périphérique toohello tooconnect utilisez PuTTY](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) pour obtenir des instructions. **Être procédure de hello toofollow vraiment exactement ou vous ne serez pas la console de hello tooaccess en mesure de.**
2. Dans la session hello qui s’ouvre, appuyez sur entrée une fois tooget une invite de commandes.
3. Vous seront demandées toochoose hello langage que tooset pour votre appareil. Spécifier la langue de hello, puis appuyez sur ENTRÉE.
   
    ![Configuration et inscription de l’appareil StorSimple 1](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. Dans le menu de console série hello qui s’affiche, choisissez l’option 1 toolog sur avec un accès complet.
   
    ![Inscription de l’appareil StorSimple 2](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. Effectuer hello suivant les paramètres de procédure tooconfigure hello réseau minimaux requis pour votre appareil.
   
   > [!IMPORTANT]
   > Ces étapes de configuration doivent toobe effectuée sur le contrôleur actif de hello du périphérique de hello. menu de console série Hello indique l’état du contrôleur hello dans message de bannière hello. Si vous ne sont pas connecter contrôleur actif de toohello, se déconnecter, puis connectez contrôleur actif de toohello.
   > 
   > 
   
   1. À l’invite de commandes hello, tapez votre mot de passe. mot de passe par défaut Hello est **Password1**.
   2. Tapez hello de commande suivante :
      
        `Invoke-HcsSetupWizard`
   3. Un Assistant d’installation s’affiche toohelp configurer les paramètres de réseau hello pour appareil de hello. Fournissez hello informations suivantes :
      
      * Adresse IP de l’interface réseau DATA 0
      * Masque de sous-réseau
      * Passerelle
      * Adresse IP du serveur DNS principal
      * Adresse IP du serveur NTP principal
      
      > [!NOTE]
      > Vous avez peut-être toowait pendant quelques minutes pour le masque de sous-réseau hello et toobe de paramètres DNS appliqué.
      > 
      > 
   4. Configurez éventuellement votre serveur proxy web.
      
      > [!IMPORTANT]
      > Bien que la configuration du proxy web soit facultative, si vous en utilisez un, vous pouvez uniquement le configurer ici. Pour plus d’informations, consultez trop[configurer un proxy web pour votre appareil](../articles/storsimple/storsimple-configure-web-proxy.md).
      > 
      > 
6. Appuyez sur Ctrl + C Assistant d’installation tooexit hello.
7. Installez les mises à jour hello comme suit :
   
   1. Utilisez hello suivant tooset de l’applet de commande des adresses IP sur les deux contrôleurs hello :
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. À l’invite de commandes hello, exécutez `Get-HcsUpdateAvailability`. Vous devez recevoir une notification indiquant que les mises à jour sont disponibles.
   3. Exécutez `Start-HcsUpdate`. Vous pouvez exécuter cette commande sur n’importe quel nœud. Les mises à jour seront appliquées sur le premier contrôleur de hello, hello contrôleur bascule et puis hello mises à jour seront appliquées sur hello autre contrôleur.
      
      Vous pouvez surveiller la progression hello de mise à jour hello en exécutant `Get-HcsUpdateStatus`.    
      
      Hello résultat de l’exemple suivant illustre hello mise à jour en cours d’exécution.
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      Hello suivant l’exemple de sortie indique que cette mise à jour hello est terminée.
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      Il peut prendre des heures too11 tooapply tous hello mises à jour, y compris hello mises à jour Windows.
8. Exécutez hello suivant le portail de Microsoft Azure Government applet de commande toopoint hello appareils toohello (car elle pointe toohello portail classique Azure public par défaut). Les deux contrôleurs redémarrent. Nous vous recommandons d’utiliser deux sessions PuTTY toosimultaneously connecter tooboth contrôleurs afin que vous puissiez voir quand chaque contrôleur est redémarré.
   
    `Set-CloudPlatform -AzureGovt_US`
   
   Un message de confirmation s’affiche. Accepter la valeur par défaut hello (**Y**).
9. Exécutez hello après l’installation de tooresume d’applet de commande :
   
    `Invoke-HcsSetupWizard`
   
    ![Reprise de l’Assistant Installation](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   Lorsque vous reprenez le programme d’installation, Assistant de hello sera la version de mise à jour 2 de hello.
10. Acceptez les paramètres de réseau hello. Un message de validation apparaît lorsque vous acceptez un paramètre.
11. Pour des raisons de sécurité, mot de passe administrateur hello appareil expire au bout de hello première session, et vous devrez toochange informatique maintenant. Lorsque vous y êtes invité, fournissez un mot de passe administrateur de l’appareil. Un mot de passe administrateur d’appareil valide doit comprendre entre 8 et 15 caractères. Hello mot de passe doit contenir 3 des éléments suivants de hello : caractères en minuscules, majuscules, numériques et spéciaux.
    
    <br/>![Inscription de l’appareil StorSimple 5](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. étape finale de Hello dans l’Assistant Installation de hello inscrit votre appareil avec hello service StorSimple Manager. Pour ce faire, vous serez peut-être hello clé d’inscription de service que vous avez obtenue dans [étape 2 : clé d’inscription Get hello](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key). Une fois que vous fournissez la clé d’inscription de hello, vous devrez peut-être toowait 2-3 minutes avant l’inscription de périphérique de hello.
    
    > [!NOTE]
    > Vous pouvez appuyer sur Ctrl + C à n’importe quel Assistant Installation de temps tooexit hello. Si vous avez entré tous les paramètres de réseau hello (adresse IP de Data 0, masque de sous-réseau et passerelle), les entrées sont conservées.
    > 
    > 
    
    ![Progression de l’inscription de StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. Après l’inscription d’appareil de hello, une clé de chiffrement de données de Service s’affiche. Copiez-la et enregistrez-la en lieu sûr. **Cette clé sera requise avec hello service d’inscription tooregister clé des unités supplémentaires dans hello service StorSimple Manager.** Consultez trop[sécurité StorSimple](../articles/storsimple/storsimple-security.md) pour plus d’informations sur cette clé.
    
    ![Inscription de l’appareil StorSimple 7](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > texte hello de toocopy à partir de la fenêtre de console série hello, sélectionnez simplement le texte hello. Vous devez maintenant être en mesure de toopaste dans le Presse-papiers de hello ou un éditeur de texte.
    > 
    > N’utilisez pas de Ctrl + C toocopy hello clé de chiffrement. À l’aide de Ctrl + C Assitant vous tooexit hello le programme d’installation. Par conséquent, mot de passe administrateur hello périphérique ne sera pas modifié et l’appareil hello seront rétablis toohello un mot de passe par défaut.
    > 
    > 
14. Quittez la console série hello.
15. Retournez toohello portail Azure du gouvernement et terminer hello comme suit :
    
    1. Double-cliquez sur votre hello tooaccess du service StorSimple Manager **Quick Start** page.
    2. Cliquez sur **Afficher les appareils connectés**.
    3. Sur hello **périphériques** page, vérifiez que cet appareil hello toohello service connecté en vérifiant hello état. état du périphérique Hello doit être **Online**.
       
        ![Page Appareils StorSimple](./media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        Si l’état du périphérique hello est **hors connexion**, attendez quelques minutes pour hello appareil toocome en ligne.
       
        Si les appareils hello sont encore hors connexion après quelques minutes, vous devez toomake que votre réseau de pare-feu a été configuré comme décrit dans [configuration réseau requise pour votre appareil StorSimple](../articles/storsimple/storsimple-system-requirements.md).
       
        Vérifiez que le port 9354 est ouvert aux communications sortantes comme il est utilisé par bus de service hello pour la communication de Service-appareil StorSimple Manager.

