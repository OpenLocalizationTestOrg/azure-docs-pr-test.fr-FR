<span data-ttu-id="ff5a6-101">tooadd un groupe de ressources tooa de balise, utilisez **jeu de groupes azure**.</span><span class="sxs-lookup"><span data-stu-id="ff5a6-101">tooadd a tag tooa resource group, use **azure group set**.</span></span> <span data-ttu-id="ff5a6-102">Si le groupe de ressources hello n’a pas de balises existantes, passez dans la balise de hello.</span><span class="sxs-lookup"><span data-stu-id="ff5a6-102">If hello resource group does not have any existing tags, pass in hello tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="ff5a6-103">Les balises sont mises à jour en tant qu'ensemble.</span><span class="sxs-lookup"><span data-stu-id="ff5a6-103">Tags are updated as a whole.</span></span> <span data-ttu-id="ff5a6-104">Si vous souhaitez tooadd balise tooa groupe de ressources qui a des balises existantes, passer toutes les balises hello.</span><span class="sxs-lookup"><span data-stu-id="ff5a6-104">If you want tooadd a tag tooa resource group that has existing tags, pass all hello tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="ff5a6-105">Les balises ne sont pas héritées par les ressources d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="ff5a6-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="ff5a6-106">tooadd une ressource tooa de balise, utilisez **jeu de Ressources azure**.</span><span class="sxs-lookup"><span data-stu-id="ff5a6-106">tooadd a tag tooa resource, use **azure resource set**.</span></span> <span data-ttu-id="ff5a6-107">Passez hello numéro de version d’API pour le type de ressource hello que vous ajoutez la balise hello.</span><span class="sxs-lookup"><span data-stu-id="ff5a6-107">Pass hello API version number for hello resource type that you are adding hello tag to.</span></span> <span data-ttu-id="ff5a6-108">Si vous avez besoin de version de hello API tooretrieve, utilisez hello commande avec le fournisseur de ressources hello pour le type de hello que configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="ff5a6-108">If you need tooretrieve hello API version, use hello following command with hello resource provider for hello type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="ff5a6-109">Dans les résultats de hello, recherchez le type de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="ff5a6-109">In hello results, look for hello resource type you want.</span></span>

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

<span data-ttu-id="ff5a6-110">Ensuite, indiquez cette version d’API, le nom du groupe de ressources, le nom de la ressource, le type de la ressource et la valeur de balise sous forme de paramètres.</span><span class="sxs-lookup"><span data-stu-id="ff5a6-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="ff5a6-111">Les balises se trouvent directement dans les ressources et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="ff5a6-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="ff5a6-112">toosee les balises existantes hello, obtenir un groupe de ressources et ses ressources avec **afficher de groupe azure**.</span><span class="sxs-lookup"><span data-stu-id="ff5a6-112">toosee hello existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="ff5a6-113">Qui retourne des métadonnées sur le groupe de ressources hello, y compris toute tooit balises appliquées.</span><span class="sxs-lookup"><span data-stu-id="ff5a6-113">Which returns metadata about hello resource group, including any tags applied tooit.</span></span>

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

<span data-ttu-id="ff5a6-114">Vous permet d’afficher à l’aide de balises hello pour une ressource particulière **afficher des Ressources azure**.</span><span class="sxs-lookup"><span data-stu-id="ff5a6-114">You view hello tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="ff5a6-115">tooretrieve toutes les ressources hello avec une valeur de balise, utilisez :</span><span class="sxs-lookup"><span data-stu-id="ff5a6-115">tooretrieve all hello resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="ff5a6-116">tooretrieve tous les groupes de ressources hello avec une valeur de balise, utilisez :</span><span class="sxs-lookup"><span data-stu-id="ff5a6-116">tooretrieve all hello resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="ff5a6-117">Vous pouvez afficher les balises existantes hello dans votre abonnement avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ff5a6-117">You can view hello existing tags in your subscription with hello following command:</span></span>

```azurecli
azure tag list
```
