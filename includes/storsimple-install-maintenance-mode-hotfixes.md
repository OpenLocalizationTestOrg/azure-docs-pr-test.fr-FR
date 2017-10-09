<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a>tooinstall les correctifs en mode de Maintenance via Windows PowerShell pour StorSimple
> [!IMPORTANT]
> En mode Maintenance, vous devez tout d’abord les tooapply hello correctif sur un contrôleur et puis hello autre contrôleur sur.
> 
> 

1. Placer les appareils hello en mode Maintenance. Consultez [étape 2 : mode de Maintenance d’entrez](../articles/storsimple/storsimple-update-device.md#step2) pour obtenir des instructions sur la façon de mode de Maintenance tooenter.
2. correctif logiciel hello tooapply, type :
   
     `Start-HcsHotfix` 
3. Lorsque vous y êtes invité, fournissez hello chemin d’accès toohello dossier réseau partagé qui contient les fichiers de correctifs logiciels hello.
4. Vous êtes invité à confirmer l’opération. Type **Y** tooproceed avec l’installation du correctif logiciel hello.
5. Après avoir appliqué hello correctif sur un contrôleur, ouverture de session toohello autre contrôleur. Appliquez le correctif de hello comme vous l’avez fait pour le contrôleur précédent de hello.
6. Après l’application des correctifs de hello, quittez le mode de Maintenance. Pour obtenir des instructions, consultez l’[Étape 4 : quitter le mode Maintenance](../articles/storsimple/storsimple-update-device.md#step4).

