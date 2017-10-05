<span data-ttu-id="e08c0-101">Pour commencer à utiliser des files d’attente Service Bus dans Azure, vous devez d’abord créer un espace de noms avec un nom unique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e08c0-101">To begin using Service Bus queues in Azure, you must first create a namespace with a name that is unique across Azure.</span></span> <span data-ttu-id="e08c0-102">Ce dernier fournit un conteneur d'étendue pour l'adressage des ressources Service Bus au sein de votre application.</span><span class="sxs-lookup"><span data-stu-id="e08c0-102">A namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="e08c0-103">Pour créer un espace de noms :</span><span class="sxs-lookup"><span data-stu-id="e08c0-103">To create a namespace:</span></span>

1. <span data-ttu-id="e08c0-104">Connectez-vous au [portail Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="e08c0-104">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="e08c0-105">Dans le volet de navigation gauche du portail, cliquez sur **Nouveau**, puis sur **Enterprise Integration** et sur **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="e08c0-105">In the left navigation pane of the portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span></span>
3. <span data-ttu-id="e08c0-106">Dans la boîte de dialogue **Créer un espace de noms** , entrez un nom d’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="e08c0-106">In the **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="e08c0-107">Le système vérifie immédiatement si le nom est disponible.</span><span class="sxs-lookup"><span data-stu-id="e08c0-107">The system immediately checks to see if the name is available.</span></span>
4. <span data-ttu-id="e08c0-108">Lorsque vous avez vérifié la disponibilité de l’espace de noms, sélectionnez le niveau tarifaire (Basique, Standard ou Premium).</span><span class="sxs-lookup"><span data-stu-id="e08c0-108">After making sure the namespace name is available, choose the pricing tier (Basic, Standard, or Premium).</span></span>
5. <span data-ttu-id="e08c0-109">Dans le champ **Abonnement** , sélectionnez un abonnement Azure dans lequel créer l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="e08c0-109">In the **Subscription** field, choose an Azure subscription in which to create the namespace.</span></span>
6. <span data-ttu-id="e08c0-110">Dans le champ **Groupe de ressources** , choisissez un groupe de ressources existant dans lequel l’espace de noms sera utilisé, ou créez-en un nouveau.</span><span class="sxs-lookup"><span data-stu-id="e08c0-110">In the **Resource group** field, choose an existing resource group in which the namespace will live, or create a new one.</span></span>      
7. <span data-ttu-id="e08c0-111">Dans **Emplacement**, sélectionnez le pays ou la région où votre espace de noms doit être hébergé.</span><span class="sxs-lookup"><span data-stu-id="e08c0-111">In **Location**, choose the country or region in which your namespace should be hosted.</span></span>
   
    ![Créer un espace de noms][create-namespace]
8. <span data-ttu-id="e08c0-113">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e08c0-113">Click **Create**.</span></span> <span data-ttu-id="e08c0-114">Le système crée l'espace de noms de service et l'active.</span><span class="sxs-lookup"><span data-stu-id="e08c0-114">The system now creates your namespace and enables it.</span></span> <span data-ttu-id="e08c0-115">Vous devrez peut-être attendre plusieurs minutes afin que le système approvisionne des ressources pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="e08c0-115">You might have to wait several minutes as the system provisions resources for your account.</span></span>

### <a name="obtain-the-management-credentials"></a><span data-ttu-id="e08c0-116">Obtenir les informations d’identification de gestion</span><span class="sxs-lookup"><span data-stu-id="e08c0-116">Obtain the management credentials</span></span>

1. <span data-ttu-id="e08c0-117">Dans la liste des espaces de noms, cliquez sur le nom de l’espace de noms que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="e08c0-117">In the list of namespaces, click the newly created namespace name.</span></span>
2. <span data-ttu-id="e08c0-118">Dans le panneau Espace de noms, cliquez sur **Stratégies d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="e08c0-118">In the namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="e08c0-119">Dans le panneau **Stratégies d’accès partagé**, cliquez sur **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="e08c0-119">In the **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![informations de connexion][connection-info]
4. <span data-ttu-id="e08c0-121">Dans le panneau **Policy: RootManageSharedAccessKey (Stratégie : RootManageSharedAccessKey)**, cliquez sur le bouton de copie situé en regard de **Clé primaire de la chaîne de connexion**, pour copier la chaîne de connexion dans le presse-papiers pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e08c0-121">In the **Policy: RootManageSharedAccessKey** blade, click the copy button next to **Connection string–primary key**, to copy the connection string to your clipboard for later use.</span></span> <span data-ttu-id="e08c0-122">Copiez cette valeur dans le Bloc-notes ou un autre emplacement temporaire.</span><span class="sxs-lookup"><span data-stu-id="e08c0-122">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="e08c0-124">Répétez l’étape précédente, en copiant et collant la valeur de **Clé primaire** dans un emplacement temporaire pour l’utiliser ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="e08c0-124">Repeat the previous step, copying and pasting the value of **Primary key** to a temporary location for later use.</span></span>

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
