1. Dans une nouvelle fenêtre, connectez-vous toohello [portail Azure](https://portal.azure.com/).
2. Dans le volet gauche de hello, cliquez sur **nouveau**, cliquez sur **bases de données**, puis sous **base de données Azure Cosmos**, cliquez sur **créer**.
   
   ![Hello volet de bases de données du portail Azure](./media/cosmos-db-create-dbaccount/create-nosql-db-databases-json-tutorial-1.png)

3. Sur hello **nouveau compte** panneau, spécifiez la configuration hello souhaitées pour ce compte de base de données Azure Cosmos. 

    Grâce à Azure Cosmos DB, vous pouvez choisir l’un des quatre modèles de programmation : Gremlin (graphique), MongoDB, SQL (DocumentDB) et Table (clé-valeur). Chacun de ces modèles requiert actuellement un compte distinct.
    
    Dans cet article de démarrage rapide nous programmer hello API DocumentDB, par conséquent, choisissez **SQL (DocumentDB)** pendant que vous remplissez le formulaire de hello. Si vous disposez de données graphiques pour une application de réseau social, de données clé/valeur (table) ou de données ayant fait l’objet d’une migration à partir d’une application MongoDB, notez qu’Azure Cosmos DB peut fournir une plateforme de service de base de données hautement disponible et distribuée dans le monde entier pour toutes vos applications stratégiques.

    Renseignez les champs hello sur hello **nouveau compte** panneau, à l’aide des informations hello Bonjour suivant comme guide - capture d’écran de vos valeurs peut-être être différente de valeurs hello dans la capture d’écran de hello.
 
    ![nouveau panneau de compte Hello pour la base de données Azure Cosmos](./media/cosmos-db-create-dbaccount/create-nosql-db-databases-json-tutorial-2.png)

    Paramètre|Valeur suggérée|Description
    ---|---|---
    ID|*Valeur unique*|Nom unique identifiant ce compte Azure Cosmos DB. Étant donné que *documents.azure.com* est ajouté toohello ID que vous fournissez toocreate votre URI, utilisation unique mais identifiables ID. ID de Hello peut contenir uniquement des lettres minuscules, des chiffres et des caractères de trait d’union (-) hello, et il doit contenir 3 caractères too50.
    API|SQL (DocumentDB)|Programmer avec hello [API DocumentDB](../articles/documentdb/documentdb-introduction.md) plus loin dans cet article.|
    Abonnement|*Votre abonnement*|Hello abonnement Azure que vous souhaitez toouse pour ce compte de base de données Azure Cosmos. 
    Groupe de ressources|*Hello même valeur que l’ID*|nom de groupe de ressources de nouveau Hello pour votre compte. Par souci de simplicité, vous pouvez utiliser hello même nom que votre code. 
    Lieu|*utilisateurs tooyour le plus proche Hello région*|Bonjour à l’emplacement géographique dans le toohost votre compte de base de données Azure Cosmos. Choisissez un emplacement hello qui est le plus proche toogive d’utilisateurs tooyour les hello plus rapide toohello accéder à des données.
4. Cliquez sur **créer** compte de hello toocreate.
5. Sur la barre d’outils supérieure hello, cliquez sur hello **Notifications** icône ![l’icône de hello](./media/cosmos-db-create-dbaccount/notification-icon.png) processus de déploiement toomonitor hello.

    ![Hello volet de Notifications du portail Azure](./media/cosmos-db-create-dbaccount-graph/azure-documentdb-nosql-notification.png)

6.  Lorsque la fenêtre de Notifications hello indique fenêtre de notification hello déploiement hello a réussi, fermez et ouvrez hello nouveau compte hello **toutes les ressources** vignette sur hello du tableau de bord. 

    ![Hello compte DocumentDB sur hello que toutes les ressources en mosaïque](./media/cosmos-db-create-dbaccount/all-resources.png)
 
