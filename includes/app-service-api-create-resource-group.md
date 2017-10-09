Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.

[!INCLUDE [resource group intro text](resource-group.md)]

Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westeurope* emplacement.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

emplacements disponibles toosee hello, exécutez hello `az appservice list-locations` commande. Vous créez généralement des ressources dans une région proche de chez vous.
