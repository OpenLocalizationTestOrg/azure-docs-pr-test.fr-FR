1. <span data-ttu-id="a612f-101">Connectez-vous à votre abonnement Azure avec la commande [az login](/cli/azure/#login) et suivez les instructions à l’écran.</span><span class="sxs-lookup"><span data-stu-id="a612f-101">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> <span data-ttu-id="a612f-102">Pour plus d’informations sur la connexion, consultez [Prise en main d’Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a612f-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

  ```azurecli
  az login
  ```
2. <span data-ttu-id="a612f-103">Si vous disposez de plusieurs abonnements Azure, répertoriez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="a612f-103">If you have more than one Azure subscription, list the subscriptions for the account.</span></span>

  ```azurecli
  az account list --all
  ```
3. <span data-ttu-id="a612f-104">Spécifiez l’abonnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="a612f-104">Specify the subscription that you want to use.</span></span>

  ```azurecli
  az account set --subscription <replace_with_your_subscription_id>
  ```