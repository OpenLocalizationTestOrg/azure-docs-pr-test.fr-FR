<!--author=SharS last changed: 02/04/2016-->

#### <a name="toocreate-a-volume"></a>toocreate un volume
1. Sur l’appareil de hello **Quick Start** , cliquez sur **ajouter un volume**. Cette commande démarre hello Assistant Ajout d’un volume.
2. Bonjour Assistant Ajout d’un volume, sous **les paramètres de base**, hello suivant :
   
   1. Saisissez un **nom** pour le volume.
   2. Spécifiez hello **capacité approvisionnée** pour votre volume en Go ou to. capacité du volume Hello doit être comprise entre 1 et 64 To pour un périphérique physique.
   3. Dans la liste déroulante hello, sélectionnez hello **Type d’utilisation** pour votre volume. 
   4. Si vous utilisez ce volume de données d’archivage, sélectionnez hello **utiliser ce volume pour les données d’archive moins fréquemment sollicitées** case à cocher. Dans tous les autres cas, sélectionnez **Volume à plusieurs niveaux**. (Les volumes à plusieurs niveaux étaient appelés volumes principaux).
      
        ![Ajouter un volume](./media/storsimple-create-volume/ScreenshotUpdate1VolumeFlow.png)
      
      1. Cliquez sur la flèche hello ![icône-flèche](./media/storsimple-create-volume/HCS_ArrowIcon-include.png) page suivante du toohello toogo.
3. Bonjour **des paramètres supplémentaires** boîte de dialogue Ajouter un nouvel enregistrement de contrôle d’accès (ACR) :
   
   1. Saisissez un **Nom** pour votre ACR.
   2. Sous **nom de l’initiateur iSCSI**, fournir hello iSCSI nom qualifié (IQN) de votre hôte Windows. Si vous n’avez pas hello IQN, passez trop[Get hello IQN d’un hôte Windows Server](#get-the-iqn-of-a-windows-server-host).
   3. Nous vous recommandons d’activer une sauvegarde par défaut en sélectionnant hello **activer une sauvegarde par défaut pour ce volume** case à cocher. sauvegarde par défaut de Hello créera une stratégie qui s’exécute à 22 h 30 (heure de l’appareil) quotidiennement et crée un instantané cloud de ce volume.
      
      > [!NOTE]
      > Une fois la sauvegarde de hello est activée ici, il ne peut pas être annulée. Vous devez tooedit hello volume toomodify ce paramètre.
      > 
      > 
      
        ![Ajouter un volume](./media/storsimple-create-volume/AddVolume2-include.png)
4. Cliquez sur une icône de coche hello ![icône en forme de coche](./media/storsimple-create-volume/HCS_CheckIcon-include.png). Un volume est créé par hello spécifié les paramètres.

![Vidéo disponible](./media/storsimple-create-volume/Video_icon.png)**Vidéo disponible**

toowatch une vidéo qui montre comment toocreate un volume StorSimple, cliquez sur [ici](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/).

