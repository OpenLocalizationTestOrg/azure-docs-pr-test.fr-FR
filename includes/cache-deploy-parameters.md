
### <a name="cacheskuname"></a><span data-ttu-id="3c5e0-101">cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="3c5e0-101">cacheSKUName</span></span>
<span data-ttu-id="3c5e0-102">Niveau de tarification du nouveau Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="3c5e0-102">The pricing tier of the new Azure Redis Cache.</span></span>

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "The pricing tier of the new Azure Redis Cache."
      }
    },

<span data-ttu-id="3c5e0-103">Le modèle définit les valeurs autorisées pour ce paramètre (De base ou Standard) et affecte une valeur par défaut (De base) si aucune valeur n’est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="3c5e0-103">The template defines the values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="3c5e0-104">Le niveau De base fournit un nœud unique disponible en plusieurs tailles, jusqu’à 53 Go.</span><span class="sxs-lookup"><span data-stu-id="3c5e0-104">Basic provides a single node with multiple sizes available up to 53 GB.</span></span>
<span data-ttu-id="3c5e0-105">Le niveau Standard fournit deux nœuds primaire/réplica disponibles en plusieurs tailles jusqu’à 53 Go et un contrat SLA de 99,9 %.</span><span class="sxs-lookup"><span data-stu-id="3c5e0-105">Standard provides two-node Primary/Replica with multiple sizes available up to 53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="3c5e0-106">cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="3c5e0-106">cacheSKUFamily</span></span>
<span data-ttu-id="3c5e0-107">Famille de la référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="3c5e0-107">The family for the sku.</span></span>

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "The family for the sku."
      }
    },


### <a name="cacheskucapacity"></a><span data-ttu-id="3c5e0-108">cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="3c5e0-108">cacheSKUCapacity</span></span>
<span data-ttu-id="3c5e0-109">Taille de la nouvelle instance de Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="3c5e0-109">The size of the new Azure Redis Cache instance.</span></span> 

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
        "description": "The size of the new Azure Redis Cache instance. "
      }
    }


<span data-ttu-id="3c5e0-110">Le modèle définit les valeurs autorisées pour ce paramètre (0, 1, 2, 3, 4, 5 ou 6) et affecte une valeur par défaut (1) si aucune valeur n’est spécifiée.</span><span class="sxs-lookup"><span data-stu-id="3c5e0-110">The template defines the values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="3c5e0-111">Ces chiffres correspondent aux tailles de cache suivantes : 0 = 250 Mo, 1 = 1 Go, 2 = 2,5 Go, 3 = 6 Go, 4 = 13 Go, 5 = 26 Go, 6 = 53 Go</span><span class="sxs-lookup"><span data-stu-id="3c5e0-111">Those numbers correspond to following cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

