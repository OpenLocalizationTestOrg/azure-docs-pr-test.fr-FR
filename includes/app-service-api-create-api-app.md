
<span data-ttu-id="fe951-101">Créer un [application API](../articles/app-service-api/app-service-api-apps-why-best-platform.md) Bonjour `myAppServicePlan` plan App Service avec hello [az webapp créer](/cli/azure/appservice/web#create) commande.</span><span class="sxs-lookup"><span data-stu-id="fe951-101">Create a [API app](../articles/app-service-api/app-service-api-apps-why-best-platform.md) in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/appservice/web#create) command.</span></span> 

<span data-ttu-id="fe951-102">Hello web application fournit un espace d’hébergement de votre API et fournit une application hello déployé de tooview URL.</span><span class="sxs-lookup"><span data-stu-id="fe951-102">hello web app provides a hosting space for your API and provides a URL tooview hello deployed app.</span></span>

<span data-ttu-id="fe951-103">Bonjour suivant de commande, remplacez  *\<nom_application >* avec un nom unique.</span><span class="sxs-lookup"><span data-stu-id="fe951-103">In hello following command, replace *\<app_name>* with a unique name.</span></span> <span data-ttu-id="fe951-104">Si `<app_name>` est n’est pas unique, vous obtenez le message d’erreur hello « Site Web nommé < nom_application > existe déjà. »</span><span class="sxs-lookup"><span data-stu-id="fe951-104">If `<app_name>` is not unique, you get hello error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="fe951-105">Hello par défaut de l’URL de l’application web hello est `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="fe951-105">hello default URL of hello web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="fe951-106">Lors de l’application hello web a été créée, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="fe951-106">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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