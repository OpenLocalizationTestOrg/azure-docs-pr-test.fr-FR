### <a name="prerequisites"></a>Composants requis
* Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)
* Un [base de données SQL Azure](../articles/sql-database/sql-database-get-started.md) avec ses informations de connexion, notamment le nom du serveur hello, nom de la base de données et nom d’utilisateur/mot de passe. Ces informations sont incluses dans la chaîne de connexion de base de données SQL de hello :
  
    Server=tcp:*nom_SQL_Server*.database.windows.net,1433;Initial Catalog=*nom_BD_SQL*;Persist Security Info=False;User ID={your_username};Password={your_password};MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
  
    Pour en savoir plus, consultez [Bases de données SQL Azure](https://azure.microsoft.com/services/sql-database).

> [!NOTE]
> Lorsque vous créez une base de données SQL Azure, vous pouvez également créer des bases de données exemple hello inclus avec SQL. 
> 
> 

Avant d’utiliser votre base de données SQL Azure dans une application logique, connectez tooyour base de données SQL. Vous pouvez effectuer cela facilement au sein de votre application logique sur hello portail Azure.  

Se connecter tooyour étapes de base de données SQL Azure à l’aide de hello suivant :  

1. Créez une application logique. Dans le concepteur hello Logic Apps, ajouter un déclencheur, puis ajoutez une action. Sélectionnez **Microsoft d’afficher les API managées** Bonjour liste déroulante, puis entrez « sql » dans la zone de recherche hello. Sélectionnez une des actions de hello :  
   
    ![étape de création de la connexion à SQL Azure](./media/connectors-create-api-sqlazure/sql-actions.png)
2. Si vous n’avez pas précédemment créé n’importe quel tooSQL de connexions de base de données, vous êtes invité hello détails de connexion :  
   
    ![étape de création de la connexion à SQL Azure](./media/connectors-create-api-sqlazure/connection-details.png) 
3. Entrez les détails de base de données SQL hello. Les propriétés marquées d’un astérisque sont obligatoires.
   
   | Propriété | Détails |
   | --- | --- |
   | Se connecter via la passerelle |Laissez cette option désactivée. Il est utilisé lors de la connexion tooan local SQL Server. |
   | Nom de connexion * |Entrez un nom pour votre connexion. |
   | Nom du serveur SQL Server * |Entrez le nom du serveur hello ; qui est un nom tel que *nomserveur.basededonnées.Windows.NET*. nom du serveur Hello est affiché dans les propriétés de base de données SQL hello Bonjour portail Azure et affiche également dans la chaîne de connexion hello. |
   | Nom de la base de données SQL * |Entrez le nom hello vous donnez à votre base de données SQL. Cette information est répertoriée dans les propriétés de base de données SQL hello dans la chaîne de connexion hello : Initial Catalog =*yoursqldbname*. |
   | Nom d’utilisateur * |Entrez le nom d’utilisateur hello que vous avez créé lors de la création de hello de base de données SQL. Cette information est répertoriée dans les propriétés de base de données SQL hello Bonjour portail Azure. |
   | Mot de passe * |Entrez le mot de passe hello créé lors de la création de hello de base de données SQL. |
   
    Ces informations d’identification sont utilisée tooauthorize votre tooconnect d’application logique et accéder à vos données SQL. Une fois terminé, votre connexion de détails, consultez similaire toohello suivantes :  
   
    ![étape de création de la connexion à SQL Azure](./media/connectors-create-api-sqlazure/sample-connection.png) 
4. Sélectionnez **Créer**. 
5. Avis hello connexion a été créée. Maintenant, hello autres étapes dans votre logique d’application : 
   
    ![étape de création de la connexion à SQL Azure](./media/connectors-create-api-sqlazure/table.png)

