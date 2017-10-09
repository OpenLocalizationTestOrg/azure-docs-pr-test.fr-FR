<!--author=alkohli last changed: 09/01/16-->

#### <a name="toodownload-hotfixes"></a>correctifs logiciels toodownload
Effectuer hello suivant étapes toodownload hello mise à jour à partir de hello catalogue Microsoft Update.

1. Démarrez Internet Explorer et accédez trop[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. S’il s’agit de votre première utilisation hello catalogue Microsoft Update sur cet ordinateur, cliquez sur **installer** lorsque tooinstall demandée hello module complémentaire du catalogue Microsoft Update.
    ![Installer le catalogue](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)
3. Dans la zone de recherche hello Hello catalogue Microsoft Update, entrez le nombre de Base de connaissances (KB) hello de hello correctif souhaité toodownload, par exemple **3186843**, puis cliquez sur **recherche**.
   
    Hello correctif liste s’affiche, par exemple, **Cumulative 3.0 mise à jour offre groupée du logiciel pour StorSimple 8000 Series**.
   
    ![Rechercher dans le catalogue](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. Cliquez sur **Add**. mise à jour Hello est ajouté toohello du panier d’achat.
5. Recherche de tous les correctifs supplémentaires répertoriées dans le tableau hello ci-dessus (**3186859**) et ajoutez chaque panier toohello.
6. Cliquez sur **Afficher le panier**.
7. Cliquez sur **Télécharger**. Spécifiez ou **Parcourir** tooa local emplacement souhaité hello télécharge tooappear. Hello mises à jour sont téléchargées toohello l’emplacement spécifié et placé dans un sous-dossier avec hello même nom en tant que mise à jour hello. dossier de Hello peut également être tooa copié partage réseau accessible à partir de l’appareil de hello.

> [!NOTE]
> les correctifs logiciels Hello doivent être accessibles depuis les deux toodetect contrôleurs toute erreur potentielle de messages à partir du contrôleur homologue de hello.
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall et vérifiez les correctifs en mode normal
Effectuer hello suivant les étapes tooinstall et vérifier les correctifs en mode normal. Si vous avez déjà installé à l’aide de hello portail Azure, passez directement trop[installer et vérifier les correctifs en mode de maintenance](#to-install-and-verify-maintenance-mode-hotfixes).

1. correctifs logiciels hello tooinstall, interface de Windows PowerShell hello accès sur votre console série du périphérique StorSimple. Suivez hello des instructions dans [console série d’utilisation PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). Appuyez sur l’invite de commande hello, **entrée**.
2. Sélectionnez **Option 1** toolog sur l’appareil toohello avec un accès complet. Nous vous recommandons d’installer hello correctif sur le contrôleur passif de hello tout d’abord.
3. correctif de hello tooinstall, à hello invite de commandes, tapez :
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Utilisez IP plutôt que DNS dans le chemin d’accès de partage Bonjour au-dessus de commande. paramètre des informations d’identification de Hello est utilisé uniquement si vous accédez à un partage authentifié.
   
    Nous vous recommandons d’utiliser les partages de tooaccess paramètre hello d’informations d’identification. Même les partages qui sont ouverts trop « tout le monde » est généralement pas ouvrir toounauthenticated utilisateurs.
   
    Fournissez le mot de passe hello lorsque vous y êtes invité.
   
    Voici un exemple de sortie obtenue.
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \hcsmdssoftwareupdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. Type **Y** lorsque tooconfirm demandée hello installation du correctif logiciel.
5. Surveiller les mises à jour hello à l’aide de hello `Get-HcsUpdateStatus` applet de commande. mise à jour Hello terminera tout d’abord sur le contrôleur passif de hello. Une fois que le contrôleur passif de hello est mise à jour, il y aura un basculement et mise à jour hello puis appliqué sur hello autre contrôleur. mise à jour Hello est terminée lorsque les deux contrôleurs hello sont mis à jour.
   
    Hello résultat de l’exemple suivant illustre hello mise à jour en cours d’exécution. Hello `RunInprogress` sera `True` lorsque la mise à jour hello est en cours d’exécution.

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 8/29/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Hello suivant l’exemple de sortie indique que cette mise à jour hello est terminée. Hello `RunInProgress` sera `False` lorsque la mise à jour hello est terminée.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 8/30/2016 9:15:55 AM
    LastUpdateTimestamp : 8/30/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE] 
    > Hello occasionnellement, les rapports de l’applet de commande `False` lorsque la mise à jour hello est toujours en cours. tooensure qui hello correctif est terminée, patientez quelques minutes, réexécutez cette commande et vérifiez que hello `RunInProgress` est `False`. S’il s’agit, hello correctif est terminée.

1. Une fois la mise à jour logicielle de hello est terminée, vérifiez les versions des logiciels système hello. Entrez :
   
    `Get-HcsSystem`
   
    Vous devez voir hello versions suivantes :
   
   * `HcsSoftwareVersion: 6.3.9600.17759`
   * `CisAgentVersion:  1.0.9343.0`
   * `MdsAgentVersion: 30.0.4698.16`
     
     Si les numéros de version hello ne changent pas après avoir appliqué la mise à jour hello, il indique ce correctif hello a échoué tooapply. Dans ce cas, contactez le [Support Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) pour obtenir une assistance supplémentaire.
     
     > [!IMPORTANT]
     > Vous devez redémarrer le contrôleur actif de hello via hello `Restart-HcsController` applet de commande avant l’application hello mises à jour restantes. 
     > 
     > 
2. Répétez les étapes 3 à 5 pilote de hello LSI tooinstall et correctif logiciel de microprogramme **KB3186859**. Après l’installation du correctif hello, utilisez hello `Get-HcsSystem` applet de commande. version de Hello LSI doit être :
   
   * `Lsisas2Version: 2.0.78.00`
3. Répétez les étapes 3 à 5 tooinstall hello Storport et mise à jour Spaceport **KB3121261**.
4. Si vous mettez à jour à partir de la mise à jour 2 ou version antérieure, vous devez également toodownload :
   
   * Correctif iSCSI avec KB3146621
   * Correctif WMI avec KB3103616

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall et vérifiez les correctifs en mode de maintenance
Utilisez les mises à jour du microprogramme KB3121899 tooinstall disque. Ces mises à jour et prennent environ 30 minutes toocomplete. Vous pouvez choisir tooinstall dans une fenêtre de maintenance planifiée par la console série du périphérique toohello connexion.

Notez que si le microprogramme du disque est déjà à jour, vous n’aurez pas tooinstall ces mises à jour. Exécutez hello `Get-HcsUpdateAvailability` applet de commande hello appareil console série toocheck si les mises à jour sont disponibles et hello si des mises à jour sont perturbateur (mode de maintenance) ou sans interruption de service (mode standard) des mises à jour.

tooinstall hello disque mises à jour, suivez les instructions de hello ci-dessous.

1. Placez l’appareil de hello en mode de Maintenance hello. Notez que vous ne devez pas utiliser la communication à distance de Windows PowerShell lors de la connexion du périphérique tooa en mode Maintenance. Au lieu de cela, exécutez cette applet de commande sur le contrôleur de l’appareil hello lorsqu’il est connecté via la console série du périphérique hello. Entrez :
   
    `Enter-HcsMaintenanceMode`
   
    Voici un exemple de sortie obtenue.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
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
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. À l’aide de moniteur hello install progression `Get-HcsUpdateStatus` commande. Hello mise à jour est terminée lorsque hello `RunInProgress` change également`False`.
4. Après que l’installation de hello est terminée, le contrôleur hello sur quel hello correctif en mode de maintenance a été installé redémarre. Connectez-vous en tant qu’option 1 avec un accès complet et vérifier la version du microprogramme du disque hello. Entrez :
   
   `Get-HcsFirmwareVersion`
   
   Hello attendu sont des versions du microprogramme de disque :
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   Voici un exemple de sortie obtenue.
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
         ActiveBIOS:0.45.0006
         BackupBIOS:0.45.0008
         MainCPLD:17.0.0005
         ActiveBMCRoot:2.0.000E
         BackupBMCRoot:2.0.000E
         BMCBoot:2.0.0001
         LsiFirmware:19.00.00.00
         LsiBios:07.37.00.00
         Battery1Firmware:06.29
         Battery2Firmware:06.29
         DomFirmware:X231600
         CanisterFirmware:3.5.0.32
         CanisterBootloader:5.03
         CanisterConfigCRC:0xD1B030A4
         CanisterVPDStructure:0x06
         CanisterGEMCPLD:0x17
         CanisterVPDCRC:0xEE3504B4
         MidplaneVPDStructure:0x0C
         MidplaneVPDCRC:0xA6BD4F64
         MidplaneCPLD:0x10
         PCM1Firmware:1.00|1.05
         PCM1VPDStructure:0x05
         PCM1VPDCRC:0x41BEF99C
         PCM2Firmware:1.00|1.05
         PCM2VPDStructure:0x05
         PCM2VPDCRC:0x41BEF99C
   
         DisksFirmware
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
   
    Exécutez hello `Get-HcsFirmwareVersion` commande hello deuxième contrôleur tooverify qui hello version du logiciel a été mis à jour. Vous pouvez ensuite quitter le mode de maintenance de hello. Par conséquent, toodo de type hello commande pour chaque contrôleur de périphérique suivante :
   
   `Exit-HcsMaintenanceMode`
5. contrôleurs de Hello redémarrer lorsque vous quittez le mode Maintenance. Une fois que du microprogramme du disque hello mises à jour sont correctement appliquées et les appareils hello sont sortie du mode de maintenance, retour toohello portail Azure classic. Notez que ce portail hello peut ne pas affiche que vous avez installé des mises à jour du mode de Maintenance hello pendant 24 heures.

