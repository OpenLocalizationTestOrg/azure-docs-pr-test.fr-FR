## <a name="log-in-toohello-azure-portal"></a>Ouvrez une session dans toohello portail Azure

Connectez-vous à toohello [portail Azure](https://portal.azure.com/).

## <a name="create-a-blank-sql-database-using-hello-azure-portal"></a>Créer une base de données SQL vide à l’aide de hello portail Azure

Une base de données SQL Azure est créée avec un ensemble défini de [ressources de calcul et de stockage](../articles/sql-database/sql-database-service-tiers.md). base de données Hello est créé dans un [groupe de ressources Azure](../articles/azure-resource-manager/resource-group-overview.md) et dans un [serveur logique de base de données SQL Azure](../articles/sql-database/sql-database-features.md). 

Suivez ces étapes de toocreate une base de données SQL vide. 

1. Cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.

2. Sélectionnez **bases de données** de hello **nouveau** page, puis sélectionnez **base de données SQL** de hello **bases de données** page. 

   ![créer une base de données vide](../articles/sql-database/media/sql-database-design-first-database/create-empty-database.png)

3. Rempliront hello de base de données SQL avec hello suivant d’informations, comme indiqué dans le hello précédant l’image :   

   | Paramètre | Valeur suggérée | Description |
   | --------| --------------- | ----------- | 
   | **Nom de la base de données** | mySampleDatabase | Pour les noms de base de données valides, consultez [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificateurs de base de données). | 
   | **Abonnement** | Votre abonnement  | Pour plus d’informations sur vos abonnements, consultez [Abonnements](https://account.windowsazure.com/Subscriptions). |
   | **Groupe de ressources** | myResourceGroup | Pour les noms de groupe de ressources valides, consultez [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Conventions d’affectation de nom). |
   | **Sélectionner une source** | Base de données vide | Indique qu’une base de données vide doit être créée. |
   ||||

4. Cliquez sur **Server** toocreate et configurer un nouveau serveur pour votre nouvelle base de données. Remplir hello **nouveau formulaire serveur** avec hello informations suivantes : 

   | Paramètre | Valeur suggérée | Description |
   | --------| --------------- | ----------- | 
   | **Nom du serveur** | Nom globalement unique. | Pour les noms de serveur valides, consultez [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Conventions d’affectation de nom). | 
   | **Connexion d’administrateur du serveur** | Nom valide. | Pour les noms de connexion valides, consultez [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificateurs de base de données).|
   | **Mot de passe** | Mot de passe valide. | Votre mot de passe doit comporter au moins huit caractères et contenir des caractères appartenant à trois des hello suivant des catégories : les caractères majuscules, caractères en minuscules, des chiffres et des caractères non alphanumériques. |
   | **Emplacement** | Emplacement valide. | Pour plus d’informations sur les régions, consultez [Régions Azure](https://azure.microsoft.com/regions/). |
   ||||

   ![create database-server](../articles/sql-database/media/sql-database-design-first-database/create-database-server.png)

5. Cliquez sur **Sélectionner**.

6. Cliquez sur **niveau tarifaire** toospecify hello performances et la couche de niveau de service pour votre nouvelle base de données. Pour ce didacticiel, sélectionnez **20 DTU** et **250** Go de stockage.

   ![create database-s1](../articles/sql-database/media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. Cliquez sur **Apply**.  

8. Sélectionnez un **classement** pour la base de données vide hello (pour ce didacticiel, utiliser la valeur par défaut hello). Pour en savoir plus sur les classements, voir [Classements](https://docs.microsoft.com/sql/t-sql/statements/collations)

9. Cliquez sur **créer** base de données tooprovision hello. Approvisionnement prend sur un toocomplete une minute et demie. 

10. Dans la barre d’outils de hello, cliquez sur **Notifications** processus de déploiement toomonitor hello.

   ![notification](../articles/sql-database/media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule-using-hello-azure-portal"></a>Créer une règle de pare-feu de niveau serveur à l’aide de hello portail Azure

Hello service de base de données SQL crée un pare-feu au niveau serveur hello. Initialement le pare-feu hello empêche les outils externes et les applications de se connecter toohello server ou tooany des bases de données sur le serveur de hello. Les connexions sont autorisées après avoir créé une règle de pare-feu tooopen des adresses IP spécifiques. Suivez ces étapes toocreate un [règle de pare-feu de niveau serveur de base de données SQL](../articles/sql-database/sql-database-firewall-configure.md) pour l’adresse IP de votre client et tooenable une connectivité externe via le pare-feu de base de données SQL hello pour votre adresse IP uniquement. 


> [!NOTE]
> Azure SQL Database communique par le biais du port 1433. Vous pouvez vous connecter tooSQL de base de données uniquement après que le pare-feu de votre réseau hello autorise le trafic sortant via le port 1433.


1. Une fois le déploiement de hello terminé, cliquez sur **bases de données SQL** de menu à gauche hello, puis cliquez sur **mySampleDatabase** sur hello **bases de données SQL** page. nom de serveur complet Hello page Vue d’ensemble de votre base de données ouvre, affichant vous hello entièrement (tel que **mynewserver20170313.database.windows.net**) et fournit des options de configuration supplémentaire. Copiez ce nom de serveur complet pour une utilisation ultérieure.

   > [!IMPORTANT]
   > Vous avez besoin de ce serveur complet nom tooconnect tooyour ses bases de données et dans les Démarrages rapides suivants.
   > 

   ![nom du serveur](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 

2. Cliquez sur **définir serveur pare-feu** barre d’outils hello comme indiqué dans l’image précédente de hello. Hello **des paramètres de pare-feu** page serveur de base de données SQL hello s’ouvre. 

   ![règle de pare-feu de serveur](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png) 


3. Cliquez sur **ajouter l’adresse IP du client** sur tooadd de barre d’outils hello votre adresse IP actuelle d’adresses tooa nouvelle règle de pare-feu. Une règle de pare-feu peut ouvrir le port 1433 pour une seule adresse IP ou une plage d’adresses IP.

4. Cliquez sur **Enregistrer**. Une règle de pare-feu de niveau serveur est créée pour votre adresse IP actuelle, ouvrir le port 1433 sur le serveur logique de hello.

   ![définir la règle de pare-feu de serveur](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. Cliquez sur **OK** , puis fermez hello **des paramètres de pare-feu** page.

Vous pouvez désormais connecter le serveur de base de données SQL Azure toohello et ses bases de données à l’aide d’un outil tel que SQL Server Management Studio (SSMS). connexion de Hello est à partir de cette adresse IP, et il utilise le compte d’administrateur de serveur hello créé précédemment.


> [!IMPORTANT]
> Par défaut, l’accès via le pare-feu de base de données SQL hello est activé pour tous les services Azure. Cliquez sur **OFF** sur toodisable de cette page pour tous les services Azure.


## <a name="get-connection-string-values-using-hello-azure-portal"></a>Obtenir les valeurs de chaîne de connexion à l’aide de hello portail Azure

Obtenir le nom du serveur complet hello pour votre serveur de base de données SQL Azure Bonjour portail Azure. Vous utilisez hello complet nom tooconnect tooyour serveur à l’aide de SQL Server Management Studio.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).

2. Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page. 

3. Bonjour **Essentials** volet Bonjour page du portail Azure pour votre base de données, recherchez et copiez hello **nom du serveur**.

   ![informations de connexion](../articles/sql-database/media/sql-database-get-started-portal/server-name.png) 
