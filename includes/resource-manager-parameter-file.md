Si vous utilisez un valeurs du paramètre paramètre fichier toopass pendant le déploiement, vous devez toocreate un fichier JSON avec un toohello même format que l’exemple suivant :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "webSiteName": {
            "value": "ExampleSite"
        },
        "webSiteHostingPlanName": {
            "value": "DefaultPlan"
        },
        "webSiteLocation": {
            "value": "West US"
        },
        "adminPassword": {
            "reference": {
               "keyVault": {
                  "id": "/subscriptions/{guid}/resourceGroups/{group-name}/providers/Microsoft.KeyVault/vaults/{vault-name}"
               }, 
               "secretName": "sqlAdminPassword" 
            }   
        }
   }
}
```

taille de Hello du fichier de paramètres hello ne peut pas être supérieure à 64 Ko.

Si vous devez tooprovide une valeur sensible pour un paramètre (par exemple, un mot de passe), ajoutez ce coffre de clés de tooa de valeur. Récupérer le coffre de clés hello lors du déploiement, comme indiqué dans l’exemple précédent de hello. Pour plus d’informations, consultez [Passage de valeurs sécurisés pendant le déploiement](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md). 

