
1. <span data-ttu-id="49222-101">Cliquez sur le **des Services d’application** bouton, sélectionnez votre serveur d’applications mobiles principal, sélectionnez **Quickstart**, puis sélectionnez votre plateforme de client (iOS, Android, Xamarin, Cordova).</span><span class="sxs-lookup"><span data-stu-id="49222-101">Click the **App Services** button, select your Mobile Apps back end, select **Quickstart**, and then select your client platform (iOS, Android, Xamarin, Cordova).</span></span>

    ![Portail Azure avec Mobile Apps Quickstart mis en surbrillance][quickstart]

2. <span data-ttu-id="49222-103">Si une connexion de base de données n’est pas configurée, créez-en un en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="49222-103">If a database connection is not configured, create one by doing the following:</span></span>

    ![Portail Azure à connecter des applications mobiles pour la base de données][connect]

    <span data-ttu-id="49222-105">a.</span><span class="sxs-lookup"><span data-stu-id="49222-105">a.</span></span> <span data-ttu-id="49222-106">Créer une nouvelle base de données SQL et le serveur.</span><span class="sxs-lookup"><span data-stu-id="49222-106">Create a new SQL database and server.</span></span>

    ![Portail Azure avec des applications mobiles créer le serveur et la nouvelle base de données][server]

    <span data-ttu-id="49222-108">b.</span><span class="sxs-lookup"><span data-stu-id="49222-108">b.</span></span> <span data-ttu-id="49222-109">Attendez que la connexion de données soit créée.</span><span class="sxs-lookup"><span data-stu-id="49222-109">Wait until the data connection is successfully created.</span></span>

    ![Notification du portail Azure de création réussie d’une connexion de données][notification]

    <span data-ttu-id="49222-111">c.</span><span class="sxs-lookup"><span data-stu-id="49222-111">c.</span></span> <span data-ttu-id="49222-112">La connexion de données doit être réussie.</span><span class="sxs-lookup"><span data-stu-id="49222-112">Data connection must be successful.</span></span>

    ![Notification du portail Azure, « vous avez déjà une connexion de données »][already-connection]

3. <span data-ttu-id="49222-114">Sous **2. Créer une API de table**, sélectionnez Node.js pour **Langage du serveur principal**.</span><span class="sxs-lookup"><span data-stu-id="49222-114">Under **2. Create a table API**, select Node.js for **Backend language**.</span></span> 
 
4. <span data-ttu-id="49222-115">Accepter l’accusé de réception, puis sélectionnez **table TodoItem de créer**.</span><span class="sxs-lookup"><span data-stu-id="49222-115">Accept the acknowledgment, and then select **Create TodoItem table**.</span></span>  
    <span data-ttu-id="49222-116">Cette action crée une nouvelle table d’élément de tâches dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="49222-116">This action creates a new to-do item table in your database.</span></span> 

    >[!IMPORTANT]
    > <span data-ttu-id="49222-117">Basculement d’un serveur principal existant pour Node.js remplace tout le contenu.</span><span class="sxs-lookup"><span data-stu-id="49222-117">Switching an existing back end to Node.js overwrites all contents.</span></span> <span data-ttu-id="49222-118">Pour créer un serveur principal de .NET au lieu de cela, consultez [fonctionne avec le serveur principal de .NET SDK pour applications mobiles][instructions].</span><span class="sxs-lookup"><span data-stu-id="49222-118">To create a .NET back end instead, see [Work with the .NET back-end server SDK for Mobile Apps][instructions].</span></span>

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
