<!--author=alkohli last changed:02/10/2017-->


#### <a name="toocreate-a-new-service"></a>toocreate un nouveau service

1. Utilisez votre toolog d’informations d’identification de compte Microsoft sur toohello [portail Azure](https://portal.azure.com/).

2. Bonjour portail Azure, cliquez sur  **+**  dans marketplace de hello, cliquez sur **afficher tous les**.

    ![Créer StorSimple Device Manager](./media/storsimple-8000-create-new-service/createssdevman1.png)

    Recherchez _StorSimple physique_. Sélectionnez **Série d’appareils physiques StorSimple** et cliquez dessus, puis cliquez sur **Créer**. Vous pouvez également, dans hello portail Azure, cliquez sur  **+**  puis, sous **stockage**, cliquez sur **série d’appareils physiques StorSimple**.

    ![Créer StorSimple Device Manager](./media/storsimple-8000-create-new-service/createssdevman11.png)

3. Bonjour **le Gestionnaire de périphériques StorSimple** panneau, hello comme suit :
   
   1. Fournissez un unique **Nom de la ressource** pour votre service. Ce nom est un nom convivial qui peut être utilisé tooidentify hello service. nom de Hello peut compter entre 2 et 50 caractères qui peuvent être des lettres, des chiffres et des traits d’union. Hello doit commencer et se terminer par une lettre ou un chiffre.

   2. Choisissez un **abonnement** à partir de la liste déroulante de hello. l’abonnement Hello est lié tooyour compte de facturation. Ce champ n’est pas présent si vous n’avez qu’un seul abonnement.

   3. Pour le **Groupe de ressources**, sélectionnez un groupe existant en cliquant sur **Utiliser existant** ou créez-en un avec l’option **Créer**. Pour plus d’informations, consultez la page [Groupes de ressources dans Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).
   
   4. Indiquez un **emplacement** pour votre service. En général, choisissez une emplacement le plus proche toohello région géographique où vous souhaitez toodeploy votre appareil. Vous pouvez également toofactor Bonjour suivant considérations : 
      
      * Si vous avez des charges de travail existantes dans Azure que vous envisagez également toodeploy avec votre appareil StorSimple, vous devez utiliser ce centre de données.
      * Votre service StorSimple Device Manager et le stockage Azure peuvent se trouver dans deux emplacements différents. Dans ce cas, vous êtes séparément de toocreate requis hello StorSimple le Gestionnaire de périphériques et le compte de stockage Azure. toocreate un compte de stockage Azure, passez le service de stockage Azure toohello Bonjour portail Azure et suivez les étapes de hello dans [créer un compte Azure Storage](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account). Après avoir créé ce compte, ajoutez-le service du Gestionnaire de périphériques StorSimple toohello en suivant les étapes de hello dans [configurer un nouveau compte de stockage pour le service de hello](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service).

   5. Sélectionnez **créer un nouveau compte de stockage** tooautomatically créer un compte de stockage avec le service de hello. Spécifiez un nom pour ce compte de stockage. Si vous avez besoin de vos données dans un autre emplacement, désactivez cette case à cocher.

   6. Vérifiez **toodashboard du code confidentiel** si vous souhaitez un service de toothis lien rapide sur votre tableau de bord.
      
   7. Cliquez sur **créer** toocreate hello StorSimple le Gestionnaire de périphériques.

       ![Créer StorSimple Device Manager](./media/storsimple-8000-create-new-service/createssdevman2.png)
   
la création du service Hello prend quelques minutes. Une fois que le service de hello est correctement créé, vous voyez une notification et nouveau panneau de service hello s’ouvre.
   
![Créer StorSimple Device Manager](./media/storsimple-8000-create-new-service/createssdevman5.png)


