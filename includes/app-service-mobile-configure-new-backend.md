
1. Cliquez sur hello **des Services d’application** bouton, sélectionnez votre serveur d’applications mobiles principal, sélectionnez **Quickstart**, puis sélectionnez votre plateforme de client (iOS, Android, Xamarin, Cordova).

    ![Portail Azure avec Démarrage rapide Mobile Apps en surbrillance][quickstart]

2. Si une connexion de base de données n’est pas configurée, créez-en un en procédant comme suit de hello :

    ![Portail Azure avec toodatabase de connecter des applications mobiles][connect]

    a. Créez une base de données SQL Database et un serveur.

    ![Portail Azure avec Mobile Apps créant une base de données et un serveur][server]

    b. Attendez que la connexion de données hello est créée avec succès.

    ![Notification du portail Azure pour la création réussie d’une connexion de données][notification]

    c. La connexion de données doit être réussie.

    ![Notification du portail Azure, « Vous avez déjà créé une connexion de données »][already-connection]

3. Sous **2. Créer une API de table**, sélectionnez Node.js pour **Langage du serveur principal**. 
 
4. Accepter l’accusé de réception hello et sélectionnez **table TodoItem de créer**.  
    Cette action crée une table d’éléments de tâche dans votre base de données. 

    >[!IMPORTANT]
    > Basculer un tooNode.js back-end existant remplace tout le contenu. toocreate principale .NET au lieu de cela, consultez [fonctionner avec le serveur de hello principal .NET SDK pour applications mobiles][instructions].

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
