## <a name="defining-a-backup-policy"></a>Définition d’une stratégie de sauvegarde
Une stratégie de sauvegarde définit une matrice de lorsque hello données instantanés et la durée de conservation de ces instantanés. Lors de la définition de la stratégie de sauvegarde d’une machine virtuelle, vous pouvez déclencher un travail de sauvegarde *une fois par jour*. Lorsque vous créez une nouvelle stratégie, il est appliqué toohello coffre. interface de stratégie de sauvegarde Hello ressemble à ceci :

![Stratégie de sauvegarde](./media/backup-create-policy-for-vms/backup-policy.png)

toocreate une stratégie :

1. Entrez un nom pour hello **nom de la stratégie**.
2. Les instantanés de vos données peuvent être pris à intervalles quotidiens ou hebdomadaires. Hello d’utilisation **fréquence de sauvegarde** menu déroulant toochoose si données instantanés quotidienne ou hebdomadaire.
   
   * Si vous choisissez un intervalle quotidien, utilisez hello mis en surbrillance contrôle tooselect hello heure hello pour la capture instantanée de hello. heure de hello toochange, désélectionnez les heures hello et sélectionnez hello nouvelle heure.
     
     ![Stratégie de sauvegarde quotidienne](./media/backup-create-policy-for-vms/backup-policy-daily.png) <br/>
   * Si vous choisissez un intervalle hebdomadaire, utilisez hello contrôles en surbrillance tooselect hello ou les jours de semaine de hello et l’heure de hello de capture instantanée de jour tootake hello. Dans le menu du jour hello, sélectionnez un ou plusieurs jours. Dans le menu d’heure hello, sélectionnez une heure. heure de hello toochange, désélectionnez horaire sélectionnée de hello et sélectionnez hello nouvelle heure.
     
     ![Stratégie de sauvegarde hebdomadaire](./media/backup-create-policy-for-vms/backup-policy-weekly.png)
3. Par défaut, toutes les options **Durée de rétention** sont sélectionnées. Décochez la case aucune limite de plage de rétention vous ne souhaitez pas toouse. Ensuite, spécifiez hello interval(s) toouse.
   
    Mensuel ou annuel de plages de rétention permettent de captures instantanées de hello toospecify basées sur un incrément hebdomadaire ou quotidien.
   
   > [!NOTE]
   > Lorsque vous protégez un ordinateur virtuel, un travail de sauvegarde s'exécute une fois par jour. heure de Hello lorsque sauvegarde s’exécute de hello est même hello pour chaque plage de rétention.
   > 
   > 
4. Après avoir défini toutes les options de stratégie de hello, en haut de hello du panneau des hello, cliquez sur **enregistrer**.
   
    Hello nouvelle stratégie est appliquée immédiatement toohello coffre.

