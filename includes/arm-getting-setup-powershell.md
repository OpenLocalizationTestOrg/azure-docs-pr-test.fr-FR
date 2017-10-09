## <a name="setting-up-powershell-for-resource-manager-templates"></a><span data-ttu-id="044fc-101">Configuration de PowerShell pour les modèles du Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="044fc-101">Setting up PowerShell for Resource Manager templates</span></span>
<span data-ttu-id="044fc-102">Avant de pouvoir utiliser Azure PowerShell avec le Gestionnaire de ressources, vous devez les versions de hello de toohave appropriées de Windows PowerShell et d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="044fc-102">Before you can use Azure PowerShell with Resource Manager, you will need toohave hello right Windows PowerShell and Azure PowerShell versions.</span></span>

### <a name="verify-powershell-versions"></a><span data-ttu-id="044fc-103">Vérifier les versions de PowerShell</span><span class="sxs-lookup"><span data-stu-id="044fc-103">Verify PowerShell versions</span></span>
<span data-ttu-id="044fc-104">Vérifiez que vous avez Windows PowerShell version 3.0 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="044fc-104">Verify you have Windows PowerShell version 3.0 or 4.0.</span></span> <span data-ttu-id="044fc-105">version de hello toofind de Windows PowerShell, tapez cette commande à une invite de commandes Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="044fc-105">toofind hello version of Windows PowerShell, type this command at a Windows PowerShell command prompt.</span></span>

    $PSVersionTable

<span data-ttu-id="044fc-106">Vous recevrez hello suivant le type d’informations :</span><span class="sxs-lookup"><span data-stu-id="044fc-106">You will receive hello following type of information:</span></span>

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


<span data-ttu-id="044fc-107">Vérifiez que la valeur de hello **PSVersion** est 3.0 ou 4.0.</span><span class="sxs-lookup"><span data-stu-id="044fc-107">Verify that hello value of **PSVersion** is 3.0 or 4.0.</span></span> <span data-ttu-id="044fc-108">Dans le cas contraire, consultez l’article [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) ou [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="044fc-108">If not, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="044fc-109">Configurer votre compte et votre abonnement Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="044fc-109">Set your Azure account and subscription</span></span>
<span data-ttu-id="044fc-110">Si vous ne possédez pas encore un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou vous inscrire pour une [version d’évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="044fc-110">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="044fc-111">Ouvrez une invite de commandes Azure PowerShell et connectez-vous à tooAzure avec cette commande.</span><span class="sxs-lookup"><span data-stu-id="044fc-111">Open an Azure PowerShell command prompt and log on tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="044fc-112">Si vous avez plusieurs abonnements Azure, vous pouvez les répertorier avec cette commande.</span><span class="sxs-lookup"><span data-stu-id="044fc-112">If you have multiple Azure subscriptions, you can list your Azure subscriptions with this command.</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="044fc-113">Vous recevrez hello suivant le type d’informations :</span><span class="sxs-lookup"><span data-stu-id="044fc-113">You will receive hello following type of information:</span></span>

    SubscriptionId            : fd22919d-eaca-4f2b-841a-e4ac6770g92e
    SubscriptionName          : Visual Studio Ultimate with MSDN
    Environment               : AzureCloud
    SupportedModes            : AzureServiceManagement,AzureResourceManager
    DefaultAccount            : johndoe@contoso.com
    Accounts                  : {johndoe@contoso.com}
    IsDefault                 : True
    IsCurrent                 : True
    CurrentStorageAccountName :
    TenantId                  : 32fa88b4-86f1-419f-93ab-2d7ce016dba7

<span data-ttu-id="044fc-114">Vous pouvez définir l’abonnement Azure hello en exécutant ces commandes à l’invite de commande Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="044fc-114">You can set hello current Azure subscription by running these commands at hello Azure PowerShell command prompt.</span></span> <span data-ttu-id="044fc-115">Remplacez tout le contenu du devis hello, notamment hello < et >, avec le nom correct de hello.</span><span class="sxs-lookup"><span data-stu-id="044fc-115">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

<span data-ttu-id="044fc-116">Pour plus d’informations sur les comptes et les abonnements Azure, consultez [Comment : se connecter tooyour abonnement](/powershell/azureps-cmdlets-docs#step-3-connect).</span><span class="sxs-lookup"><span data-stu-id="044fc-116">For more information about Azure subscriptions and accounts, see [How to: Connect tooyour subscription](/powershell/azureps-cmdlets-docs#step-3-connect).</span></span>

