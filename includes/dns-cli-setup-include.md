## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="aba60-101">Configuration de l’interface de ligne de commande Azure pour Azure DNS</span><span class="sxs-lookup"><span data-stu-id="aba60-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="aba60-102">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="aba60-102">Before you begin</span></span>

<span data-ttu-id="aba60-103">Vérifiez que vous disposez des éléments ci-dessous avant de commencer votre configuration.</span><span class="sxs-lookup"><span data-stu-id="aba60-103">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="aba60-104">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="aba60-104">An Azure subscription.</span></span> <span data-ttu-id="aba60-105">Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aba60-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="aba60-106">Installez la dernière version de l’interface de ligne de commande Azure, disponible pour Windows, Linux ou MAC.</span><span class="sxs-lookup"><span data-stu-id="aba60-106">Install the latest version of the Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="aba60-107">Pour plus d’informations, consultez la page [Installation de l’interface de ligne de commande Azure](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="aba60-107">More information is available at [Install the Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="aba60-108">Connexion à votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="aba60-108">Sign in to your Azure account</span></span>

<span data-ttu-id="aba60-109">Ouvrez une fenêtre de console et procédez à l’authentification à l’aide de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="aba60-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="aba60-110">Pour plus d’informations, consultez [Se connecter à Azure avec la CLI Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="aba60-110">For more information, see [Log in to Azure from the Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="aba60-111">Passage en mode CLI</span><span class="sxs-lookup"><span data-stu-id="aba60-111">Switch CLI mode</span></span>

<span data-ttu-id="aba60-112">Azure DNS utilise Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aba60-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="aba60-113">Veillez à utiliser le mode d’interface de ligne de commande pour exécuter les commandes Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aba60-113">Make sure you switch CLI mode to use Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-the-subscription"></a><span data-ttu-id="aba60-114">Sélection de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="aba60-114">Select the subscription</span></span>

<span data-ttu-id="aba60-115">Vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="aba60-115">Check the subscriptions for the account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="aba60-116">Parmi vos abonnements Azure, choisissez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="aba60-116">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="aba60-117">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="aba60-117">Create a resource group</span></span>

<span data-ttu-id="aba60-118">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="aba60-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="aba60-119">Ce dernier est utilisé comme emplacement par défaut des ressources de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="aba60-119">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="aba60-120">Toutefois, étant donné que toutes les ressources DNS sont globales et non régionales, le choix de l’emplacement du groupe de ressources n’a aucun impact sur Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="aba60-120">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="aba60-121">Ignorez cette étape si vous utilisez un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="aba60-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="aba60-122">S’inscrire auprès du fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="aba60-122">Register resource provider</span></span>

<span data-ttu-id="aba60-123">Le service Azure DNS est géré par le fournisseur de ressources Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="aba60-123">The Azure DNS service is managed by the Microsoft.Network resource provider.</span></span> <span data-ttu-id="aba60-124">Votre abonnement Azure doit être enregistré auprès de ce fournisseur de ressources pour que vous puissiez utiliser Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="aba60-124">Your Azure subscription must be registered to use this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="aba60-125">Cette opération n’est à effectuer qu’une fois par abonnement.</span><span class="sxs-lookup"><span data-stu-id="aba60-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

