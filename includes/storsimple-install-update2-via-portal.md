<!--author=alkohli last changed: 02/06/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a>tooinstall une mise à jour à partir de hello portail Azure

1. Sur la page du service StorSimple hello, sélectionnez votre appareil. Accédez trop**périphériques** > **Maintenance**.
2. Au bas de hello de page de hello, cliquez sur **d’analyse des mises à jour**. Un travail est créé tooscan mises à jour disponibles. Vous êtes averti lorsque la fin du travail hello.
3. Bonjour **mises à jour logicielles** section hello même page, les mises à jour logicielles nouveau hello sont disponibles. Nous vous recommandons de consulter les notes de publication hello avant d’appliquer une mise à jour sur votre appareil.
4. Au bas de hello de page de hello, cliquez sur **installer les mises à jour**, puis **OK**.
5. Bonjour **installer les mises à jour** boîte de dialogue, assurez-vous que vous avez suivi les recommandations de hello, puis sélectionnez **je hello ci-dessus impératif de comprendre et suis prêt tooupgrade mon appareil** et cliquez sur vérifier de hello bouton.
   
    ![Message de confirmation](./media/storsimple-install-update2-via-portal/InstallUpdate12_2M.png)
6. Un ensemble de vérifications préalables démarre. Ces vérifications incluent :
   
   * **Contrôles d’intégrité de contrôleur** tooverify que les deux hello contrôleurs d’appareil sont sains et en ligne.
   * **Contrôles d’intégrité de composant matériel** tooverify que tous les hello des composants matériels de votre appareil StorSimple sont intègres.
   * **DATA 0 vérifie** tooverify que DATA 0 est activé sur votre appareil. Si cette interface n’est pas activée, vous devez l’activer, puis réessayer.
   * **DATA 2 et DATA 3 vérifications** tooverify que les interfaces réseau DATA 2 et DATA 3 ne sont pas activés. Si ces interfaces sont activées, puis vous devez désactiver ces de tooupdate votre appareil. Cette vérification est effectuée uniquement si vous mettez à jour un appareil exécutant un logiciel de disponibilité générale. Les appareils exécutant les versions 0.1, 0.2 ou 0.3 ne sont pas soumis à cette vérification.
   * **Vérification de la passerelle** sur n’importe quel appareil exécutant une tooUpdate préalable de version 1. Cette vérification est effectuée sur tous les périphériques hello exécutant le logiciel avant mise à jour 1, mais échoue sur les appareils hello qui ont une passerelle est configurée pour une interface réseau autres que DATA 0.
     
     mise à jour de Hello est appliquée si toutes les vérifications sont terminées avec succès. Vous êtes averti lorsque des vérifications de hello sont en cours d’exécution.
     
     ![Notification de la vérification préalable](./media/storsimple-install-update2-via-portal/InstallUpdate12_3M.png)
     
     Hello Voici un exemple dans lequel échec des vérifications de hello. Vous devez vérifier que les deux contrôleurs de périphérique hello sont sains et en ligne. Vous devez également l’intégrité de hello toocheck des composants matériels de hello. Dans cet exemple, les composants Contrôleur 0 et Contrôleur 1 méritent attention. Vous devrez peut-être toocontact Support technique de Microsoft si vous ne pouvez pas résoudre ces problèmes vous-même.
     
       ![Les vérifications ont échoué](./media/storsimple-install-update2-via-portal/HCS_PreUpgradeChecksFailed-include.png)
7. Une fois que les vérifications de hello sont correctement effectuées, création d’un travail de mise à jour. Vous êtes averti lorsque la tâche de mise à jour hello est créée.
   
    ![Création de la tâche de mise à jour](./media/storsimple-install-update2-via-portal/InstallUpdate12_44M.png)
   
    mise à jour Hello est ensuite appliqué sur votre appareil.
    
8. progression de hello toomonitor de tâche de mise à jour de hello, cliquez sur **afficher le travail**. Sur hello **travaux** page, vous pouvez voir hello mettre à jour de progression.
9. mise à jour Hello prend quelques heures toocomplete. Sélectionnez la tâche de mise à jour hello et cliquez sur **détails** tooview les détails de hello du travail hello à tout moment.
10. Une fois le travail de hello est terminée, accédez à toohello **Maintenance** page et faites défiler trop**mises à jour logicielles**.

