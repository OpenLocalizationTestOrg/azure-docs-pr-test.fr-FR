Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.

[!INCLUDE [resource group intro text](resource-group.md)]

Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westeurope* emplacement.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Vous créez généralement votre ressource hello et groupe de ressources dans une région de près de chez vous. emplacements toosee tous pris en charge pour les applications Web Azure, exécutez hello `az appservice list-locations` commande. 
