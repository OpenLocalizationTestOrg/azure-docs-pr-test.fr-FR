<!--author=alkohli last changed: 07/07/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a>tooinstall une mise à jour à partir de hello portail Azure

1. Sur la page du service StorSimple hello, sélectionnez votre appareil.

    ![Sélectionnez l’appareil](./media/storsimple-8000-install-update4-via-portal/update1.png)

2. Accédez trop**paramètres de périphérique** > **mises à jour de l’appareil**.

    ![Cliquez sur Mises à jour de l’appareil](./media/storsimple-8000-install-update4-via-portal/update2.png)

2. Une notification s’affiche si de nouvelles mises à jour sont disponibles. Également, dans hello **mises à jour de l’appareil** panneau, cliquez sur **d’analyse des mises à jour**. Un travail est créé tooscan mises à jour disponibles. Vous êtes averti lorsque la fin du travail hello.

    ![Cliquez sur Mises à jour de l’appareil](./media/storsimple-8000-install-update4-via-portal/update3.png)

3. Nous vous recommandons de consulter les notes de publication hello avant d’appliquer une mise à jour sur votre appareil. Cliquez sur les mises à jour de tooapply, **installer les mises à jour**. Bonjour **confirmer les mises à jour régulières** panneau, révision hello conditions préalables toocomplete avant d’appliquer les mises à jour. Sélectionnez tooindicate de case à cocher hello que vous tooupdate prêt hello du périphérique, puis sur **installer**.

    ![Cliquez sur Mises à jour de l’appareil](./media/storsimple-8000-install-update4-via-portal/update4.png)

6. Un ensemble de vérifications préalables démarre. Ces vérifications incluent :
   
   * **Contrôles d’intégrité de contrôleur** tooverify que les deux hello contrôleurs d’appareil sont sains et en ligne.
   * **Contrôles d’intégrité de composant matériel** tooverify que tous les hello des composants matériels de votre appareil StorSimple sont intègres.
   * **DATA 0 vérifie** tooverify que DATA 0 est activé sur votre appareil. Si cette interface n’est pas activée, vous devez l’activer, puis réessayer.

    mise à jour Hello est téléchargé et installé uniquement si toutes les vérifications de hello sont correctement terminées. Vous êtes averti lorsque des vérifications de hello sont en cours d’exécution. Si hello prechecks échouent, vous êtes fourni avec les raisons pour lesquelles les hello. Répondre à ces problèmes, puis recommencez les opération hello. Vous devrez peut-être toocontact Support technique de Microsoft si vous ne pouvez pas résoudre ces problèmes vous-même.

7. Une fois hello prechecks sont correctement effectués, création d’un travail de mise à jour. Vous êtes averti lorsque la tâche de mise à jour hello est créée.
   
    ![Création de la tâche de mise à jour](./media/storsimple-8000-install-update4-via-portal/update6.png)
   
    mise à jour Hello est ensuite appliqué sur votre appareil.

9. mise à jour Hello prend quelques heures toocomplete. Sélectionnez la tâche de mise à jour hello et cliquez sur **détails** tooview les détails de hello du travail hello à tout moment.

    ![Création de la tâche de mise à jour](./media/storsimple-8000-install-update4-via-portal/update8.png)

     Vous pouvez également surveiller hello progression du travail de mise à jour hello à partir de **paramètres du périphérique > travaux**. Sur hello **travaux** panneau, vous pouvez voir hello mettre à jour de progression.

     ![Création de la tâche de mise à jour](./media/storsimple-8000-install-update4-via-portal/update7.png)

10. Une fois le travail de hello est terminée, accédez à toohello **paramètres du périphérique > mises à jour de l’appareil**. version du logiciel Hello doit maintenant être mis à jour.

    ![Création de la tâche de mise à jour](./media/storsimple-8000-install-update4-via-portal/update9.png)

