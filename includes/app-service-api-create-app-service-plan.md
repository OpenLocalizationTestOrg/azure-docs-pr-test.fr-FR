Créer un plan App Service avec hello [création d’un plan de az](/cli/azure/appservice/plan#create) commande.

[!INCLUDE [app-service-plan](app-service-plan.md)]

Hello exemple suivant crée un plan App Service nommé `myAppServicePlan` Bonjour **libre** niveau tarifaire :

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Lorsque hello plan App Service a été créé, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :

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