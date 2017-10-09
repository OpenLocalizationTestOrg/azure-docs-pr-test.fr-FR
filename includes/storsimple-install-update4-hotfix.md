<!--author=alkohli last changed: 02/10/17-->

#### <a name="toodownload-hotfixes"></a>correctifs logiciels toodownload

Effectuer hello suivant étapes toodownload hello mise à jour à partir de hello catalogue Microsoft Update.

1. Démarrez Internet Explorer et accédez trop[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. S’il s’agit de votre première utilisation hello catalogue Microsoft Update sur cet ordinateur, cliquez sur **installer** lorsque tooinstall demandée hello module complémentaire du catalogue Microsoft Update.

    ![Installer le catalogue](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. Dans la zone de recherche hello Hello catalogue Microsoft Update, entrez le nombre de Base de connaissances (KB) hello de hello correctif souhaité toodownload, par exemple **4011839**, puis cliquez sur **recherche**.
   
    Hello correctif liste s’affiche, par exemple, **Cumulative 4.0 de mise à jour logicielle offre groupée pour StorSimple 8000 Series**.
   
    ![Rechercher dans le catalogue](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)

4. Cliquez sur **Télécharger**. Spécifiez ou **Parcourir** tooa local emplacement souhaité hello télécharge tooappear. Cliquez sur les fichiers hello toodownload toohello spécifié l’emplacement et le dossier. dossier de Hello peut également être tooa copié partage réseau accessible à partir de l’appareil de hello.
5. Recherche de tous les correctifs supplémentaires répertoriées dans le tableau hello ci-dessus (**4011841**), et hello de téléchargement correspondant de fichiers des dossiers spécifiques toohello comme indiqué dans le tableau précédent de hello.

> [!NOTE]
> les correctifs logiciels Hello doivent être accessibles depuis les deux toodetect contrôleurs toute erreur potentielle de messages à partir du contrôleur homologue de hello.
>
> les correctifs logiciels Hello doivent être copiés dans des dossiers distincts 3. Par exemple, la mise à jour de l’agent de logiciel/Cis/MDS hello périphérique peut être copié dans _FirstOrderUpdate_ hello de dossier, tous les autres mises à jour sans interruption de service peuvent être copiées à hello _SecondOrderUpdate_ dossier, et mises à jour du mode maintenance copiés dans _ThirdOrderUpdate_ dossier.

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall et vérifiez les correctifs en mode normal

Effectuer hello suivant les étapes tooinstall et vérifier les correctifs en mode normal. Si vous avez déjà installé à l’aide de hello portail Azure classic, passez directement trop[installer et vérifier les correctifs en mode de maintenance](#to-install-and-verify-maintenance-mode-hotfixes).

1. correctifs logiciels hello tooinstall, interface de Windows PowerShell hello accès sur votre console série du périphérique StorSimple. Suivez hello des instructions dans [console série d’utilisation PuTTy tooconnect toohello](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). Appuyez sur l’invite de commande hello, **entrée**.
2. Sélectionnez **Option 1** toolog sur l’appareil toohello avec un accès complet. Nous vous recommandons d’installer hello correctif sur le contrôleur passif de hello tout d’abord.
3. correctif de hello tooinstall, à hello invite de commandes, tapez :
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Utilisez IP plutôt que DNS dans le chemin d’accès de partage Bonjour au-dessus de commande. paramètre des informations d’identification de Hello est utilisé uniquement si vous accédez à un partage authentifié.
   
    Nous vous recommandons d’utiliser les partages de tooaccess paramètre hello d’informations d’identification. Même les partages qui sont ouverts trop « tout le monde » est généralement pas ouvrir toounauthenticated utilisateurs.
   
    Fournissez le mot de passe hello lorsque vous y êtes invité.
   
    Vous trouverez ci-dessous un exemple de sortie pour l’installation des mises à jour de commande premier hello. Hello première commande mise à jour, vous devez toopoint toohello un fichier spécifique.
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
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
    LastUpdateTimestamp : 02/03/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     Hello suivant l’exemple de sortie indique que cette mise à jour hello est terminée. Hello `RunInProgress` sera `False` lorsque la mise à jour hello est terminée.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 02/03/2017 9:15:55 AM
    LastUpdateTimestamp : 02/03/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > Hello occasionnellement, les rapports de l’applet de commande `False` lorsque la mise à jour hello est toujours en cours. tooensure qui hello correctif est terminée, patientez quelques minutes, réexécutez cette commande et vérifiez que hello `RunInProgress` est `False`. S’il s’agit, hello correctif est terminée.

6. Une fois la mise à jour logicielle de hello est terminée, vérifiez les versions des logiciels système hello. Entrez :
   
    `Get-HcsSystem`
   
    Vous devez voir hello versions suivantes :
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 4.0`
   *  `HcsSoftwareVersion: 6.3.9600.17820`
   
    Si le numéro de version hello ne change pas après avoir appliqué la mise à jour hello, il indique ce correctif hello a échoué tooapply. Dans ce cas, contactez le [Support Microsoft](../articles/storsimple/storsimple-contact-microsoft-support.md) pour obtenir une assistance supplémentaire.
     
    > [!IMPORTANT]
    > Vous devez redémarrer le contrôleur actif de hello via hello `Restart-HcsController` applet de commande avant l’application hello prochaine mise à jour.
     
7. Répétez les étapes 3 à 5 tooinstall hello Cis/MDS agent téléchargé tooyour _FirstOrderUpdate_ dossier. 
8. Répétez les étapes 3 à 5 tooinstall hello deuxième mises à jour. **Deuxième mise à jour de l’ordre, plusieurs mises à jour peuvent être installés en exécutant simplement les hello `Start-HcsHotfix cmdlet` et pointage toohello dossier dans lequel se trouvent les mises à jour de deuxième ordre. applet de commande hello s’exécute toutes les mises à jour de hello disponibles dans le dossier de hello.** Si une mise à jour est déjà installé, la logique de mise à jour hello détectera qu’et pas appliquer cette mise à jour. 

Une fois que tous les correctifs hello sont installés, utilisez hello `Get-HcsSystem` applet de commande. les versions Hello doivent être :

   * `CisAgentVersion:  1.0.9441.0`
   * `MdsAgentVersion: 35.2.2.0`
   * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall et vérifiez les correctifs en mode de maintenance
Utilisez les mises à jour du microprogramme KB4011837 tooinstall disque. Ces mises à jour et prennent environ 30 minutes toocomplete. Vous pouvez choisir tooinstall dans une fenêtre de maintenance planifiée par la console série du périphérique toohello connexion.

Notez que si le microprogramme du disque est déjà à jour, vous n’aurez pas tooinstall ces mises à jour. Exécutez hello `Get-HcsUpdateAvailability` applet de commande hello appareil console série toocheck si les mises à jour sont disponibles et hello si des mises à jour sont perturbateur (mode de maintenance) ou sans interruption de service (mode standard) des mises à jour.

tooinstall hello disque mises à jour, suivez les instructions de hello ci-dessous.

1. Placez l’appareil de hello en mode de maintenance hello. **Notez que vous ne devez pas utiliser la communication à distance de Windows PowerShell lors de la connexion du périphérique tooa en mode maintenance. Au lieu de cela, exécutez cette applet de commande sur le contrôleur de l’appareil hello lorsqu’il est connecté via la console série du périphérique hello.** Entrez :
   
    `Enter-HcsMaintenanceMode`
   
    Voici un exemple de sortie obtenue.
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    Les deux contrôleurs hello puis redémarrez en mode de maintenance.
2. tooinstall hello disque microprogramme mise à jour, type :
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Voici un exemple de sortie obtenue.
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
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
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N002, 0106`
   
   Voici un exemple de sortie obtenue.
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17820
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
           ActiveBIOS:0.45.0010
              BackupBIOS:0.45.0006
              MainCPLD:17.0.000b
              ActiveBMCRoot:2.0.001F
              BackupBMCRoot:2.0.001F
              BMCBoot:2.0.0002
              LsiFirmware:20.00.04.00
              LsiBios:07.37.00.00
              Battery1Firmware:06.2C
              Battery2Firmware:06.2C
              DomFirmware:X231600
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0x9134777A
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x19
              CanisterVPDCRC:0x142F7DC2
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:1.00|1.05
              PCM1VPDStructure:0x05
              PCM1VPDCRC:0x41BEF99C
              PCM2Firmware:1.00|1.05
              PCM2VPDStructure:0x05
              PCM2VPDCRC:0x41BEF99C

           EbodFirmware
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0xB23150F8
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x14
              CanisterVPDCRC:0xBAA55828
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:3.11
              PCM1VPDStructure:0x03
              PCM1VPDCRC:0x6B58AD13
              PCM2Firmware:3.11
              PCM2VPDStructure:0x03
              PCM2VPDCRC:0x6B58AD13

           DisksFirmware
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
   
    Exécutez hello `Get-HcsFirmwareVersion` commande hello deuxième contrôleur tooverify qui hello version du logiciel a été mis à jour. Vous pouvez ensuite quitter le mode de maintenance de hello. Par conséquent, toodo de type hello commande pour chaque contrôleur de périphérique suivante :
   
   `Exit-HcsMaintenanceMode`

5. contrôleurs de Hello redémarrer lorsque vous quittez le mode maintenance. Une fois que du microprogramme du disque hello mises à jour sont correctement appliquées et les appareils hello sont sortie du mode de maintenance, retour toohello portail Azure classic. Notez que ce portail hello peut ne pas affiche que vous avez installé des mises à jour du mode de maintenance hello pendant 24 heures.

