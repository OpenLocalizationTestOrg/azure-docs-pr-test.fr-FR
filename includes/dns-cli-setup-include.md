## <a name="set-up-azure-cli-for-azure-dns"></a>Configuration de l’interface de ligne de commande Azure pour Azure DNS

### <a name="before-you-begin"></a>Avant de commencer

Vérifiez que vous disposez des éléments suivants avant de commencer votre configuration de hello.

* Un abonnement Azure. Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).
* Installez hello dernière version de hello CLI d’Azure, disponible pour Windows, Linux ou Mac. Plus d’informations est disponible à l’adresse [installation Bonjour Azure CLI](../articles/cli-install-nodejs.md).

### <a name="sign-in-tooyour-azure-account"></a>Se connecter tooyour compte Azure

Ouvrez une fenêtre de console et procédez à l’authentification à l’aide de vos informations d’identification. Pour plus d’informations, consultez [connecter tooAzure de hello CLI d’Azure](../articles/xplat-cli-connect.md)

```azurecli
azure login
```

### <a name="switch-cli-mode"></a>Passage en mode CLI

Azure DNS utilise Azure Resource Manager. Assurez-vous que vous passez des commandes CLI mode toouse Azure Resource Manager.

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a>Sélectionnez l’abonnement de hello

Vérifiez les abonnements hello pour le compte de hello.

```azurecli
azure account list
```

Choisissez parmi vos toouse abonnements Azure.

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a>Créer un groupe de ressources

Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement. Cela est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources. Toutefois, étant donné que toutes les ressources DNS sont globales, pas régional, choix hello de l’emplacement du groupe de ressources n’a aucun impact sur le système DNS Azure.

Ignorez cette étape si vous utilisez un groupe de ressources existant.

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a>S’inscrire auprès du fournisseur de ressources

Hello service DNS Azure est géré par le fournisseur de ressources Microsoft.Network hello. Votre abonnement Azure doit d’être toouse inscrit ce fournisseur de ressources avant de pouvoir utiliser Azure DNS. Cette opération n’est à effectuer qu’une fois par abonnement.

```azurecli
azure provider register --namespace Microsoft.Network
```

