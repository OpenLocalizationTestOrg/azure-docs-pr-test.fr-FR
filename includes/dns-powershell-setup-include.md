## <a name="set-up-azure-powershell-for-azure-dns"></a>Configurer Azure PowerShell pour Azure DNS

### <a name="before-you-begin"></a>Avant de commencer

Vérifiez que vous disposez des éléments suivants avant de commencer votre configuration de hello.

* Un abonnement Azure. Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).
* Vous devez tooinstall hello dernière version de hello applets de commande PowerShell de gestionnaire de ressources Azure. Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="sign-in-tooyour-azure-account"></a>Se connecter tooyour compte Azure

Ouvrez la console PowerShell et tooyour compte de connexion. Pour en avoir plus, voir [Utilisation de Windows PowerShell avec Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a>Sélectionnez l’abonnement de hello
 
Vérifiez les abonnements hello pour le compte de hello.

```powershell
Get-AzureRmSubscription
```

Choisissez parmi vos toouse abonnements Azure.

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a>Créer un groupe de ressources

Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement. Cet emplacement est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources. Toutefois, étant donné que toutes les ressources DNS sont globales, pas régional, choix hello de l’emplacement du groupe de ressources n’a aucun impact sur le système DNS Azure.

Ignorez cette étape si vous utilisez un groupe de ressources existant.

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a>S’inscrire auprès du fournisseur de ressources

Hello service DNS Azure est géré par le fournisseur de ressources Microsoft.Network hello. Votre abonnement Azure doit d’être toouse inscrit ce fournisseur de ressources avant de pouvoir utiliser Azure DNS. Cette opération n’est à effectuer qu’une fois par abonnement.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```