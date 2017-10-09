<!--author=alkohli last changed: 03/17/16-->

## <a name="troubleshooting-update-failures"></a>Résolution des échecs de mise à jour
**Que se passe-t-il si vous voyez une notification qui hello des vérifications de pré-mise à niveau a échoué ?**

Si une vérification préalable échoue, assurez-vous que vous avez recherché dans la barre de notification détaillée hello bas hello de page de hello. Ce guide lors de la vérification préalable de toowhich a échoué. Hello l’illustration suivante montre une instance dans laquelle une notification s’affiche. Dans ce cas, la vérification d’intégrité du contrôleur hello et vérification d’intégrité du composant matériel ont échoué. Sous hello **état du matériel** section, vous pouvez voir que les deux **contrôleur 0** et **contrôleur 1** composants nécessiter une attention.

  ![Échec de la vérification préalable](./media/storsimple-install-troubleshooting/HCS_PreUpdateCheckFailed-include.png)

Vous devez toomake que les deux contrôleurs sont sains et en ligne. Vous devez également toomake que tous les composants matériels de hello dans l’appareil StorSimple hello soient affichée toobe intègre sur la page Maintenance de hello. Vous pouvez ensuite essayer tooinstall les mises à jour. Si vous n’êtes pas les problèmes de composant matériel toofix en mesure de hello, puis vous devez toocontact Support technique de Microsoft pour les étapes suivantes.

**Que se passe-t-il si vous recevez un message d’erreur « Pas pu installer les mises à jour » et hello recommandation est mise à jour de toohello toorefer dépannage guide toodetermine hello cause de l’échec de hello ?**

Une des causes possibles de ce peut être que vous n’avez pas de serveurs de connectivité toohello Microsoft Update. Il s’agit d’une vérification manuelle qui doit toobe effectuée. Si vous perdez le serveur de mise à jour de connectivité toohello, votre tâche de mise à jour échoue. Vous pouvez vérifier la connectivité de hello en hello suivant l’applet de commande à partir de l’interface Windows PowerShell de hello de votre appareil StorSimple en cours d’exécution :

 `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter>`

Exécutez l’applet de commande hello sur les deux contrôleurs.

Si vous avez vérifié la connectivité de hello existe et que les toosee ce problème, contactez le Support technique de Microsoft pour les étapes suivantes.

**Que se passe-t-il si vous consultez un échec de la mise à jour lors de la mise à jour de votre appareil de tooUpdate 4 et les deux contrôleurs hello sont en cours d’exécution 4 de mettre à jour ?**

À partir de mise à jour 4, si les deux contrôleurs hello sont en cours d’exécution hello même version du logiciel et s’il existe un échec de la mise à jour, les contrôleurs hello n’entrez pas en mode de récupération. Cette situation peut survenir si hello correctif logiciel de périphérique (1er mise à jour de commande) est contrôleurs de hello tooboth appliquée avec succès, mais d’autres correctifs (2e et 3e ordre) sont encore toobe appliqué. À partir de mise à jour 4, les contrôleurs hello passera en mode de récupération uniquement si les deux contrôleurs de hello exécutent des versions de logiciels différents. 

Si l’utilisateur de hello détecte un échec de la mise à jour lorsque les deux contrôleurs sont en cours d’exécution mise à jour 4, nous recommandons qu’ils Patientez quelques minutes et recommencez la mise à jour. Si les tentatives de hello n’aboutit pas, ils doivent contacter le Support Microsoft.
