<!--author=alkohli last changed: 02/22/2016-->


### <a name="tooconfigure-and-register-hello-device"></a>Appareil de hello tooconfigure et Registre
1. Accéder à l’interface Windows PowerShell hello sur votre console série du périphérique StorSimple. Consultez [console série du périphérique toohello tooconnect utilisez PuTTY](#use-putty-to-connect-to-the-device-serial-console) pour obtenir des instructions. **Être procédure de hello toofollow vraiment exactement ou vous ne serez pas la console de hello tooaccess en mesure de.**
2. Dans la session hello qui s’ouvre, appuyez sur entrée une fois tooget une invite de commandes. 
3. Vous seront demandées toochoose hello langage que tooset pour votre appareil. Spécifier la langue de hello, puis appuyez sur ENTRÉE. 
   
    ![Configuration et inscription de l’appareil StorSimple 1](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice1-U1-include.png)
4. Dans le menu de console série hello qui s’affiche, choisissez l’option 1 toolog sur avec un accès complet. 
   
    ![Inscription de l’appareil StorSimple 2](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice2_U1-include.png)
   
     Complétez les paramètres de configuration réseau requise minimale de hello de tooconfigure étapes 5 à 12 pour votre appareil. **Ces étapes de configuration doivent toobe effectuée sur le contrôleur actif de hello du périphérique de hello.** menu de console série Hello indique l’état du contrôleur hello dans message de bannière hello. Si vous n’êtes pas connecté toohello de contrôleur actif, vous déconnecter, puis connectez contrôleur actif de toohello.
5. À l’invite de commandes hello, tapez votre mot de passe. mot de passe par défaut Hello est **Password1**.
6. Hello type commande suivante : `Invoke-HcsSetupWizard`. 
7. Un Assistant d’installation s’affiche toohelp configurer les paramètres de réseau hello pour appareil de hello. Fournissez hello hello informations suivantes : 
   
   * Adresse IP pour hello interface réseau DATA 0
   * Masque de sous-réseau
   * Passerelle
   * Adresse IP du serveur DNS principal
     
        Notez que le système de hello est validation des paramètres de réseau après chaque étape dans le processus de hello.
     
     > [!NOTE]
     > Vous avez peut-être toowait pendant quelques minutes pour le masque de sous-réseau hello et hello DNS paramètres toobe appliqué. Si vous obtenez un message d’erreur « Vérification hello réseau connectivité tooData 0 », vérifiez la connexion de réseau physique hello sur hello interface réseau DATA 0 de votre contrôleur actif.
     > 
     > 
8. (Facultatif) Configurez votre serveur proxy web. Bien que la configuration du proxy web soit facultative, **si vous en utilisez un, vous pouvez uniquement le configurer ici**. Pour plus d’informations, consultez trop[configurer un proxy web pour votre appareil](../articles/storsimple/storsimple-configure-web-proxy.md).
9. Configurez un serveur NTP principal pour votre appareil. Les serveurs NTP sont requis. En effet, votre appareil doit synchroniser les heures pour pouvoir s’authentifier auprès de vos fournisseurs de services cloud. Vérifiez que votre réseau permet toopass de trafic NTP à partir de votre toohello de centre de données Internet. Si ce n’est pas possible, spécifiez un serveur NTP interne. 
10. Pour des raisons de sécurité, mot de passe administrateur hello appareil expire au bout de hello première session, et vous devrez toochange informatique maintenant. Lorsque vous y êtes invité, fournissez un mot de passe administrateur de l’appareil. Un mot de passe administrateur d’appareil valide doit comprendre entre 8 et 15 caractères. Hello mot de passe doit contenir 3 des éléments suivants de hello : caractères en minuscules, majuscules, numériques et spéciaux.
    
    <br/>![Inscription de l’appareil StorSimple 5](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice5_U1-include.png)
11. étape finale de Hello dans l’Assistant Installation de hello inscrit votre appareil avec hello service StorSimple Manager. Pour ce faire, vous devez hello clé d’inscription que vous avez obtenue à l’étape 2. Une fois que vous fournissez la clé d’inscription de hello, vous devrez peut-être toowait 2-3 minutes avant l’inscription de périphérique de hello.
    
    > [!NOTE]
    > Vous pouvez appuyer sur Ctrl + C à n’importe quel Assistant Installation de temps tooexit hello. Si vous avez entré tous les paramètres de réseau hello (adresse IP de Data 0, masque de sous-réseau et passerelle), les entrées sont conservées.
    > 
    > 
    
    ![Inscription de l’appareil StorSimple 6](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice6_U1-include.png)
12. Après l’inscription d’appareil de hello, une clé de chiffrement de données de Service s’affiche. Copiez-la et enregistrez-la en lieu sûr. **Cette clé sera requise avec hello service d’inscription tooregister clé des unités supplémentaires dans hello service StorSimple Manager.** Consultez trop[sécurité StorSimple](../articles/storsimple/storsimple-security.md) pour plus d’informations sur cette clé.
    
    ![Inscription de l’appareil StorSimple 7](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice7_U1-include.png)    
    
    > [!NOTE]
    > texte hello de toocopy à partir de la fenêtre de console série hello, sélectionnez simplement le texte hello. Vous devez maintenant être en mesure de toopaste dans le Presse-papiers de hello ou un éditeur de texte. N’utilisez pas de Ctrl + C toocopy hello clé de chiffrement. À l’aide de Ctrl + C Assitant vous tooexit hello le programme d’installation. Par conséquent, mot de passe administrateur hello périphérique ne sera pas modifié et l’appareil hello seront rétablis toohello un mot de passe par défaut.
    > 
    > 
13. Quittez la console série hello.
14. Retour toohello portail Azure classic et hello complète comme suit :
    
    1. Double-cliquez sur votre hello tooaccess du service StorSimple Manager **Quick Start** page.
    2. Cliquez sur **Afficher les appareils connectés**.
    3. Sur hello **périphériques** page, vérifiez que cet appareil hello toohello service connecté en vérifiant hello état. état du périphérique Hello doit être **Online**.
       
        ![Page Appareils StorSimple](./media/storsimple-configure-and-register-device-u1/HCS_DevicesPageM_U1-include.png) 
       
        Si l’état du périphérique hello est **hors connexion**, attendez quelques minutes pour hello appareil toocome en ligne. 
       
        Si les appareils hello sont encore hors connexion après quelques minutes, vous devez toomake que votre réseau de pare-feu a été configuré comme décrit dans [configuration réseau requise pour votre appareil StorSimple](../articles/storsimple/storsimple-system-requirements.md). 
       
        Vérifiez que le port 9354 est ouvert aux communications sortantes comme il est utilisé par bus de service hello pour la communication de Service-appareil StorSimple Manager.

