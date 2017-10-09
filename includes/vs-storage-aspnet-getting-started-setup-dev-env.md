## <a name="set-up-hello-development-environment"></a><span data-ttu-id="3d726-101">Configuration d’environnement de développement hello</span><span class="sxs-lookup"><span data-stu-id="3d726-101">Set up hello development environment</span></span>

<span data-ttu-id="3d726-102">Cette section vous guide Configuration de votre environnement de développement, y compris la création d’une application ASP.NET MVC, ajoutez une connexion de Services connectés, ajoutez un contrôleur, et en spécifiant hello nécessaire directives d’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="3d726-102">This section walks you setting up your development environment, including creating an ASP.NET MVC app, adding a Connected Services connection, adding a controller, and specifying hello required namespace directives.</span></span>

### <a name="create-an-aspnet-mvc-app-project"></a><span data-ttu-id="3d726-103">Création d’un projet d’application MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="3d726-103">Create an ASP.NET MVC app project</span></span>

1. <span data-ttu-id="3d726-104">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3d726-104">Open Visual Studio.</span></span>

1. <span data-ttu-id="3d726-105">Sélectionnez **fichier -> Nouveau -> projet** à partir du menu principal de hello</span><span class="sxs-lookup"><span data-stu-id="3d726-105">Select **File->New->Project** from hello main menu</span></span>

1. <span data-ttu-id="3d726-106">Sur hello **nouveau projet** boîte de dialogue, spécifiez les options de hello en hello figure suivante :</span><span class="sxs-lookup"><span data-stu-id="3d726-106">On hello **New Project** dialog, specify hello options as highlighted in hello following figure:</span></span>

    ![Création d’un projet ASP.NET](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-1.png)

1. <span data-ttu-id="3d726-108">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d726-108">Select **OK**.</span></span>

1. <span data-ttu-id="3d726-109">Sur hello **nouveau projet ASP.NET** boîte de dialogue, spécifiez les options de hello en hello figure suivante :</span><span class="sxs-lookup"><span data-stu-id="3d726-109">On hello **New ASP.NET Project** dialog, specify hello options as highlighted in hello following figure:</span></span>

    ![Spécification de MVC](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-2.png)

1. <span data-ttu-id="3d726-111">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d726-111">Select **OK**.</span></span>

### <a name="use-connected-services-tooconnect-tooan-azure-storage-account"></a><span data-ttu-id="3d726-112">Utiliser le compte de stockage Azure des Services connectés tooconnect tooan</span><span class="sxs-lookup"><span data-stu-id="3d726-112">Use Connected Services tooconnect tooan Azure storage account</span></span>

1. <span data-ttu-id="3d726-113">Bonjour **l’Explorateur de solutions**, cliquez sur le projet de hello et dans le menu contextuel de hello, sélectionnez **Ajouter -> Service connecté**.</span><span class="sxs-lookup"><span data-stu-id="3d726-113">In hello **Solution Explorer**, right-click hello project, and from hello context menu, select **Add->Connected Service**.</span></span>

1. <span data-ttu-id="3d726-114">Sur hello **ajouter un Service connecté** boîte de dialogue, sélectionnez **Azure Storage**, puis sélectionnez **configurer**.</span><span class="sxs-lookup"><span data-stu-id="3d726-114">On hello **Add Connected Service** dialog, select **Azure Storage**, and then select **Configure**.</span></span>

    ![Boîte de dialogue Ajouter un service connecté](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-3.png)

1. <span data-ttu-id="3d726-116">Sur hello **Azure Storage** boîte de dialogue, sélectionnez hello compte de stockage Azure souhaité avec lequel vous souhaitez toowork, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3d726-116">On hello **Azure Storage** dialog, select hello desired Azure storage account with which you want toowork, and select **Add**.</span></span>
