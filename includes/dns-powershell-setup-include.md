## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="9849c-101">Configurer Azure PowerShell pour Azure DNS</span><span class="sxs-lookup"><span data-stu-id="9849c-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="9849c-102">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="9849c-102">Before you begin</span></span>

<span data-ttu-id="9849c-103">Vérifiez que vous disposez des éléments suivants avant de commencer votre configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="9849c-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="9849c-104">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9849c-104">An Azure subscription.</span></span> <span data-ttu-id="9849c-105">Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9849c-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9849c-106">Vous devez tooinstall hello dernière version de hello applets de commande PowerShell de gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9849c-106">You need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="9849c-107">Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="9849c-107">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="9849c-108">Se connecter tooyour compte Azure</span><span class="sxs-lookup"><span data-stu-id="9849c-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="9849c-109">Ouvrez la console PowerShell et tooyour compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="9849c-109">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="9849c-110">Pour en avoir plus, voir [Utilisation de Windows PowerShell avec Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9849c-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a><span data-ttu-id="9849c-111">Sélectionnez l’abonnement de hello</span><span class="sxs-lookup"><span data-stu-id="9849c-111">Select hello subscription</span></span>
 
<span data-ttu-id="9849c-112">Vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="9849c-112">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="9849c-113">Choisissez parmi vos toouse abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="9849c-113">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="9849c-114">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="9849c-114">Create a resource group</span></span>

<span data-ttu-id="9849c-115">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="9849c-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="9849c-116">Cet emplacement est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="9849c-116">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="9849c-117">Toutefois, étant donné que toutes les ressources DNS sont globales, pas régional, choix hello de l’emplacement du groupe de ressources n’a aucun impact sur le système DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="9849c-117">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="9849c-118">Ignorez cette étape si vous utilisez un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="9849c-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="9849c-119">S’inscrire auprès du fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="9849c-119">Register resource provider</span></span>

<span data-ttu-id="9849c-120">Hello service DNS Azure est géré par le fournisseur de ressources Microsoft.Network hello.</span><span class="sxs-lookup"><span data-stu-id="9849c-120">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="9849c-121">Votre abonnement Azure doit d’être toouse inscrit ce fournisseur de ressources avant de pouvoir utiliser Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="9849c-121">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="9849c-122">Cette opération n’est à effectuer qu’une fois par abonnement.</span><span class="sxs-lookup"><span data-stu-id="9849c-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```