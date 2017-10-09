
## <a name="start-your-powershell-session"></a>Démarrer votre session PowerShell
Vous devez toohave hello dernières [Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) installés et en cours d’exécution. Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Hello d’exemples dans cette rubrique utilisent [modèle de déploiement Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md), de sorte que les exemples utilisent hello [applets de commande Azure Resource Manager](http://msdn.microsoft.com/library/azure/mt125356.aspx). 
> 
> 

Exécutez hello [ **Add-AzureRmAccount** ](http://msdn.microsoft.com/library/mt619267.aspx) applet de commande et vous verrez une tooenter d’écran de connexion vos informations d’identification. Utilisez hello mêmes informations d’identification que vous utilisez toosign dans toohello portail Azure.

    Add-AzureRmAccount

Si vous avez plusieurs abonnements utilisent hello [ **Set-AzureRmContext** ](http://msdn.microsoft.com/library/mt619263.aspx) tooselect d’applet de commande abonnement votre session PowerShell doit utiliser. toosee quel abonnement hello PowerShell actuel à l’aide de la session, exécutez [ **Get-AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx). l’exécution de tous les abonnements, toosee [ **Get-AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx).

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'

