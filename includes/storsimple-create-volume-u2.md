<!--author=alkohli last changed: 08/16/2016-->

#### <a name="toocreate-a-volume"></a>toocreate un volume
1. Sur l’appareil de hello **Quick Start** , cliquez sur **ajouter un volume** toostart hello Assistant Ajout d’un volume.
2. Bonjour Assistant Ajout d’un volume, sous **les paramètres de base**:
   
   1. Saisissez un **nom** pour le volume.
   2. Dans la liste déroulante hello, sélectionnez hello **Type d’utilisation** pour votre volume. Pour les charges de travail qui nécessitent des garanties locales, une faible latence et les meilleures performances possibles, sélectionnez un volume **épinglé localement** . Pour toutes les autres données, sélectionnez un volume **à plusieurs niveaux** . Si vous utilisez ce volume pour les données d’archivage, cochez la case **Utiliser ce volume pour des données d’archivage moins fréquemment sollicitées**. 
      
       Un volume attaché localement est approvisionné et garantit que les données de salutation principal sur le volume de hello restent local toohello appareil et ne pas déborder toohello cloud.  Si vous créez un volume attaché localement, hello de vérification d’espace disponible sur les couches locales hello taille de volume de hello tooprovision Hello demandée. opération Hello de création d’un volume attaché localement peut impliquer le débordement des données existantes à partir de hello appareil toohello cloud et durée hello de volume de hello toocreate peut être longue. durée totale de Hello dépend hello taille du volume de hello configuré, la bande passante réseau disponible et données hello sur votre appareil. 
      
       La configuration d’un volume à plusieurs niveaux est légère, et sa création peut être rapide. En sélectionnant **utiliser ce volume pour les données d’archive moins fréquemment sollicitées** pour le volume hiérarchisé ciblé pour la taille de segment de la déduplication des données d’archivage des modifications hello pour votre volume too512 Ko. Si ce champ n’est pas coché, volume de hiérarchisé correspondant hello utilise une taille de segment de 64 Ko. Une plus grande taille de segment de la déduplication permet de transfert hello tooexpedite des appareils hello du cloud toohello de données d’archivage volumineux.
   3. Spécifiez hello **capacité approvisionnée** pour votre volume. Prenez note de la capacité de hello est disponible selon le type de volume hello sélectionné. Hello spécifié la taille du volume ne doit pas dépasser espace hello.
      
       Vous pouvez configurer les volumes attachés localement des too8.5 To ou des volumes hiérarchisés jusqu'à to too200 sur l’appareil 8100 de hello. Sur l’appareil 8600 supérieure de hello, vous pouvez configurer les volumes attachés localement des too22.5 To ou des volumes hiérarchisés jusqu'à too500 to. Comme espace local sur le périphérique de hello hello requis toohost jeu de travail de volumes hiérarchisés, la création de volumes attachés localement affecte espace hello disponible pour l’approvisionnement des volumes hiérarchisés. Par conséquent, si vous créez un volume épinglé localement, l’espace disponible pour la création de volumes à plusieurs niveaux sera réduit. De même, si vous créez un volume hiérarchisé, espace disponible de hello pour la création de volumes attachés localement est réduite.
      
       Si vous configurez un volume attaché localement de 8,5 To (taille maximale autorisée) sur votre appareil 8100, vous avez épuisé tout hello local l’espace disponible sur le périphérique de hello. Vous ne serez pas en mesure de toocreate n’importe quel volume hiérarchisé que l’espace local sur hello appareil toohost hello plage de travail de hello point, qu’il est hiérarchisé volume. Volumes hiérarchisés existants affectent également les espace hello disponible. Par exemple, si vous avez un appareil 8100 qui possède déjà des volumes à plusieurs niveaux de 106 To, seuls 4 To d’espace sont disponibles pour les volumes épinglés localement.
      
       Hello image suivante montre hello **les paramètres de base** boîte de dialogue pour un volume attaché localement.
      
        ![Ajouter un volume local](./media/storsimple-create-volume-u2/add-local-volume-include.png)
      
       Hello image suivante montre hello **les paramètres de base** boîte de dialogue pour un volume hiérarchisé.
      
        ![Ajouter un volume local](./media/storsimple-create-volume-u2/add-tiered-volume-include.png)
   
   1. Cliquez sur la flèche hello ![icône-flèche](./media/storsimple-create-volume-u2/HCS_ArrowIcon-include.png) page suivante du toohello toogo.
3. Bonjour **des paramètres supplémentaires** boîte de dialogue Ajouter un nouvel enregistrement de contrôle d’accès (ACR) :
   
   1. Saisissez un **Nom** pour votre ACR.
   2. Sous **nom de l’initiateur iSCSI**, fournir hello iSCSI nom qualifié (IQN) de votre hôte Windows. Si vous n’avez pas hello IQN, passez trop[Get hello IQN d’un hôte Windows Server](#get-the-iqn-of-a-windows-server-host).
   3. Sous **sauvegarde par défaut pour ce volume ?**, sélectionnez hello **activer** case à cocher. sauvegarde de Hello par défaut crée une stratégie qui s’exécute à 22 h 30 (heure de l’appareil) quotidiennement et crée un instantané cloud de ce volume.
      
      > [!NOTE]
      > Une fois la sauvegarde de hello est activée ici, il ne peut pas être annulée. Vous devez tooedit hello volume toomodify ce paramètre.
      > 
      > 
      
      ![Ajouter un volume](./media/storsimple-create-volume-u2/AddVolumeAdditionalSettings1.png)
4. Cliquez sur une icône de coche hello ![icône en forme de coche](./media/storsimple-create-volume-u2/HCS_CheckIcon-include.png). Création d’un volume avec hello spécifié les paramètres.

