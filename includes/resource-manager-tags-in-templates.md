tootag une ressource pendant le déploiement, ajoutez hello `tags` ressource d’élément toohello vous déployez. Fournir une valeur et le nom de la balise hello.

### <a name="apply-a-literal-value-toohello-tag-name"></a>Appliquer un nom de balise toohello valeur littérale
Hello suivant montre un compte de stockage avec deux balises (`Dept` et `Environment`) qui sont définies les valeurs tooliteral :

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

### <a name="apply-an-object-toohello-tag-element"></a>Appliquer un élément de balise d’objet toohello
Vous pouvez définir un paramètre d’objet qui stocke plusieurs balises et s’appliquent à cet élément de balise toohello objet. Chaque propriété de l’objet de hello devient une balise distincte pour la ressource de hello. exemple Hello possède un paramètre nommé `tagValues` qui est un élément balise toohello appliqué.

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

### <a name="apply-a-json-string-toohello-tag-name"></a>Appliquer un nom de balise toohello chaîne JSON

toostore nombre de valeurs dans une balise unique, appliquer une chaîne JSON qui représente les valeurs hello. chaîne JSON entière de Hello est stockée en tant qu’une seule balise ne peut pas dépasser 256 caractères. exemple Hello possède une balise unique nommée `CostCenter` qui contient plusieurs valeurs à partir d’une chaîne JSON :  

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