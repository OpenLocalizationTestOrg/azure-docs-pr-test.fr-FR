
<span data-ttu-id="87cb7-101">Créez une [application API](../articles/app-service-api/app-service-api-apps-why-best-platform.md) dans le plan App Service `myAppServicePlan` avec la commande [az webapp create](/cli/azure/appservice/web#create).</span><span class="sxs-lookup"><span data-stu-id="87cb7-101">Create a [API app](../articles/app-service-api/app-service-api-apps-why-best-platform.md) in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/appservice/web#create) command.</span></span> 

<span data-ttu-id="87cb7-102">L’application web offre un espace d’hébergement pour votre API et fournit une URL pour afficher l’application déployée.</span><span class="sxs-lookup"><span data-stu-id="87cb7-102">The web app provides a hosting space for your API and provides a URL to view the deployed app.</span></span>

<span data-ttu-id="87cb7-103">Dans la commande suivante, remplacez *\<app_name>* par un nom unique.</span><span class="sxs-lookup"><span data-stu-id="87cb7-103">In the following command, replace *\<app_name>* with a unique name.</span></span> <span data-ttu-id="87cb7-104">Si `<app_name>` n’est pas une valeur unique, un message d’erreur s’affiche : « Un site web avec ce nom <app_name> existe déjà. »</span><span class="sxs-lookup"><span data-stu-id="87cb7-104">If `<app_name>` is not unique, you get the error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="87cb7-105">L’URL par défaut de l’application web est `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="87cb7-105">The default URL of the web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="87cb7-106">Une fois l’application web créée, Azure CLI affiche des informations similaires à celles de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="87cb7-106">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "<app_name>.azurewebsites.net",
    "<app_name>.scm.azurewebsites.net"
  ],
  "gatewaySiteName": null,
  "hostNameSslStates": [
    {
      "hostType": "Standard",
      "name": "<app_name>.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "virtualIp": null
    }
    < JSON data removed for brevity. >
}
```