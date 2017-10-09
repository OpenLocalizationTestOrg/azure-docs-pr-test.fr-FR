
1. <span data-ttu-id="a0d44-101">Cliquez sur hello **des Services d’application** bouton, sélectionnez votre serveur d’applications mobiles principal, sélectionnez **Quickstart**, puis sélectionnez votre plateforme de client (iOS, Android, Xamarin, Cordova).</span><span class="sxs-lookup"><span data-stu-id="a0d44-101">Click hello **App Services** button, select your Mobile Apps back end, select **Quickstart**, and then select your client platform (iOS, Android, Xamarin, Cordova).</span></span>

    ![Portail Azure avec Démarrage rapide Mobile Apps en surbrillance][quickstart]

2. <span data-ttu-id="a0d44-103">Si une connexion de base de données n’est pas configurée, créez-en un en procédant comme suit de hello :</span><span class="sxs-lookup"><span data-stu-id="a0d44-103">If a database connection is not configured, create one by doing hello following:</span></span>

    ![Portail Azure avec toodatabase de connecter des applications mobiles][connect]

    <span data-ttu-id="a0d44-105">a.</span><span class="sxs-lookup"><span data-stu-id="a0d44-105">a.</span></span> <span data-ttu-id="a0d44-106">Créez une base de données SQL Database et un serveur.</span><span class="sxs-lookup"><span data-stu-id="a0d44-106">Create a new SQL database and server.</span></span>

    ![Portail Azure avec Mobile Apps créant une base de données et un serveur][server]

    <span data-ttu-id="a0d44-108">b.</span><span class="sxs-lookup"><span data-stu-id="a0d44-108">b.</span></span> <span data-ttu-id="a0d44-109">Attendez que la connexion de données hello est créée avec succès.</span><span class="sxs-lookup"><span data-stu-id="a0d44-109">Wait until hello data connection is successfully created.</span></span>

    ![Notification du portail Azure pour la création réussie d’une connexion de données][notification]

    <span data-ttu-id="a0d44-111">c.</span><span class="sxs-lookup"><span data-stu-id="a0d44-111">c.</span></span> <span data-ttu-id="a0d44-112">La connexion de données doit être réussie.</span><span class="sxs-lookup"><span data-stu-id="a0d44-112">Data connection must be successful.</span></span>

    ![Notification du portail Azure, « Vous avez déjà créé une connexion de données »][already-connection]

3. <span data-ttu-id="a0d44-114">Sous **2. Créer une API de table**, sélectionnez Node.js pour **Langage du serveur principal**.</span><span class="sxs-lookup"><span data-stu-id="a0d44-114">Under **2. Create a table API**, select Node.js for **Backend language**.</span></span> 
 
4. <span data-ttu-id="a0d44-115">Accepter l’accusé de réception hello et sélectionnez **table TodoItem de créer**.</span><span class="sxs-lookup"><span data-stu-id="a0d44-115">Accept hello acknowledgment, and then select **Create TodoItem table**.</span></span>  
    <span data-ttu-id="a0d44-116">Cette action crée une table d’éléments de tâche dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="a0d44-116">This action creates a new to-do item table in your database.</span></span> 

    >[!IMPORTANT]
    > <span data-ttu-id="a0d44-117">Basculer un tooNode.js back-end existant remplace tout le contenu.</span><span class="sxs-lookup"><span data-stu-id="a0d44-117">Switching an existing back end tooNode.js overwrites all contents.</span></span> <span data-ttu-id="a0d44-118">toocreate principale .NET au lieu de cela, consultez [fonctionner avec le serveur de hello principal .NET SDK pour applications mobiles][instructions].</span><span class="sxs-lookup"><span data-stu-id="a0d44-118">toocreate a .NET back end instead, see [Work with hello .NET back-end server SDK for Mobile Apps][instructions].</span></span>

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
