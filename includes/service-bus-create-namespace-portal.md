<span data-ttu-id="7aa9e-101">les files d’attente de toobegin à l’aide du Service Bus dans Azure, vous devez d’abord créer un espace de noms avec un nom qui est unique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-101">toobegin using Service Bus queues in Azure, you must first create a namespace with a name that is unique across Azure.</span></span> <span data-ttu-id="7aa9e-102">Ce dernier fournit un conteneur d'étendue pour l'adressage des ressources Service Bus au sein de votre application.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-102">A namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="7aa9e-103">toocreate un espace de noms :</span><span class="sxs-lookup"><span data-stu-id="7aa9e-103">toocreate a namespace:</span></span>

1. <span data-ttu-id="7aa9e-104">Ouvrez une session sur toohello [portail Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="7aa9e-104">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="7aa9e-105">Dans le volet de navigation gauche hello du portail de hello, cliquez sur **nouveau**, puis cliquez sur **intégration**, puis cliquez sur **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-105">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span></span>
3. <span data-ttu-id="7aa9e-106">Bonjour **créer l’espace de noms** boîte de dialogue, entrez un nom d’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-106">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="7aa9e-107">système de Hello vérifie immédiatement toosee si le nom hello est disponible.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-107">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="7aa9e-108">Une fois que nom d’espace de noms hello de fabrication est disponible, choisissez hello tarification (Basic, Standard ou Premium).</span><span class="sxs-lookup"><span data-stu-id="7aa9e-108">After making sure hello namespace name is available, choose hello pricing tier (Basic, Standard, or Premium).</span></span>
5. <span data-ttu-id="7aa9e-109">Bonjour **abonnement** champ, choisissez un abonnement Azure dans l’espace de noms toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-109">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
6. <span data-ttu-id="7aa9e-110">Bonjour **groupe de ressources** champ, choisissez un groupe de ressources existant dans le hello espace de noms dynamique, ou créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-110">In hello **Resource group** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
7. <span data-ttu-id="7aa9e-111">Dans **emplacement**, choisissez hello pays ou une région dans laquelle votre espace de noms doit être hébergé.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-111">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![Créer un espace de noms][create-namespace]
8. <span data-ttu-id="7aa9e-113">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-113">Click **Create**.</span></span> <span data-ttu-id="7aa9e-114">système de Hello maintenant crée votre espace de noms et active.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-114">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="7aa9e-115">Vous pouvez avoir toowait plusieurs minutes en tant que hello système configure des ressources pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-115">You might have toowait several minutes as hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="7aa9e-116">Obtenir des informations d’identification de gestion hello</span><span class="sxs-lookup"><span data-stu-id="7aa9e-116">Obtain hello management credentials</span></span>

1. <span data-ttu-id="7aa9e-117">Dans hello d’espaces de noms, cliquez sur hello nouvellement créée le nom de l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-117">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="7aa9e-118">Dans le panneau espace de noms de hello, cliquez sur **les stratégies d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-118">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="7aa9e-119">Bonjour **les stratégies d’accès partagé** panneau, cliquez sur **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-119">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![informations de connexion][connection-info]
4. <span data-ttu-id="7aa9e-121">Bonjour **stratégie : RootManageSharedAccessKey** panneau, cliquez sur bouton hello suivant trop**la clé de chaîne – primary connexion**, toocopy hello connexion chaîne tooyour le Presse-papiers pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-121">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="7aa9e-122">Copiez cette valeur dans le Bloc-notes ou un autre emplacement temporaire.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-122">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="7aa9e-124">Étape précédente hello répétition, copier et coller la valeur hello **clé primaire** tooa les emplacement temporaire pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7aa9e-124">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
