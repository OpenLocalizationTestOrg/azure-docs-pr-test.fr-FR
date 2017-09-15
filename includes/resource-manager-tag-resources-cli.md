<span data-ttu-id="8da96-101">Pour ajouter une balise à un groupe de ressources, utilisez **azure group set**.</span><span class="sxs-lookup"><span data-stu-id="8da96-101">To add a tag to a resource group, use **azure group set**.</span></span> <span data-ttu-id="8da96-102">Si le groupe de ressources ne comporte aucune balise, transmettez la balise.</span><span class="sxs-lookup"><span data-stu-id="8da96-102">If the resource group does not have any existing tags, pass in the tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="8da96-103">Les balises sont mises à jour en tant qu'ensemble.</span><span class="sxs-lookup"><span data-stu-id="8da96-103">Tags are updated as a whole.</span></span> <span data-ttu-id="8da96-104">Si vous souhaitez ajouter une balise à un groupe de ressources comportant déjà des balises, transmettez toutes les balises.</span><span class="sxs-lookup"><span data-stu-id="8da96-104">If you want to add a tag to a resource group that has existing tags, pass all the tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="8da96-105">Les balises ne sont pas héritées par les ressources d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8da96-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="8da96-106">Pour ajouter une balise à une ressource, utilisez **azure resource set**.</span><span class="sxs-lookup"><span data-stu-id="8da96-106">To add a tag to a resource, use **azure resource set**.</span></span> <span data-ttu-id="8da96-107">Transmettez le numéro de version d’API associé au type de ressource auquel vous ajoutez la balise.</span><span class="sxs-lookup"><span data-stu-id="8da96-107">Pass the API version number for the resource type that you are adding the tag to.</span></span> <span data-ttu-id="8da96-108">Si vous avez besoin de récupérer la version d’API, utilisez la commande ci-après avec le fournisseur de ressources pour le type que vous définissez :</span><span class="sxs-lookup"><span data-stu-id="8da96-108">If you need to retrieve the API version, use the following command with the resource provider for the type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="8da96-109">Dans les résultats, recherchez le type de ressource souhaité.</span><span class="sxs-lookup"><span data-stu-id="8da96-109">In the results, look for the resource type you want.</span></span>

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

<span data-ttu-id="8da96-110">Ensuite, indiquez cette version d’API, le nom du groupe de ressources, le nom de la ressource, le type de la ressource et la valeur de balise sous forme de paramètres.</span><span class="sxs-lookup"><span data-stu-id="8da96-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="8da96-111">Les balises se trouvent directement dans les ressources et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="8da96-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="8da96-112">Pour afficher les balises existantes, récupérez un groupe de ressources ainsi que ses ressources avec **azure group show**.</span><span class="sxs-lookup"><span data-stu-id="8da96-112">To see the existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="8da96-113">Ce qui renvoie des métadonnées sur le groupe de ressources, y compris toutes les balises appliquées.</span><span class="sxs-lookup"><span data-stu-id="8da96-113">Which returns metadata about the resource group, including any tags applied to it.</span></span>

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

<span data-ttu-id="8da96-114">Vous affichez les balises d’une ressource spécifique avec **azure resource show**.</span><span class="sxs-lookup"><span data-stu-id="8da96-114">You view the tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="8da96-115">Pour récupérer toutes les ressources avec une valeur de balise, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8da96-115">To retrieve all the resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="8da96-116">Pour récupérer tous les groupes de ressources avec une valeur de balise, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8da96-116">To retrieve all the resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="8da96-117">Vous pouvez visualiser les balises existantes dans votre abonnement avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8da96-117">You can view the existing tags in your subscription with the following command:</span></span>

```azurecli
azure tag list
```
