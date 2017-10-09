<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>mises à jour du mode de Maintenance tooinstall via Windows PowerShell pour StorSimple
1. Si vous n’avez pas déjà fait, accès console série du périphérique hello et sélectionnez l’option 1, **connecter avec un accès complet**. 
2. Mot de passe type hello. mot de passe Hello **Password1**.
3. À l’invite de commandes hello, tapez :
   
     `Get-HcsUpdateAvailability` 
4. Vous êtes averti si des mises à jour sont disponibles et si les mises à jour hello sont sans interruption ou sans interruption de service. tooapply mises à jour, vous avez besoin tooput hello périphérique en mode Maintenance. Pour obtenir des instructions, consultez l’[Étape 2 : passage en mode Maintenance](../articles/storsimple/storsimple-update-device.md#step2).
5. Lorsque votre appareil est en mode Maintenance, à l’invite de commande hello, tapez :`Start-HcsUpdate`
6. Vous êtes invité à confirmer l’opération. Après avoir confirmé les mises à jour hello, ils seront installés sur le contrôleur hello auquel vous accédez. Après installent des mises à jour hello, hello redémarre. 
7. Surveiller l’état de hello des mises à jour. Entrez :
   
    `Get-HcsUpdateStatus`
   
    Si hello `RunInProgress` est `True`, mise à jour hello est toujours en cours. Si `RunInProgress` est `False`, il indique que cette mise à jour hello est terminée.  
8. Lors de la mise à jour hello est installé sur le contrôleur actuel de hello et il a redémarré, connectez-vous toohello autre contrôleur et effectuez les étapes 1 à 6.
9. Après la mise à jour des deux contrôleurs, quittez le mode Maintenance. Pour obtenir des instructions, consultez l’[Étape 4 : quitter le mode Maintenance](../articles/storsimple/storsimple-update-device.md#step4).

