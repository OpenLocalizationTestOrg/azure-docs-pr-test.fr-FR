<!--author=alkohli last changed: 06/22/17-->

#### <a name="toocreate-a-volume-container"></a>toocreate un conteneur de volume
1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour et cliquez sur **périphériques**. Hello tabulaire liste des périphériques de hello, sélectionnez et cliquez sur l’appareil. 

    ![Panneau du conteneur de volumes](./media/storsimple-8000-create-volume-container/createvolumecontainer1.png)

2. Dans le tableau de bord du périphérique hello, cliquez sur **+ ajouter volume conteneur**

    ![Panneau du conteneur de volumes](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

3. Bonjour **conteneur de volume ajouter** panneau :
   
   1. Hello périphérique est automatiquement sélectionné.
   2. Saisissez un **Nom** pour votre conteneur de volume. nom de Hello doit comporter 3 caractères too32. Vous ne pouvez pas renommer un conteneur de volumes une fois qu’il a été créé.
   3. Sélectionnez **activer le chiffrement de stockage du Cloud** tooenable le chiffrement de données hello envoyés à partir de hello appareil toohello cloud.
   4. Entrez et confirmez un **clé de chiffrement de stockage Cloud** c'est-à-dire 8 too32 caractères. Cette clé est utilisée par les données tooaccess chiffré de l’appareil hello.
   5. Sélectionnez un **compte de stockage** tooassociate avec ce conteneur de volume. Vous pouvez choisir un compte de stockage existant ou un compte par défaut hello qui est généré lors de la création du service hello. Vous pouvez également utiliser hello **ajouter un nouveau** option toospecify un compte de stockage qui n’est pas lié toothis abonnement au service.
   6. Sélectionnez **illimité** Bonjour **spécifier la bande passante** liste déroulante, si vous le souhaitez tooconsume toute la bande passante disponible hello. Vous pouvez également définir cette option trop**personnalisé** tooemploy des contrôles de bande passante et spécifiez une valeur comprise entre 1 et 1 000 Mbps.
      Si vous disposez de vos informations d’utilisation de la bande passante disponibles, vous pouvez être la bande passante en mesure de tooallocate selon une planification en spécifiant **sélectionner un modèle de bande passante**. Pour une procédure pas à pas, consultez trop[ajouter un modèle de bande passante](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).

      ![Panneau du conteneur de volumes](./media/storsimple-8000-create-volume-container/createvolumecontainer6b.png)
   7. Cliquez sur **Create**.

        ![Panneau du conteneur de volumes](./media/storsimple-8000-create-volume-container/createvolumecontainer6.png)
   
       Vous êtes averti lorsque le conteneur de volume hello est créé avec succès.

       ![Notification de la création du conteneur de volumes](./media/storsimple-8000-create-volume-container/createvolumecontainer8.png)

   Hello créé le conteneur de volume est répertorié dans la liste hello des conteneurs de volumes pour votre appareil.

   ![Panneau Ajouter un conteneur de volumes](./media/storsimple-8000-create-volume-container/createvolumecontainer9.png)


