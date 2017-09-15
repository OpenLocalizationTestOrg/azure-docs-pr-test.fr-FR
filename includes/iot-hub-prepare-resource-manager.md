## <a name="prepare-to-authenticate-azure-resource-manager-requests"></a><span data-ttu-id="1b1db-101">Préparation de l’authentification des demandes d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b1db-101">Prepare to authenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="1b1db-102">Vous devez authentifier toutes les opérations que vous effectuez sur des ressources à l’aide d’[Azure Resource Manager][lnk-authenticate-arm] avec Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="1b1db-102">You must authenticate all the operations that you perform on resources using the [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="1b1db-103">La manière la plus simple de configurer cela consiste à utiliser PowerShell ou l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="1b1db-103">The easiest way to configure this is to use PowerShell or Azure CLI.</span></span>

<span data-ttu-id="1b1db-104">Avant toute chose, installez les [applets de commande Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="1b1db-104">Install the [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="1b1db-105">Les étapes suivantes montrent comment configurer l’authentification par mot de passe pour une application Active Directory à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b1db-105">The following steps show how to set up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="1b1db-106">Vous pouvez exécuter ces commandes dans le cadre d’une session PowerShell standard.</span><span class="sxs-lookup"><span data-stu-id="1b1db-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="1b1db-107">Pour vous connecter à votre abonnement Azure, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1b1db-107">Log in to your Azure subscription using the following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="1b1db-108">Si vous possédez plusieurs abonnements Azure, la connexion à Azure vous donne accès à tous les abonnements Azure associés à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="1b1db-108">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="1b1db-109">Utilisez la commande suivante pour répertorier les abonnements Azure que vous pouvez utiliser :</span><span class="sxs-lookup"><span data-stu-id="1b1db-109">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="1b1db-110">Utilisez la commande suivante pour sélectionner l’abonnement que vous souhaitez utiliser afin d'exécuter les commandes pour gérer votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1b1db-110">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="1b1db-111">Vous pouvez utiliser le nom de l’abonnement ou l’ID de la sortie de la commande précédente :</span><span class="sxs-lookup"><span data-stu-id="1b1db-111">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="1b1db-112">Prenez note des valeurs **TenantId** et **SubscriptionId**.</span><span class="sxs-lookup"><span data-stu-id="1b1db-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="1b1db-113">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="1b1db-113">You need them later.</span></span>
3. <span data-ttu-id="1b1db-114">Créez une application Azure Active Directory à l’aide de la commande suivante, en remplaçant les espaces réservés :</span><span class="sxs-lookup"><span data-stu-id="1b1db-114">Create a new Azure Active Directory application using the following command, replacing the place holders:</span></span>
   
   * <span data-ttu-id="1b1db-115">**{Nom d’affichage} :** nom d’affichage pour votre application, par exemple, **MySampleApp**</span><span class="sxs-lookup"><span data-stu-id="1b1db-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="1b1db-116">**{URL de la page d’accueil} :** URL de la page d’accueil de votre application, par exemple, **http://mysampleapp/home**.</span><span class="sxs-lookup"><span data-stu-id="1b1db-116">**{Home page URL}:** the URL of the home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="1b1db-117">Cette URL n’a pas besoin de pointer vers une application réelle.</span><span class="sxs-lookup"><span data-stu-id="1b1db-117">This URL does not need to point to a real application.</span></span>
   * <span data-ttu-id="1b1db-118">**{Identificateur d’application} :** identificateur unique, par exemple, **http://mysampleapp**.</span><span class="sxs-lookup"><span data-stu-id="1b1db-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="1b1db-119">Cette URL n’a pas besoin de pointer vers une application réelle.</span><span class="sxs-lookup"><span data-stu-id="1b1db-119">This URL does not need to point to a real application.</span></span>
   * <span data-ttu-id="1b1db-120">**{Mot de passe} :** mot de passe que vous utiliserez pour vous authentifier dans votre application.</span><span class="sxs-lookup"><span data-stu-id="1b1db-120">**{Password}:** A password that you use to authenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="1b1db-121">Prenez note de l’ **ApplicationId** de l’application que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="1b1db-121">Make a note of the **ApplicationId** of the application you created.</span></span> <span data-ttu-id="1b1db-122">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="1b1db-122">You need this later.</span></span>
5. <span data-ttu-id="1b1db-123">Créez un principal de service à l’aide de la commande suivante, en remplaçant **{MyApplicationId}** par **l’ApplicationId** de l’étape précédente :</span><span class="sxs-lookup"><span data-stu-id="1b1db-123">Create a new service principal using the following command, replacing **{MyApplicationId}** with the **ApplicationId** from the previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="1b1db-124">Configurez une attribution de rôle à l’aide de la commande suivante, en remplaçant **{MyApplicationId}** par votre **ApplicationId**.</span><span class="sxs-lookup"><span data-stu-id="1b1db-124">Set up a role assignment using the following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="1b1db-125">Vous avez maintenant créé l’application Azure AD qui vous permet de vous authentifier à partir de votre application C#.</span><span class="sxs-lookup"><span data-stu-id="1b1db-125">You have now finished creating the Azure AD application that enables you to authenticate from your custom C# application.</span></span> <span data-ttu-id="1b1db-126">Vous aurez besoin des valeurs suivantes plus loin dans ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="1b1db-126">You need the following values later in this tutorial:</span></span>

* <span data-ttu-id="1b1db-127">TenantId</span><span class="sxs-lookup"><span data-stu-id="1b1db-127">TenantId</span></span>
* <span data-ttu-id="1b1db-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="1b1db-128">SubscriptionId</span></span>
* <span data-ttu-id="1b1db-129">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="1b1db-129">ApplicationId</span></span>
* <span data-ttu-id="1b1db-130">Mot de passe</span><span class="sxs-lookup"><span data-stu-id="1b1db-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
