<span data-ttu-id="fdaac-101">Créez un plan App Service avec la commande [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="fdaac-101">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span>

[!INCLUDE [app-service-plan](app-service-plan.md)]

<span data-ttu-id="fdaac-102">L’exemple suivant crée un plan App Service nommé `myAppServicePlan` dans le niveau tarifaire **Gratuit** :</span><span class="sxs-lookup"><span data-stu-id="fdaac-102">The following example creates an App Service plan named `myAppServicePlan` in the **Free** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="fdaac-103">Lorsque le plan App Service est créé, l’interface Azure CLI affiche des informations similaires à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="fdaac-103">When the App Service plan has been created, the Azure CLI shows information similar to the following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "West Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  < JSON data removed for brevity. >
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
} 
```