<span data-ttu-id="d7059-101">Pour marquer une ressource au cours du déploiement, ajoutez l’élément `tags` à la ressource que vous déployez.</span><span class="sxs-lookup"><span data-stu-id="d7059-101">To tag a resource during deployment, add the `tags` element to the resource you are deploying.</span></span> <span data-ttu-id="d7059-102">Indiquez le nom et la valeur de la balise.</span><span class="sxs-lookup"><span data-stu-id="d7059-102">Provide the tag name and value.</span></span>

### <a name="apply-a-literal-value-to-the-tag-name"></a><span data-ttu-id="d7059-103">Appliquer une valeur littérale au nom de balise</span><span class="sxs-lookup"><span data-stu-id="d7059-103">Apply a literal value to the tag name</span></span>
<span data-ttu-id="d7059-104">L’exemple suivant illustre un compte de stockage avec deux balises (`Dept` et `Environment`) définies sur des valeurs littérales :</span><span class="sxs-lookup"><span data-stu-id="d7059-104">The following example shows a storage account with two tags (`Dept` and `Environment`) that are set to literal values:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

### <a name="apply-an-object-to-the-tag-element"></a><span data-ttu-id="d7059-105">Appliquer un objet à l’élément de balise</span><span class="sxs-lookup"><span data-stu-id="d7059-105">Apply an object to the tag element</span></span>
<span data-ttu-id="d7059-106">Vous pouvez définir un paramètre d’objet qui stocke plusieurs balises et appliquer cet objet à l’élément de balise.</span><span class="sxs-lookup"><span data-stu-id="d7059-106">You can define an object parameter that stores several tags, and apply that object to the tag element.</span></span> <span data-ttu-id="d7059-107">Chaque propriété de l’objet devient une balise distincte pour la ressource.</span><span class="sxs-lookup"><span data-stu-id="d7059-107">Each property in the object becomes a separate tag for the resource.</span></span> <span data-ttu-id="d7059-108">L’exemple suivant illustre un paramètre nommé `tagValues` appliqué à l’élément de balise.</span><span class="sxs-lookup"><span data-stu-id="d7059-108">The following example has a parameter named `tagValues` that is applied to the tag element.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "tagValues": {
      "type": "object",
      "defaultValue": {
        "Dept": "Finance",
        "Environment": "Production"
      }
    }
  },
  "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": "[parameters('tagValues')]",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": {}
    }
  ]
}
```

### <a name="apply-a-json-string-to-the-tag-name"></a><span data-ttu-id="d7059-109">Appliquer une chaîne JSON au nom de balise</span><span class="sxs-lookup"><span data-stu-id="d7059-109">Apply a JSON string to the tag name</span></span>

<span data-ttu-id="d7059-110">Pour stocker plusieurs valeurs dans une seule balise, appliquez une chaîne JSON qui représente les valeurs.</span><span class="sxs-lookup"><span data-stu-id="d7059-110">To store many values in a single tag, apply a JSON string that represents the values.</span></span> <span data-ttu-id="d7059-111">La chaîne JSON complète est stockée sous la forme d’une balise ne pouvant pas dépasser 256 caractères.</span><span class="sxs-lookup"><span data-stu-id="d7059-111">The entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="d7059-112">L’exemple illustre une balise unique nommée `CostCenter` qui contient plusieurs valeurs d’une chaîne JSON :</span><span class="sxs-lookup"><span data-stu-id="d7059-112">The following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storage', uniqueString(resourceGroup().id))]",
      "location": "[resourceGroup().location]",
      "tags": {
        "CostCenter": "{\"Dept\":\"Finance\",\"Environment\":\"Production\"}"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```