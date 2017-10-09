<!--author=alkohli last changed: 07/19/2017-->

#### <a name="toocreate-a-volume"></a>toocreate un volume
1. À partir de hello tableau qui répertorie les périphériques hello Bonjour **périphériques** panneau, sélectionnez votre appareil. Cliquez sur **+ Ajouter un volume**.

    ![Ajouter un volume](./media/storsimple-8000-create-volume-u2/step5createvol1.png)

2. Bonjour **ajouter un volume** panneau :
   
   1. Hello **périphérique** est automatiquement renseigné avec votre appareil.

   2. À partir de la liste déroulante hello, sélectionnez le conteneur de volume hello où vous avez besoin d’un volume de tooadd. 

   3.  Saisissez un **nom** pour le volume. Vous ne pouvez pas renommer un volume une fois que le volume hello est créé.

   4. Dans la liste déroulante hello, sélectionnez hello **Type** pour votre volume. Pour les charges de travail qui nécessitent des garanties locales, une faible latence et les meilleures performances possibles, sélectionnez un volume **épinglé localement** . Pour toutes les autres données, sélectionnez un volume **à plusieurs niveaux** . Si vous utilisez ce volume pour les données d’archivage, cochez la case **Utiliser ce volume pour des données d’archivage moins fréquemment sollicitées**.
      
       La configuration d’un volume à plusieurs niveaux est légère, et sa création peut être rapide. En sélectionnant **utiliser ce volume pour les données d’archive moins fréquemment sollicitées** pour le volume hiérarchisé ciblé pour la taille de segment de la déduplication des données d’archivage des modifications hello pour votre volume too512 Ko. Si ce champ n’est pas coché, volume de hiérarchisé correspondant hello utilise une taille de segment de 64 Ko. Une plus grande taille de segment de la déduplication permet de transfert hello tooexpedite des appareils hello du cloud toohello de données d’archivage volumineux.
       
       Un volume attaché localement est approvisionné et garantit que les données de salutation principal sur le volume de hello restent local toohello appareil et ne pas déborder toohello cloud.  Si vous créez un volume attaché localement, hello de vérification d’espace disponible sur les couches locales hello taille de volume de hello tooprovision Hello demandée. opération Hello de création d’un volume attaché localement peut impliquer le débordement des données existantes à partir de hello appareil toohello cloud et durée hello de volume de hello toocreate peut être longue. durée totale de Hello dépend hello taille du volume de hello configuré, la bande passante réseau disponible et données hello sur votre appareil.

   5. Spécifiez hello **capacité approvisionnée** pour votre volume. Prenez note de la capacité de hello est disponible selon le type de volume hello sélectionné. Hello spécifié la taille du volume ne doit pas dépasser espace hello.
      
       Vous pouvez configurer les volumes attachés localement des too8.5 To ou des volumes hiérarchisés jusqu'à to too200 sur l’appareil 8100 de hello. Sur l’appareil 8600 supérieure de hello, vous pouvez configurer les volumes attachés localement des too22.5 To ou des volumes hiérarchisés jusqu'à too500 to. Comme espace local sur le périphérique de hello hello requis toohost jeu de travail de volumes hiérarchisés, la création de volumes attachés localement affecte espace hello disponible pour l’approvisionnement des volumes hiérarchisés. Par conséquent, si vous créez un volume épinglé localement, l’espace disponible pour la création de volumes à plusieurs niveaux est réduit. De même, si vous créez un volume hiérarchisé, espace disponible de hello pour la création de volumes attachés localement est réduite.
      
       Si vous configurez un volume attaché localement de 8,5 To (taille maximale autorisée) sur votre appareil 8100, vous avez épuisé tout hello local l’espace disponible sur le périphérique de hello. Impossible de créer un volume à plusieurs niveaux à partir de ce point, car il n’existe aucun espace local sur hello appareil toohost hello plage de travail de hello à plusieurs niveaux de volume. Volumes hiérarchisés existants affectent également les espace hello disponible. Par exemple, si vous avez un appareil 8100 qui possède déjà des volumes à plusieurs niveaux de 106 To, seuls 4 To d’espace sont disponibles pour les volumes épinglés localement.

    6. Bonjour **connecté des ordinateurs hôtes** , cliquez sur la flèche de hello. 

        ![Hôtes connectés](./media/storsimple-8000-create-volume-u2/step5createvol2.png)

    7. Bonjour **connecté des ordinateurs hôtes** panneau, choisissez un ACR existant ou ajouter un nouvel ACR en effectuant hello comme suit :

       1. Saisissez un **Nom** pour votre ACR.
       2. Sous **nom de l’initiateur iSCSI**, fournir hello iSCSI nom qualifié (IQN) de votre hôte Windows. Si vous n’avez pas hello IQN, passez trop[Get hello IQN d’un hôte Windows Server](#get-the-iqn-of-a-windows-server-host).

    9. Cliquez sur **Créer**. Création d’un volume avec hello spécifié les paramètres.

        ![Click Create](./media/storsimple-8000-create-volume-u2/step5createvol3.png)

        > [!NOTE]
        > N’oubliez pas que le volume hello que vous avez créé ici n’est pas protégé. Vous devez toocreate et associer les stratégies de sauvegarde avec des sauvegardes tootake planifiée de ce volume. 

