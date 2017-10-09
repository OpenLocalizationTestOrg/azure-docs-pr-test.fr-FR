<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a>mises à jour régulières de tooinstall via Windows PowerShell pour StorSimple
1. Ouvrez la console série du périphérique hello et sélectionnez l’option 1, **connecter avec un accès complet**. Mot de passe type hello. mot de passe Hello *Password1*. 
2. À l’invite de commandes hello, tapez :
   
     `Get-HcsUpdateAvailability`
   
    Vous êtes averti si des mises à jour sont disponibles et si les mises à jour hello sont sans interruption ou sans interruption de service.
3. À l’invite de commandes hello, tapez :
   
     `Start-HcsUpdate`
   
    processus de mise à jour Hello démarre.

> [!IMPORTANT]
> * Cette commande s’applique uniquement les mises à jour tooregular. Vous exécutez cette commande sur un seul contrôleur, mais les deux contrôleurs sont mis à jour. 
> * Vous pouvez remarquer un basculement de contrôleur pendant le processus de mise à jour hello ; Toutefois, hello basculement affecteront pas la disponibilité du système ou l’opération.
> 
> 

