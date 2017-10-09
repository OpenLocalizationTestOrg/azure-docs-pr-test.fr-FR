<span data-ttu-id="cb122-101">tootag une ressource pendant le déploiement, ajoutez hello `tags` ressource d’élément toohello vous déployez.</span><span class="sxs-lookup"><span data-stu-id="cb122-101">tootag a resource during deployment, add hello `tags` element toohello resource you are deploying.</span></span> <span data-ttu-id="cb122-102">Fournir une valeur et le nom de la balise hello.</span><span class="sxs-lookup"><span data-stu-id="cb122-102">Provide hello tag name and value.</span></span>

### <a name="apply-a-literal-value-toohello-tag-name"></a><span data-ttu-id="cb122-103">Appliquer un nom de balise toohello valeur littérale</span><span class="sxs-lookup"><span data-stu-id="cb122-103">Apply a literal value toohello tag name</span></span>
<span data-ttu-id="cb122-104">Hello suivant montre un compte de stockage avec deux balises (`Dept` et `Environment`) qui sont définies les valeurs tooliteral :</span><span class="sxs-lookup"><span data-stu-id="cb122-104">hello following example shows a storage account with two tags (`Dept` and `Environment`) that are set tooliteral values:</span></span>

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

### <a name="apply-an-object-toohello-tag-element"></a><span data-ttu-id="cb122-105">Appliquer un élément de balise d’objet toohello</span><span class="sxs-lookup"><span data-stu-id="cb122-105">Apply an object toohello tag element</span></span>
<span data-ttu-id="cb122-106">Vous pouvez définir un paramètre d’objet qui stocke plusieurs balises et s’appliquent à cet élément de balise toohello objet.</span><span class="sxs-lookup"><span data-stu-id="cb122-106">You can define an object parameter that stores several tags, and apply that object toohello tag element.</span></span> <span data-ttu-id="cb122-107">Chaque propriété de l’objet de hello devient une balise distincte pour la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="cb122-107">Each property in hello object becomes a separate tag for hello resource.</span></span> <span data-ttu-id="cb122-108">exemple Hello possède un paramètre nommé `tagValues` qui est un élément balise toohello appliqué.</span><span class="sxs-lookup"><span data-stu-id="cb122-108">hello following example has a parameter named `tagValues` that is applied toohello tag element.</span></span>

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

### <a name="apply-a-json-string-toohello-tag-name"></a><span data-ttu-id="cb122-109">Appliquer un nom de balise toohello chaîne JSON</span><span class="sxs-lookup"><span data-stu-id="cb122-109">Apply a JSON string toohello tag name</span></span>

<span data-ttu-id="cb122-110">toostore nombre de valeurs dans une balise unique, appliquer une chaîne JSON qui représente les valeurs hello.</span><span class="sxs-lookup"><span data-stu-id="cb122-110">toostore many values in a single tag, apply a JSON string that represents hello values.</span></span> <span data-ttu-id="cb122-111">chaîne JSON entière de Hello est stockée en tant qu’une seule balise ne peut pas dépasser 256 caractères.</span><span class="sxs-lookup"><span data-stu-id="cb122-111">hello entire JSON string is stored as one tag that cannot exceed 256 characters.</span></span> <span data-ttu-id="cb122-112">exemple Hello possède une balise unique nommée `CostCenter` qui contient plusieurs valeurs à partir d’une chaîne JSON :</span><span class="sxs-lookup"><span data-stu-id="cb122-112">hello following example has a single tag named `CostCenter` that contains several values from a JSON string:</span></span>  

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