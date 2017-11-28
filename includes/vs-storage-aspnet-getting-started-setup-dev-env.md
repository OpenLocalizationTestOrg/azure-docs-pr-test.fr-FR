## <a name="set-up-the-development-environment"></a><span data-ttu-id="24e78-101">Configuration de l’environnement de développement</span><span class="sxs-lookup"><span data-stu-id="24e78-101">Set up the development environment</span></span>

<span data-ttu-id="24e78-102">Cette section vous guide lors de la configuration d’un environnement de déploiement. Cela inclut la création d’une application MVC ASP.NET, l’ajout d’une connexion Services connectés et d’un contrôleur et la spécification des directives requises portant sur les espaces de noms.</span><span class="sxs-lookup"><span data-stu-id="24e78-102">This section walks you setting up your development environment, including creating an ASP.NET MVC app, adding a Connected Services connection, adding a controller, and specifying the required namespace directives.</span></span>

### <a name="create-an-aspnet-mvc-app-project"></a><span data-ttu-id="24e78-103">Création d’un projet d’application MVC ASP.NET</span><span class="sxs-lookup"><span data-stu-id="24e78-103">Create an ASP.NET MVC app project</span></span>

1. <span data-ttu-id="24e78-104">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24e78-104">Open Visual Studio.</span></span>

1. <span data-ttu-id="24e78-105">Sélectionnez **Fichier -> Nouveau -> Projet** dans le menu principal.</span><span class="sxs-lookup"><span data-stu-id="24e78-105">Select **File->New->Project** from the main menu</span></span>

1. <span data-ttu-id="24e78-106">Dans la boîte de dialogue **Nouveau projet**, spécifiez les options requises, comme indiqué dans la figure suivante :</span><span class="sxs-lookup"><span data-stu-id="24e78-106">On the **New Project** dialog, specify the options as highlighted in the following figure:</span></span>

    ![Création d’un projet ASP.NET](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-1.png)

1. <span data-ttu-id="24e78-108">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="24e78-108">Select **OK**.</span></span>

1. <span data-ttu-id="24e78-109">Dans la boîte de dialogue **Nouveau projet ASP.NET**, spécifiez les options requises, comme indiqué dans la figure suivante :</span><span class="sxs-lookup"><span data-stu-id="24e78-109">On the **New ASP.NET Project** dialog, specify the options as highlighted in the following figure:</span></span>

    ![Spécification de MVC](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-2.png)

1. <span data-ttu-id="24e78-111">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="24e78-111">Select **OK**.</span></span>

### <a name="use-connected-services-to-connect-to-an-azure-storage-account"></a><span data-ttu-id="24e78-112">Utiliser la fonctionnalité Services connectés pour se connecter à un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="24e78-112">Use Connected Services to connect to an Azure storage account</span></span>

1. <span data-ttu-id="24e78-113">Dans l’**Explorateur de solutions** de Visual Studio, cliquez avec le bouton droit sur le projet, puis sélectionnez **Ajouter -> Service connecté** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="24e78-113">In the **Solution Explorer**, right-click the project, and from the context menu, select **Add->Connected Service**.</span></span>

1. <span data-ttu-id="24e78-114">Dans la boîte de dialogue **Ajouter un service connecté**, choisissez **Stockage Azure**, puis cliquez sur le bouton **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="24e78-114">On the **Add Connected Service** dialog, select **Azure Storage**, and then select **Configure**.</span></span>

    ![Boîte de dialogue Ajouter un service connecté](./media/vs-storage-aspnet-getting-started-setup-dev-env/vs-storage-aspnet-getting-started-setup-dev-env-3.png)

1. <span data-ttu-id="24e78-116">Dans la boîte de dialogue **Stockage Azure**, sélectionnez le compte de stockage Azure que vous souhaitez utiliser, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="24e78-116">On the **Azure Storage** dialog, select the desired Azure storage account with which you want to work, and select **Add**.</span></span>
