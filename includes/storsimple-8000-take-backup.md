<!--author=alkohli last changed: 01/12/17-->

### <a name="tootake-a-backup"></a>tootake une sauvegarde

1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour. À partir de hello tabulaire la liste des périphériques, sélectionnez et cliquez sur votre appareil, puis cliquez **tous les paramètres**. Bonjour **paramètres** panneau, accédez trop**Paramètres > Gérer > stratégie de sauvegarde**.

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu1.png)

2. Bonjour **stratégie de sauvegarde** panneau, cliquez sur **+ ajouter une stratégie**.

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu2.png)

3. Bonjour **créer la stratégie de sauvegarde** panneau, fournissez un nom qui contient entre 3 et 150 caractères pour votre stratégie de sauvegarde.

4. Sélectionnez toobe de volumes hello sauvegardé. Si vous sélectionnez plusieurs volumes, ces volumes sont toocreate ensemble groupée une sauvegarde avec cohérence d’incident.

    ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu4.png)

5. Dans le panneau **Ajouter la première planification** :

    1. Sélectionnez le type hello de sauvegarde. Pour une restauration plus rapide, sélectionnez Instantané **local**. Pour la résilience des données, sélectionnez Instantané **cloud**.
    2. Spécifiez la fréquence de sauvegarde hello en minutes, heures, jours ou semaines.
    3. Sélectionnez une durée de conservation. choix de rétention Hello dépend de la fréquence de sauvegarde hello. Par exemple, pour une stratégie quotidienne, rétention de hello peut être spécifiée en semaines, tandis que la rétention pour une stratégie mensuelle est en mois.
    4. Sélectionnez hello à partir des date et heure pour la stratégie de sauvegarde hello.
    5. Cliquez sur **OK** stratégie de sauvegarde toocreate hello.

        ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu5.png) 

6. Cliquez sur **créer** la création de stratégie de sauvegarde toostart hello. Vous êtes averti lorsque la stratégie de sauvegarde hello est créé avec succès. Hello liste des stratégies de sauvegarde est également mise à jour.
      
      ![Add-backup-policy](./media/storsimple-8000-take-backup/step8takebu9.png)
      
      Vous disposez maintenant d’une stratégie de sauvegarde, qui crée des sauvegardes planifiées des données de volume.




