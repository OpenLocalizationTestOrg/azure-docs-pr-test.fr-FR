<span data-ttu-id="ed0a3-101">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ed0a3-101">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="ed0a3-102">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *westeurope*.</span><span class="sxs-lookup"><span data-stu-id="ed0a3-102">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="ed0a3-103">Pour visualiser les emplacements disponibles, exécutez la commande `az appservice list-locations`.</span><span class="sxs-lookup"><span data-stu-id="ed0a3-103">To see the available locations, run the `az appservice list-locations` command.</span></span> <span data-ttu-id="ed0a3-104">Vous créez généralement des ressources dans une région proche de chez vous.</span><span class="sxs-lookup"><span data-stu-id="ed0a3-104">You generally create resources in a region near you.</span></span>
