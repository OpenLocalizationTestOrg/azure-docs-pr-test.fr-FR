<span data-ttu-id="b8f25-101">Si vous utilisez un valeurs du paramètre paramètre fichier toopass pendant le déploiement, vous devez toocreate un fichier JSON avec un toohello même format que l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b8f25-101">If you use a parameter file toopass parameter values during deployment, you need toocreate a JSON file with a format similar toohello following example:</span></span>

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

<span data-ttu-id="b8f25-102">taille de Hello du fichier de paramètres hello ne peut pas être supérieure à 64 Ko.</span><span class="sxs-lookup"><span data-stu-id="b8f25-102">hello size of hello parameter file cannot be more than 64 KB.</span></span>

<span data-ttu-id="b8f25-103">Si vous devez tooprovide une valeur sensible pour un paramètre (par exemple, un mot de passe), ajoutez ce coffre de clés de tooa de valeur.</span><span class="sxs-lookup"><span data-stu-id="b8f25-103">If you need tooprovide a sensitive value for a parameter (such as a password), add that value tooa key vault.</span></span> <span data-ttu-id="b8f25-104">Récupérer le coffre de clés hello lors du déploiement, comme indiqué dans l’exemple précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="b8f25-104">Retrieve hello key vault during deployment as shown in hello previous example.</span></span> <span data-ttu-id="b8f25-105">Pour plus d’informations, consultez [Passage de valeurs sécurisés pendant le déploiement](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="b8f25-105">For more information, see [Pass secure values during deployment](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span> 

