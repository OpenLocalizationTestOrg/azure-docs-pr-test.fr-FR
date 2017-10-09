<span data-ttu-id="f6b1b-101">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="f6b1b-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="f6b1b-102">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westeurope* emplacement.</span><span class="sxs-lookup"><span data-stu-id="f6b1b-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="f6b1b-103">Vous créez généralement votre ressource hello et groupe de ressources dans une région de près de chez vous.</span><span class="sxs-lookup"><span data-stu-id="f6b1b-103">You generally create your resource group and hello resources in a region near you.</span></span> <span data-ttu-id="f6b1b-104">emplacements toosee tous pris en charge pour les applications Web Azure, exécutez hello `az appservice list-locations` commande.</span><span class="sxs-lookup"><span data-stu-id="f6b1b-104">toosee all supported locations for Azure Web Apps, run hello `az appservice list-locations` command.</span></span> 
