1. <span data-ttu-id="5dcb5-101">Ouvrez une session sur toohello [portail Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="5dcb5-101">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="5dcb5-102">Dans le volet de navigation gauche hello du portail de hello, cliquez sur **nouveau**, puis cliquez sur **intégration**, puis cliquez sur **relais**.</span><span class="sxs-lookup"><span data-stu-id="5dcb5-102">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="5dcb5-103">Bonjour **créer l’espace de noms** boîte de dialogue, entrez un nom d’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="5dcb5-103">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="5dcb5-104">système de Hello vérifie immédiatement toosee si le nom hello est disponible.</span><span class="sxs-lookup"><span data-stu-id="5dcb5-104">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="5dcb5-105">Bonjour **abonnement** champ, choisissez un abonnement Azure dans l’espace de noms toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="5dcb5-105">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
5. <span data-ttu-id="5dcb5-106">Bonjour  **[groupe de ressources](../articles/azure-resource-manager/resource-group-portal.md)**  champ, choisissez un groupe de ressources existant dans le hello espace de noms dynamique, ou créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="5dcb5-106">In hello **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="5dcb5-107">Dans **emplacement**, choisissez hello pays ou une région dans laquelle votre espace de noms doit être hébergé.</span><span class="sxs-lookup"><span data-stu-id="5dcb5-107">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![Créer un espace de noms][create-namespace]
7. <span data-ttu-id="5dcb5-109">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="5dcb5-109">Click **Create**.</span></span> <span data-ttu-id="5dcb5-110">système de Hello maintenant crée votre espace de noms et active.</span><span class="sxs-lookup"><span data-stu-id="5dcb5-110">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="5dcb5-111">Après quelques minutes, hello système configure des ressources pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="5dcb5-111">After a few minutes, hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="5dcb5-112">Obtenir des informations d’identification de gestion hello</span><span class="sxs-lookup"><span data-stu-id="5dcb5-112">Obtain hello management credentials</span></span>
1. <span data-ttu-id="5dcb5-113">Dans hello d’espaces de noms, cliquez sur hello nouvellement créée le nom de l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="5dcb5-113">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="5dcb5-114">Dans le panneau espace de noms de hello, cliquez sur **les stratégies d’accès partagé**.</span><span class="sxs-lookup"><span data-stu-id="5dcb5-114">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="5dcb5-115">Bonjour **les stratégies d’accès partagé** panneau, cliquez sur **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="5dcb5-115">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![informations de connexion][connection-info]
4. <span data-ttu-id="5dcb5-117">Bonjour **stratégie : RootManageSharedAccessKey** panneau, cliquez sur bouton hello suivant trop**la clé de chaîne – primary connexion**, toocopy hello connexion chaîne tooyour le Presse-papiers pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="5dcb5-117">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="5dcb5-118">Copiez cette valeur dans le Bloc-notes ou un autre emplacement temporaire.</span><span class="sxs-lookup"><span data-stu-id="5dcb5-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![connection-string][connection-string]

5. <span data-ttu-id="5dcb5-120">Étape précédente hello répétition, copier et coller la valeur hello **clé primaire** tooa les emplacement temporaire pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="5dcb5-120">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
