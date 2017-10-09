## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="644b2-101">Configuration de l’interface de ligne de commande Azure pour Azure DNS</span><span class="sxs-lookup"><span data-stu-id="644b2-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="644b2-102">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="644b2-102">Before you begin</span></span>

<span data-ttu-id="644b2-103">Vérifiez que vous disposez des éléments suivants avant de commencer votre configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="644b2-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="644b2-104">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="644b2-104">An Azure subscription.</span></span> <span data-ttu-id="644b2-105">Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="644b2-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="644b2-106">Installez hello dernière version de hello CLI d’Azure, disponible pour Windows, Linux ou Mac.</span><span class="sxs-lookup"><span data-stu-id="644b2-106">Install hello latest version of hello Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="644b2-107">Plus d’informations est disponible à l’adresse [installation Bonjour Azure CLI](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="644b2-107">More information is available at [Install hello Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="644b2-108">Se connecter tooyour compte Azure</span><span class="sxs-lookup"><span data-stu-id="644b2-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="644b2-109">Ouvrez une fenêtre de console et procédez à l’authentification à l’aide de vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="644b2-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="644b2-110">Pour plus d’informations, consultez [connecter tooAzure de hello CLI d’Azure](../articles/xplat-cli-connect.md)</span><span class="sxs-lookup"><span data-stu-id="644b2-110">For more information, see [Log in tooAzure from hello Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="644b2-111">Passage en mode CLI</span><span class="sxs-lookup"><span data-stu-id="644b2-111">Switch CLI mode</span></span>

<span data-ttu-id="644b2-112">Azure DNS utilise Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="644b2-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="644b2-113">Assurez-vous que vous passez des commandes CLI mode toouse Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="644b2-113">Make sure you switch CLI mode toouse Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a><span data-ttu-id="644b2-114">Sélectionnez l’abonnement de hello</span><span class="sxs-lookup"><span data-stu-id="644b2-114">Select hello subscription</span></span>

<span data-ttu-id="644b2-115">Vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="644b2-115">Check hello subscriptions for hello account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="644b2-116">Choisissez parmi vos toouse abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="644b2-116">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="644b2-117">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="644b2-117">Create a resource group</span></span>

<span data-ttu-id="644b2-118">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="644b2-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="644b2-119">Cela est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="644b2-119">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="644b2-120">Toutefois, étant donné que toutes les ressources DNS sont globales, pas régional, choix hello de l’emplacement du groupe de ressources n’a aucun impact sur le système DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="644b2-120">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="644b2-121">Ignorez cette étape si vous utilisez un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="644b2-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="644b2-122">S’inscrire auprès du fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="644b2-122">Register resource provider</span></span>

<span data-ttu-id="644b2-123">Hello service DNS Azure est géré par le fournisseur de ressources Microsoft.Network hello.</span><span class="sxs-lookup"><span data-stu-id="644b2-123">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="644b2-124">Votre abonnement Azure doit d’être toouse inscrit ce fournisseur de ressources avant de pouvoir utiliser Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="644b2-124">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="644b2-125">Cette opération n’est à effectuer qu’une fois par abonnement.</span><span class="sxs-lookup"><span data-stu-id="644b2-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

