1. Connectez-vous à tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran. Pour plus d’informations sur la connexion, consultez [Prise en main d’Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).

  ```azurecli
  az login
  ```
2. Si vous avez plusieurs abonnements Azure, liste des abonnements hello pour le compte de hello.

  ```azurecli
  az account list --all
  ```
3. Spécifiez un abonnement hello que vous souhaitez toouse.

  ```azurecli
  az account set --subscription <replace_with_your_subscription_id>
  ```