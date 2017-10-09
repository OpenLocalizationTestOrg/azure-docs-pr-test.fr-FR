#### <a name="toocreate-a-new-service"></a>toocreate un nouveau service

1.  Vos informations d’identification de compte Microsoft, ouvrez une session toohello portail Azure à cette URL : <https://portal.azure.com/>. Si vous déployez un appareil hello dans le portail d’administration, connectez-vous à l’adresse : <https://portal.azure.us/>

2.  Bonjour portail Azure, cliquez sur **+ nouveau** &gt; **stockage** &gt; **série virtuel de StorSimple**.

    ![Créer un nouveau service](./media/storsimple-virtual-array-create-new-service/createnewservice2.png) 

3.  Bonjour **le Gestionnaire de périphériques StorSimple** panneau s’ouvre, procédez comme hello suivant :

    1.  Fournissez un unique **Nom de la ressource** pour votre service. nom de la ressource Hello est un nom convivial qui peut être utilisé tooidentify hello service. nom de Hello peut compter entre 2 et 50 caractères qui peuvent être des lettres, des chiffres et des traits d’union. Hello doit commencer et se terminer par une lettre ou un chiffre.

    2.  Choisissez un **abonnement** à partir de la liste déroulante de hello. l’abonnement Hello est lié tooyour compte de facturation. Ce champ n’est pas présent si vous n’avez qu’un seul abonnement.

    3.  Pour le **Groupe de ressources**, sélectionnez un groupe existant ou créez-en un. Pour plus d’informations, consultez la page [Groupes de ressources dans Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).

    4.  Indiquez un **emplacement** pour votre service. Pour plus d’informations sur les services disponibles dans chaque région, consultez la page [Régions Azure](https://azure.microsoft.com/regions/#services). En général, choisissez un **emplacement** le plus proche toohello géographique où vous souhaitez toodeploy votre appareil. Vous pouvez également toofactor suivante de hello :

        -   Si vous avez des charges de travail existantes dans Azure que vous envisagez également toodeploy avec votre appareil StorSimple, nous vous recommandons d’utiliser ce centre de données.

        -   Le gestionnaire d’appareil StorSimple et le stockage Azure peuvent se trouver en deux emplacements différents. Dans ce cas, vous êtes séparément de toocreate requis hello StorSimple le Gestionnaire de périphériques et le compte de stockage Azure. toocreate un compte de stockage Azure, passez le service de stockage Azure toohello Bonjour portail Azure et suivez les étapes de hello dans [créer un compte Azure Storage](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/#create-a-storage-account). Après avoir créé ce compte, ajoutez-le service du Gestionnaire de périphériques StorSimple toohello en suivant les étapes de hello dans [configurer un nouveau compte de stockage pour le service de hello](https://azure.microsoft.com/en-us/documentation/articles/storsimple-deployment-walkthrough/#configure-a-new-storage-account-for-the-service).

        -   Si vous déployez un appareil virtuel hello Bonjour gouvernement Portal, hello service du Gestionnaire de périphériques StorSimple est disponible dans les emplacements de Iowa nous et nous Virginie.

    5.  Sélectionnez **créer un nouveau compte de stockage Azure** tooautomatically créer un compte de stockage avec le service de hello. Spécifiez un **Nom du compte de stockage**. Si vous avez besoin de vos données dans un autre emplacement, désactivez cette case à cocher.

    6.  Vérifiez **toodashboard du code confidentiel** si vous souhaitez un service de toothis lien rapide sur votre tableau de bord.

    7.  Cliquez sur **créer** toocreate hello StorSimple le Gestionnaire de périphériques.

        ![Créer un nouveau service](./media/storsimple-virtual-array-create-new-service/createnewservice4.png)  

Vous êtes dirigé toohello **Service** page d’accueil. la création du service Hello prend quelques minutes. Une fois hello service est correctement créé, vous recevrez une notification quand et état de hello du service de hello devient trop**Active**.


