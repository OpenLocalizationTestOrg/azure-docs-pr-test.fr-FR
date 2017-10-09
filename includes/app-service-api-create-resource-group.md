<span data-ttu-id="429b8-101">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="429b8-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="429b8-102">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westeurope* emplacement.</span><span class="sxs-lookup"><span data-stu-id="429b8-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="429b8-103">emplacements disponibles toosee hello, exécutez hello `az appservice list-locations` commande.</span><span class="sxs-lookup"><span data-stu-id="429b8-103">toosee hello available locations, run hello `az appservice list-locations` command.</span></span> <span data-ttu-id="429b8-104">Vous créez généralement des ressources dans une région proche de chez vous.</span><span class="sxs-lookup"><span data-stu-id="429b8-104">You generally create resources in a region near you.</span></span>
