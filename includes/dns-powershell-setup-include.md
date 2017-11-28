## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="21d92-101">Configurer Azure PowerShell pour Azure DNS</span><span class="sxs-lookup"><span data-stu-id="21d92-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="21d92-102">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="21d92-102">Before you begin</span></span>

<span data-ttu-id="21d92-103">Vérifiez que vous disposez des éléments ci-dessous avant de commencer votre configuration.</span><span class="sxs-lookup"><span data-stu-id="21d92-103">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="21d92-104">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="21d92-104">An Azure subscription.</span></span> <span data-ttu-id="21d92-105">Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="21d92-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="21d92-106">Vous devez installer la dernière version des applets de commande PowerShell Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="21d92-106">You need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="21d92-107">Pour plus d’informations, consultez la rubrique [Installation et configuration d’Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="21d92-107">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="21d92-108">Connexion à votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="21d92-108">Sign in to your Azure account</span></span>

<span data-ttu-id="21d92-109">Ouvrez la console PowerShell et connectez-vous à votre compte.</span><span class="sxs-lookup"><span data-stu-id="21d92-109">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="21d92-110">Pour en avoir plus, voir [Utilisation de Windows PowerShell avec Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="21d92-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-the-subscription"></a><span data-ttu-id="21d92-111">Sélection de l’abonnement</span><span class="sxs-lookup"><span data-stu-id="21d92-111">Select the subscription</span></span>
 
<span data-ttu-id="21d92-112">Vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="21d92-112">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="21d92-113">Parmi vos abonnements Azure, choisissez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="21d92-113">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="21d92-114">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="21d92-114">Create a resource group</span></span>

<span data-ttu-id="21d92-115">Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement.</span><span class="sxs-lookup"><span data-stu-id="21d92-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="21d92-116">Celui-ci est utilisé comme emplacement par défaut des ressources de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="21d92-116">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="21d92-117">Toutefois, étant donné que toutes les ressources DNS sont globales et non régionales, le choix de l’emplacement du groupe de ressources n’a aucun impact sur Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="21d92-117">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="21d92-118">Ignorez cette étape si vous utilisez un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="21d92-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="21d92-119">S’inscrire auprès du fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="21d92-119">Register resource provider</span></span>

<span data-ttu-id="21d92-120">Le service Azure DNS est géré par le fournisseur de ressources Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="21d92-120">The Azure DNS service is managed by the Microsoft.Network resource provider.</span></span> <span data-ttu-id="21d92-121">Votre abonnement Azure doit être enregistré auprès de ce fournisseur de ressources pour que vous puissiez utiliser Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="21d92-121">Your Azure subscription must be registered to use this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="21d92-122">Cette opération n’est à effectuer qu’une fois par abonnement.</span><span class="sxs-lookup"><span data-stu-id="21d92-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```