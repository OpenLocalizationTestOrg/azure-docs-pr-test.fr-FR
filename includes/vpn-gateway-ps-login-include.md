Avant de commencer cette configuration, vous devez vous connecter tooyour compte Azure. applet de commande Hello vous demande des informations d’identification de connexion hello pour votre compte Azure. Une fois connecté, il télécharge les paramètres de votre compte afin qu’ils soient disponible tooAzure PowerShell. Pour plus d’informations, consultez la page [Utilisation de Windows PowerShell avec Resource Manager](../articles/powershell-azure-resource-manager.md).

toolog, ouvrez la console PowerShell avec des privilèges élevés et tooyour compte de connexion. Utilisez hello suivant toohelp exemple que vous connectez :

```powershell
Login-AzureRmAccount
```

Si vous avez plusieurs abonnements Azure, vérifiez les abonnements hello pour le compte de hello.

```powershell
Get-AzureRmSubscription
```

Spécifiez un abonnement hello que vous souhaitez toouse.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```