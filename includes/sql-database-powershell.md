
## <a name="start-your-powershell-session"></a>Démarrer votre session PowerShell
Tout d’abord, vous devez hello dernière Azure PowerShell installé et en cours d’exécution. Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Plusieurs nouvelles fonctionnalités de base de données SQL seulement sont pris en charge que lorsque vous utilisez hello [modèle de déploiement Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md), de sorte que les exemples utilisent hello [applets de commande PowerShell de base de données SQL Azure](https://msdn.microsoft.com/library/azure/mt574084\(v=azure.300\).aspx) pour le Gestionnaire de ressources . modèle de déploiement de gestion (classiques) service Hello [applets de commande de gestion des services de base de données SQL Azure](https://msdn.microsoft.com/library/azure/dn546723\(v=azure.300\).aspx) sont pris en charge pour la compatibilité descendante, mais nous vous recommandons d’utiliser hello applets de commande Gestionnaire de ressources.
> 
> 

Exécutez hello [ **Add-AzureRmAccount** ](https://msdn.microsoft.com/library/azure/mt619267\(v=azure.300\).aspx) applet de commande et vous aurez un écran de connexion de tooenter vos informations d’identification. Utilisez hello mêmes informations d’identification que vous utilisez toosign dans toohello portail Azure.

```PowerShell
Add-AzureRmAccount
```

Si vous avez plusieurs abonnements, utilisez hello [ **Set-AzureRmContext** ](https://msdn.microsoft.com/library/azure/mt619263\(v=azure.300\).aspx) tooselect d’applet de commande abonnement votre session PowerShell doit utiliser. toosee quel abonnement hello PowerShell actuel à l’aide de la session, exécutez [ **Get-AzureRmContext**](https://msdn.microsoft.com/library/azure/mt619265\(v=azure.300\).aspx). l’exécution de tous les abonnements, toosee [ **Get-AzureRmSubscription**](https://msdn.microsoft.com/library/azure/mt619284\(v=azure.300\).aspx).

```PowerShell
Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'
```
