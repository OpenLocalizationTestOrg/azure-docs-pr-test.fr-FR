### <a name="troubleshoot-azure-diagnostics"></a><span data-ttu-id="c04c4-101">Résoudre les problèmes d’Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="c04c4-101">Troubleshoot Azure Diagnostics</span></span>

<span data-ttu-id="c04c4-102">Si vous recevez hello message d’erreur suivant, le fournisseur de ressources Microsoft.insights hello n’est pas enregistrée :</span><span class="sxs-lookup"><span data-stu-id="c04c4-102">If you receive hello following error message, hello Microsoft.insights resource provider is not registered:</span></span>

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

<span data-ttu-id="c04c4-103">fournisseur de ressources tooregister hello, effectuer hello Bonjour portail Azure comme suit :</span><span class="sxs-lookup"><span data-stu-id="c04c4-103">tooregister hello resource provider, perform hello following steps in hello Azure portal:</span></span>

1.  <span data-ttu-id="c04c4-104">Dans le volet de navigation hello hello gauche, cliquez sur *abonnements*</span><span class="sxs-lookup"><span data-stu-id="c04c4-104">In hello navigation pane on hello left, click *Subscriptions*</span></span>
2.  <span data-ttu-id="c04c4-105">Sélectionnez l’abonnement hello identifié dans le message d’erreur hello</span><span class="sxs-lookup"><span data-stu-id="c04c4-105">Select hello subscription identified in hello error message</span></span>
3.  <span data-ttu-id="c04c4-106">Cliquez sur *Fournisseurs de ressources*</span><span class="sxs-lookup"><span data-stu-id="c04c4-106">Click *Resource Providers*</span></span>
4.  <span data-ttu-id="c04c4-107">Recherche hello *Microsoft.insights* fournisseur</span><span class="sxs-lookup"><span data-stu-id="c04c4-107">Find hello *Microsoft.insights* provider</span></span>
5.  <span data-ttu-id="c04c4-108">Cliquez sur hello *inscrire* lien</span><span class="sxs-lookup"><span data-stu-id="c04c4-108">Click hello *Register* link</span></span>

![Enregistrez le fournisseur de ressources microsoft.insights](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

<span data-ttu-id="c04c4-110">Une fois hello *Microsoft.insights* fournisseur de ressources est enregistré, puis réessayez la configuration des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="c04c4-110">Once hello *Microsoft.insights* resource provider is registered, retry configuring diagnostics.</span></span>


<span data-ttu-id="c04c4-111">Dans PowerShell, si vous recevez hello après le message d’erreur, vous devez tooupdate votre version de PowerShell :</span><span class="sxs-lookup"><span data-stu-id="c04c4-111">In PowerShell, if you receive hello following error message, you need tooupdate your version of PowerShell:</span></span>

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

<span data-ttu-id="c04c4-112">Mettre à jour votre version de PowerShell toohello novembre 2016 (v2.3.0) ou une version plus récente, à l’aide des instructions de hello Bonjour [prise en main des applets de commande Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) l’article.</span><span class="sxs-lookup"><span data-stu-id="c04c4-112">Update your version of PowerShell toohello November 2016 (v2.3.0), or later, release using hello instructions in hello [Get started with Azure PowerShell cmdlets](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) article.</span></span>
