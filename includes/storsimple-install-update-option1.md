<!--author=SharS last changed: 03/17/2016-->

#### <a name="toodownload-hotfixes"></a>correctifs logiciels toodownload
Effectuer hello étapes toodownload hello logiciel mise à jour suivante.

1. Démarrez Internet Explorer et accédez trop[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. S’il s’agit de votre première utilisation hello catalogue Microsoft Update sur cet ordinateur, cliquez sur **installer** lorsque tooinstall demandée hello module complémentaire du catalogue Microsoft Update.
    ![Installer le catalogue](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)
3. Dans la zone de recherche hello Hello catalogue Microsoft Update, entrez le nombre de Base de connaissances (KB) hello de hello correctif souhaité toodownload, par exemple **3063418**, puis cliquez sur **recherche**.
4. Vous verrez hello **StorSimple Appliance 1.2 jour** offre groupée. Cliquez sur **Add**. mise à jour Hello sera ajouté toohello du panier d’achat.
5. Recherche de tous les correctifs supplémentaires répertoriées dans le tableau hello ci-dessus (**3043005** et **3063416**) et ajoutez chaque panier hello.
6. Cliquez sur **Afficher le panier**.
   
    ![Afficher le panier](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. Cliquez sur **Télécharger**. Spécifiez ou **Parcourir** tooa local emplacement souhaité hello télécharge tooappear. Hello mises à jour sont téléchargées toohello l’emplacement spécifié et placé dans un sous-dossier portant le même nom qu’une mise à jour hello de hello. dossier de Hello peut également être tooa copié partage réseau accessible à partir de l’appareil de hello.

> [!NOTE]
> les correctifs logiciels Hello doivent être accessibles depuis les deux toodetect contrôleurs toute erreur potentielle de messages à partir du contrôleur homologue de hello.
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall et vérifiez les correctifs en mode normal
Effectuer hello suivant les étapes tooinstall et vérifier les correctifs en mode normal hello. Si vous avez déjà installé à l’aide de hello portail Azure, passez directement trop[installer et vérifier les correctifs en mode de maintenance](#to-install-and-verify-maintenance-mode-hotfixes).

1. mettre à jour de logiciels de hello tooinstall, interface de Windows PowerShell hello accès sur votre console série du périphérique StorSimple. Suivez hello des instructions dans [console série d’utilisation PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). Appuyez sur l’invite de commande hello, **entrée**.
2. Sélectionnez **Option 1** toolog sur l’appareil toohello avec un accès complet.
3. packages de mise à jour hello tooinstall, à hello invite de commandes, tapez :
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Utilisez IP plutôt que DNS dans le chemin d’accès de partage Bonjour au-dessus de commande. paramètre des informations d’identification de Hello est utilisé uniquement si vous accédez à un partage authentifié.
   
    Nous vous recommandons d’utiliser les partages de tooaccess paramètre hello d’informations d’identification. Même les partages qui sont ouverts trop « tout le monde » est généralement pas ouvrir toounauthenticated utilisateurs.
   
    Voici un exemple de sortie obtenue.
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. Type **Y** lorsque tooconfirm demandée hello installation du correctif logiciel.
5. Surveiller les mises à jour hello à l’aide de hello `Get-HcsUpdateStatus` applet de commande.
   
    Hello résultat de l’exemple suivant illustre hello mise à jour en cours d’exécution. Hello `RunInprogress` sera `True` lorsque la mise à jour hello est en cours d’exécution.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Hello suivant l’exemple de sortie indique que cette mise à jour hello est terminée. Hello `RunInProgress` sera `False` lorsque la mise à jour hello est terminée.

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > Hello occasionnellement, les rapports de l’applet de commande `False` lorsque la mise à jour hello est toujours en cours. tooensure qui hello correctif est terminée, patientez quelques minutes, réexécutez cette commande et vérifiez que hello `RunInProgress` est `False`. S’il s’agit, hello correctif est terminée.
   > 
   > 
6. Une fois la mise à jour logicielle de hello est terminée, vérifiez les versions des logiciels système hello. Tapez hello de commande suivante :
   
    `Get-HcsSystem`
   
    Vous devez voir hello versions suivantes :
   
   * HcsSoftwareVersion : 6.3.9600.17584
   * CisAgentVersion : 1.0.9049.0
   * MdsAgentVersion : 26.0.4696.1433
     
     Si les numéros de version hello ne changent pas après avoir appliqué la mise à jour hello, il indique ce correctif hello a échoué tooapply. Dans ce cas, contactez le [Support Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) pour obtenir une assistance supplémentaire.
7. Répétez les étapes 3 à 5 hello de tooinstall restant le correctif en mode normal (KB3043005).

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall et vérifiez les correctifs en mode de maintenance
Utilisez les mises à jour du microprogramme KB3063416 tooinstall disque. Ces mises à jour et prennent autour de toocomplete de 30 à 45 minutes. Vous pouvez choisir tooinstall dans une fenêtre de maintenance planifiée par la console série du périphérique toohello connexion.

tooinstall hello disque mises à jour, suivez les instructions de hello ci-dessous.

1. Placez l’appareil de hello en mode Maintenance. Notez que vous ne devez pas utiliser la communication à distance de Windows PowerShell lors de la connexion du périphérique tooa en mode Maintenance. Vous devez toorun cette applet de commande sur le contrôleur de l’appareil hello lorsqu’il est connecté via la console série du périphérique hello. Entrez :
   
    `Enter-HcsMaintenanceMode`
   
    Voici un exemple de sortie obtenue.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    Les deux contrôleurs hello puis redémarrez en mode de Maintenance.
2. tooinstall hello disque microprogramme mise à jour, type :
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Voici un exemple de sortie obtenue.
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. À l’aide de moniteur hello install progression `Get-HcsUpdateStatus` commande. Hello mise à jour est terminée lorsque hello `RunInProgress` change également`False`.
4. Une fois l’installation de hello est terminée, contrôleur hello sur lequel le correctif en mode de maintenance hello a été installé sera redémarré. Connectez-vous en tant qu’option 1 avec un accès complet et vérifier la version du microprogramme du disque hello. Entrez :
   
   `Get-HcsFirmwareVersion`
   
   Hello attendu sont des versions du microprogramme de disque :
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   Exécutez hello `Get-HcsFirmwareVersion` commande hello deuxième contrôleur tooverify qui hello version du logiciel a été mis à jour. Vous pouvez ensuite quitter le mode de maintenance de hello. Tapez hello commande pour chaque contrôleur de périphérique suivante :
   
   `Exit-HcsMaintenanceMode`
5. contrôleurs de Hello redémarrer lorsque vous quittez le mode Maintenance. Une fois que du microprogramme du disque hello mises à jour sont correctement appliquées et les appareils hello sont sortie du mode de maintenance, retour toohello portail Azure classic. Notez que ce portail hello peut ne pas affiche que vous avez installé des mises à jour du mode de Maintenance hello pendant 24 heures.

