## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a><span data-ttu-id="f3378-101">Préparer tooauthenticate demande du Gestionnaire de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="f3378-101">Prepare tooauthenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="f3378-102">Vous devez vous authentifier toutes les opérations de hello que vous effectuez sur les ressources à l’aide de hello [Azure Resource Manager] [ lnk-authenticate-arm] avec Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="f3378-102">You must authenticate all hello operations that you perform on resources using hello [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="f3378-103">Hello tooconfigure de façon plus simple Voici toouse PowerShell ou CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="f3378-103">hello easiest way tooconfigure this is toouse PowerShell or Azure CLI.</span></span>

<span data-ttu-id="f3378-104">Installer hello [applets de commande Azure PowerShell] [ lnk-powershell-install] avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="f3378-104">Install hello [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="f3378-105">Hello suivant les étapes indiquent comment tooset l’authentification du mot de passe pour une application AD à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3378-105">hello following steps show how tooset up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="f3378-106">Vous pouvez exécuter ces commandes dans le cadre d’une session PowerShell standard.</span><span class="sxs-lookup"><span data-stu-id="f3378-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="f3378-107">Ouvrez une session dans tooyour abonnement Azure à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f3378-107">Log in tooyour Azure subscription using hello following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="f3378-108">Si vous avez plusieurs abonnements Azure, l’ouverture de session tooAzure accorde vous accédez tooall hello Azure abonnements associés à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="f3378-108">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="f3378-109">Utilisez hello toolist hello abonnements Azure disponibles pour vous toouse de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f3378-109">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="f3378-110">Utilisez hello suivant abonnement tooselect de commande que vous souhaitez toouse toorun hello commandes toomanage votre hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f3378-110">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="f3378-111">Vous pouvez utiliser le nom de l’abonnement hello ou ID de sortie hello de la commande précédente hello :</span><span class="sxs-lookup"><span data-stu-id="f3378-111">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="f3378-112">Prenez note des valeurs **TenantId** et **SubscriptionId**.</span><span class="sxs-lookup"><span data-stu-id="f3378-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="f3378-113">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="f3378-113">You need them later.</span></span>
3. <span data-ttu-id="f3378-114">Créer une nouvelle application Azure Active Directory à l’aide de hello commande suivante, en remplaçant les espaces réservés hello :</span><span class="sxs-lookup"><span data-stu-id="f3378-114">Create a new Azure Active Directory application using hello following command, replacing hello place holders:</span></span>
   
   * <span data-ttu-id="f3378-115">**{Nom d’affichage} :** nom d’affichage pour votre application, par exemple, **MySampleApp**</span><span class="sxs-lookup"><span data-stu-id="f3378-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="f3378-116">**{URL de la page d’accueil} :** hello telles que les URL de page d’accueil hello de votre application **http://mysampleapp/home**.</span><span class="sxs-lookup"><span data-stu-id="f3378-116">**{Home page URL}:** hello URL of hello home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="f3378-117">Cette URL ne doit pas toopoint tooa véritable application.</span><span class="sxs-lookup"><span data-stu-id="f3378-117">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="f3378-118">**{Identificateur d’application} :** identificateur unique, par exemple, **http://mysampleapp**.</span><span class="sxs-lookup"><span data-stu-id="f3378-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="f3378-119">Cette URL ne doit pas toopoint tooa véritable application.</span><span class="sxs-lookup"><span data-stu-id="f3378-119">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="f3378-120">**{Password} :** un mot de passe que vous utilisez tooauthenticate avec votre application.</span><span class="sxs-lookup"><span data-stu-id="f3378-120">**{Password}:** A password that you use tooauthenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="f3378-121">Prenez note de hello **ApplicationId** de l’application hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="f3378-121">Make a note of hello **ApplicationId** of hello application you created.</span></span> <span data-ttu-id="f3378-122">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="f3378-122">You need this later.</span></span>
5. <span data-ttu-id="f3378-123">Créer une nouvelle entité de service à l’aide de hello commande suivante, en remplaçant **{MyApplicationId}** avec hello **ApplicationId** à partir de l’étape précédente de hello :</span><span class="sxs-lookup"><span data-stu-id="f3378-123">Create a new service principal using hello following command, replacing **{MyApplicationId}** with hello **ApplicationId** from hello previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="f3378-124">Configurer une attribution de rôle à l’aide de hello commande suivante, en remplaçant **{MyApplicationId}** avec votre **ApplicationId**.</span><span class="sxs-lookup"><span data-stu-id="f3378-124">Set up a role assignment using hello following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="f3378-125">Vous avez terminé de création d’application Azure AD hello qui vous permet de tooauthenticate à partir de votre application c# personnalisée.</span><span class="sxs-lookup"><span data-stu-id="f3378-125">You have now finished creating hello Azure AD application that enables you tooauthenticate from your custom C# application.</span></span> <span data-ttu-id="f3378-126">Vous devez hello valeurs suivantes plus loin dans ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="f3378-126">You need hello following values later in this tutorial:</span></span>

* <span data-ttu-id="f3378-127">TenantId</span><span class="sxs-lookup"><span data-stu-id="f3378-127">TenantId</span></span>
* <span data-ttu-id="f3378-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="f3378-128">SubscriptionId</span></span>
* <span data-ttu-id="f3378-129">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="f3378-129">ApplicationId</span></span>
* <span data-ttu-id="f3378-130">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="f3378-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
