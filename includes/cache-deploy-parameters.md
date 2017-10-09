
### <a name="cacheskuname"></a><span data-ttu-id="c2b16-101">cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="c2b16-101">cacheSKUName</span></span>
<span data-ttu-id="c2b16-102">niveau de tarification Hello Hello nouveau Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="c2b16-102">hello pricing tier of hello new Azure Redis Cache.</span></span>

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "hello pricing tier of hello new Azure Redis Cache."
      }
    },

<span data-ttu-id="c2b16-103">modèle de Hello définit les valeurs hello sont autorisées pour ce paramètre (base ou Standard) et affecte la valeur par défaut (Basic) si aucune valeur n’est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="c2b16-103">hello template defines hello values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="c2b16-104">Basic fournit un nœud unique avec plusieurs tailles disponibles too53 go.</span><span class="sxs-lookup"><span data-stu-id="c2b16-104">Basic provides a single node with multiple sizes available up too53 GB.</span></span>
<span data-ttu-id="c2b16-105">Norme fournit deux nœuds principal/réplica avec plusieurs tailles disponibles too53 Go et 99,9 % de contrat SLA.</span><span class="sxs-lookup"><span data-stu-id="c2b16-105">Standard provides two-node Primary/Replica with multiple sizes available up too53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="c2b16-106">cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="c2b16-106">cacheSKUFamily</span></span>
<span data-ttu-id="c2b16-107">famille de Hello pour hello référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="c2b16-107">hello family for hello sku.</span></span>

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "hello family for hello sku."
      }
    },


### <a name="cacheskucapacity"></a><span data-ttu-id="c2b16-108">cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="c2b16-108">cacheSKUCapacity</span></span>
<span data-ttu-id="c2b16-109">taille de Hello de la nouvelle instance de Cache Redis Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c2b16-109">hello size of hello new Azure Redis Cache instance.</span></span> 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "hello size of hello new Azure Redis Cache instance. "
      }
    }


<span data-ttu-id="c2b16-110">modèle de Hello définit les valeurs hello qui sont autorisées pour ce paramètre (0, 1, 2, 3, 4, 5 ou 6) et affecte la valeur par défaut (1) si aucune valeur n’est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="c2b16-110">hello template defines hello values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="c2b16-111">Ces chiffres correspondent à des tailles de cache toofollowing : 0 = 250 Mo, 1 = 1 Go, 2 = 2,5 Go, 3 = 6 Go, 4 = 13 Go, 5 = 26 Go, 6 = 53 Go</span><span class="sxs-lookup"><span data-stu-id="c2b16-111">Those numbers correspond toofollowing cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

