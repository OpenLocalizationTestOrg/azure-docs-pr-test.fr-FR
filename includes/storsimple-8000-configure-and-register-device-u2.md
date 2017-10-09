<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a>Appareil de hello tooconfigure et Registre

1. Accéder à l’interface Windows PowerShell hello sur votre console série du périphérique StorSimple. Consultez [console série du périphérique toohello tooconnect utilisez PuTTY](#use-putty-to-connect-to-the-device-serial-console) pour obtenir des instructions. **Être procédure de hello toofollow vraiment exactement ou vous ne serez pas la console de hello tooaccess en mesure de.**

2. Dans la session hello qui s’ouvre, appuyez sur **entrée** un temps tooget une invite de commandes.

3. Vous seront demandées toochoose hello langage que tooset pour votre appareil. Spécifiez la langue de hello, puis appuyez sur **entrée**.

4. Dans le menu de console série hello qui s’affiche, sélectionnez l’option 1 trop**connecter avec un accès complet**.
     Complétez les paramètres de configuration réseau requise minimale de hello de tooconfigure étapes 5 à 12 pour votre appareil. **Ces étapes de configuration doivent toobe effectuée sur le contrôleur actif de hello du périphérique de hello.** menu de console série Hello indique l’état du contrôleur hello dans message de bannière hello. Si vous n’êtes pas connecté toohello de contrôleur actif, vous déconnecter, puis connectez contrôleur actif de toohello.

5. À l’invite de commandes hello, tapez votre mot de passe. mot de passe par défaut Hello est **Password1**.

6. Hello type commande suivante : `Invoke-HcsSetupWizard`.

7. Un Assistant d’installation s’affiche toohelp configurer les paramètres de réseau hello pour appareil de hello. Fournissez hello hello informations suivantes :
   
   * Adresse IP pour hello interface réseau DATA 0
   * Masque de sous-réseau
   * Passerelle
   * Adresse IP du serveur DNS principal

   Un exemple de sortie est présenté ci-dessous.

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
    Bonjour précédant le résultat de l’exemple, vous pouvez voir que le système de hello est validation des paramètres de réseau après chaque étape dans le processus de hello.

     > [!NOTE]
     > Vous avez peut-être toowait pendant quelques minutes pour le masque de sous-réseau hello et hello DNS paramètres toobe appliqué. Si vous obtenez un message d’erreur « Vérification hello réseau connectivité tooData 0 », vérifiez la connexion de réseau physique hello sur hello interface réseau DATA 0 de votre contrôleur actif.

8. (Facultatif) Configurez votre serveur proxy web. Bien que la configuration du proxy web soit facultative, **si vous en utilisez un, vous pouvez uniquement le configurer ici**. Pour plus d’informations, consultez trop[configurer un proxy web pour votre appareil](../articles/storsimple/storsimple-8000-configure-web-proxy.md).
9. Configurez un serveur NTP principal pour votre appareil. Les serveurs NTP sont requis. En effet, votre appareil doit synchroniser les heures pour pouvoir s’authentifier auprès de vos fournisseurs de services cloud. Vérifiez que votre réseau permet toopass de trafic NTP à partir de votre toohello de centre de données Internet. Si ce n’est pas possible, spécifiez un serveur NTP interne.

    Voici un exemple de sortie obtenue.

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. Pour des raisons de sécurité, mot de passe administrateur hello appareil expire au bout de hello première session, et vous devrez toochange informatique maintenant. Lorsque vous y êtes invité, fournissez un mot de passe administrateur de l’appareil. Un mot de passe administrateur d’appareil valide doit comprendre entre 8 et 15 caractères. Hello mot de passe doit contenir 3 des éléments suivants de hello : caractères en minuscules, majuscules, numériques et spéciaux.

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. étape finale de Hello dans l’Assistant Installation de hello inscrit votre appareil avec hello service du Gestionnaire de périphériques StorSimple. Pour ce faire, vous devez hello clé d’inscription que vous avez obtenue à l’étape 2. Une fois que vous fournissez la clé d’inscription de hello, vous devrez peut-être toowait 2-3 minutes avant l’inscription de périphérique de hello.
    
    > [!NOTE]
    > Vous pouvez appuyer sur Ctrl + C à n’importe quel Assistant Installation de temps tooexit hello. Si vous avez entré tous les paramètres de réseau hello (adresse IP de Data 0, masque de sous-réseau et passerelle), les entrées sont conservées.
    
    Voici un exemple de sortie obtenue.

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. Après l’inscription d’appareil de hello, une clé de chiffrement de données de Service s’affiche. Copiez-la et enregistrez-la en lieu sûr. **Cette clé sera requise avec hello service d’inscription tooregister clé des unités supplémentaires dans hello service du Gestionnaire de périphériques StorSimple.** Consultez trop[sécurité StorSimple](../articles/storsimple/storsimple-security.md) pour plus d’informations sur cette clé.
    
    ![Inscription de l’appareil StorSimple 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > texte hello de toocopy à partir de la fenêtre de console série hello, sélectionnez simplement le texte hello. Vous devez maintenant être en mesure de toopaste dans le Presse-papiers de hello ou un éditeur de texte. N’utilisez pas de Ctrl + C toocopy hello clé de chiffrement. À l’aide de Ctrl + C Assitant vous tooexit hello le programme d’installation. Par conséquent, mot de passe administrateur hello périphérique ne sera pas modifié et l’appareil hello seront rétablis toohello un mot de passe par défaut.
    
13. Quittez la console série hello.
14. Retour toohello portail Azure et hello complète comme suit :
    
    1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour.
    2. Cliquez sur **Appareils**.
    3. Bonjour tabulaires liste des périphériques, vérifiez que ce périphérique hello toohello service connecté en vérifiant hello état. état du périphérique Hello doit être **prêt tooset des**.
       
        ![Page Appareils StorSimple](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        Vous devrez peut-être trop toowait de quelques minutes pour hello appareil état toochange**prêt tooset des**.
       
        Si les appareils hello n’apparaît pas dans cette liste, vous devez toomake que votre réseau de pare-feu a été configuré comme décrit dans [configuration réseau requise pour votre appareil StorSimple](../articles/storsimple/storsimple-8000-system-requirements.md). Vérifiez que le port 9354 est ouvert aux communications sortantes comme il est utilisé par bus de service hello pour la communication de service sur l’appareil StorSimple le Gestionnaire de périphériques.

