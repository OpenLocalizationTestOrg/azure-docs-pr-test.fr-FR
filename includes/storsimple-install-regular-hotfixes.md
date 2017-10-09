<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a>correctifs normaux de tooinstall via Windows PowerShell pour StorSimple
1. Connecter la console série du périphérique toohello. Pour plus d’informations, consultez [étape 1 : connecter la console série de toohello](../articles/storsimple/storsimple-update-device.md#step1).
2. Dans le menu de console série hello, sélectionnez l’option 1, **connecter avec un accès complet**. Mot de passe type hello. mot de passe Hello **Password1**.
3. À l’invite de commandes hello, tapez :
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > Cette commande s’applique uniquement les correctifs logiciels tooregular. Vous exécutez cette commande sur un seul contrôleur, mais les deux contrôleurs sont mis à jour.
    > Vous pouvez remarquer un basculement de contrôleur pendant le processus de mise à jour hello ; Toutefois, hello basculement affecteront pas la disponibilité du système ou l’opération.

4. Lorsque vous y êtes invité, fournissez hello chemin d’accès toohello dossier réseau partagé qui contient les fichiers de correctifs logiciels hello.
5. Vous êtes invité à confirmer l’opération. Type **Y** tooproceed avec l’installation du correctif logiciel hello.

