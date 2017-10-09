tooadd un groupe de ressources tooa de balise, utilisez **jeu de groupes azure**. Si le groupe de ressources hello n’a pas de balises existantes, passez dans la balise de hello.

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

Les balises sont mises à jour en tant qu'ensemble. Si vous souhaitez tooadd balise tooa groupe de ressources qui a des balises existantes, passer toutes les balises hello. 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

Les balises ne sont pas héritées par les ressources d’un groupe de ressources. tooadd une ressource tooa de balise, utilisez **jeu de Ressources azure**. Passez hello numéro de version d’API pour le type de ressource hello que vous ajoutez la balise hello. Si vous avez besoin de version de hello API tooretrieve, utilisez hello commande avec le fournisseur de ressources hello pour le type de hello que configuration suivante :

```azurecli
azure provider show -n Microsoft.Storage --json
```

Dans les résultats de hello, recherchez le type de ressource hello.

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

Ensuite, indiquez cette version d’API, le nom du groupe de ressources, le nom de la ressource, le type de la ressource et la valeur de balise sous forme de paramètres.

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

Les balises se trouvent directement dans les ressources et les groupes de ressources. toosee les balises existantes hello, obtenir un groupe de ressources et ses ressources avec **afficher de groupe azure**.

```azurecli
azure group show -n tag-demo-group --json
```

Qui retourne des métadonnées sur le groupe de ressources hello, y compris toute tooit balises appliquées.

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

Vous permet d’afficher à l’aide de balises hello pour une ressource particulière **afficher des Ressources azure**.

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

tooretrieve toutes les ressources hello avec une valeur de balise, utilisez :

```azurecli
azure resource list -t Dept=Finance --json
```

tooretrieve tous les groupes de ressources hello avec une valeur de balise, utilisez :

```azurecli
azure group list -t Dept=Finance
```

Vous pouvez afficher les balises existantes hello dans votre abonnement avec hello de commande suivante :

```azurecli
azure tag list
```
