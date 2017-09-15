<span data-ttu-id="1fa4c-101">Avant de commencer cette configuration, vous devez vous connecter à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="1fa4c-101">Before beginning this configuration, you must log in to your Azure account.</span></span> <span data-ttu-id="1fa4c-102">Les applets de commande vous invitent à entrer les informations d’identification de connexion pour votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="1fa4c-102">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="1fa4c-103">Une fois que vous êtes connecté, l’applet de commande télécharge vos paramètres de compte pour qu’ils soient reconnus par Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1fa4c-103">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span> <span data-ttu-id="1fa4c-104">Pour plus d’informations, consultez la page [Utilisation de Windows PowerShell avec Resource Manager](../articles/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1fa4c-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="1fa4c-105">Pour vous connecter, ouvrez la console PowerShell avec des privilèges élevés et connectez-vous à votre compte.</span><span class="sxs-lookup"><span data-stu-id="1fa4c-105">To log in, open your PowerShell console with elevated privileges, and connect to your account.</span></span> <span data-ttu-id="1fa4c-106">Utilisez l’exemple suivant pour faciliter votre connexion :</span><span class="sxs-lookup"><span data-stu-id="1fa4c-106">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="1fa4c-107">Si vous disposez de plusieurs abonnements Azure, vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="1fa4c-107">If you have multiple Azure subscriptions, check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="1fa4c-108">Spécifiez l’abonnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="1fa4c-108">Specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```