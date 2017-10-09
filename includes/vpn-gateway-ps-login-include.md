<span data-ttu-id="429b5-101">Avant de commencer cette configuration, vous devez vous connecter tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="429b5-101">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="429b5-102">applet de commande Hello vous demande des informations d’identification de connexion hello pour votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="429b5-102">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="429b5-103">Une fois connecté, il télécharge les paramètres de votre compte afin qu’ils soient disponible tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="429b5-103">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span> <span data-ttu-id="429b5-104">Pour plus d’informations, consultez la page [Utilisation de Windows PowerShell avec Resource Manager](../articles/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="429b5-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="429b5-105">toolog, ouvrez la console PowerShell avec des privilèges élevés et tooyour compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="429b5-105">toolog in, open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="429b5-106">Utilisez hello suivant toohelp exemple que vous connectez :</span><span class="sxs-lookup"><span data-stu-id="429b5-106">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="429b5-107">Si vous avez plusieurs abonnements Azure, vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="429b5-107">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="429b5-108">Spécifiez un abonnement hello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="429b5-108">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```