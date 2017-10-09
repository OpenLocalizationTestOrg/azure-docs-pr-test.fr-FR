<span data-ttu-id="9c9dd-101">Créer un [application web](../articles/app-service-web/app-service-web-overview.md) Bonjour `myAppServicePlan` plan App Service avec hello [az webapp créer](/cli/azure/webapp#create) commande.</span><span class="sxs-lookup"><span data-stu-id="9c9dd-101">Create a [web app](../articles/app-service-web/app-service-web-overview.md) in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="9c9dd-102">Hello web application fournit un espace d’hébergement pour votre code et fournit une application hello déployé de tooview URL.</span><span class="sxs-lookup"><span data-stu-id="9c9dd-102">hello web app provides a hosting space for your code and provides a URL tooview hello deployed app.</span></span>

<span data-ttu-id="9c9dd-103">Bonjour suivant de commande, remplacez  *\<nom_application >* avec un nom unique (les caractères valides sont `a-z`, `0-9`, et `-`).</span><span class="sxs-lookup"><span data-stu-id="9c9dd-103">In hello following command, replace *\<app_name>* with a unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="9c9dd-104">Si `<app_name>` est n’est pas unique, vous obtenez le message d’erreur hello « Site Web nommé < nom_application > existe déjà. »</span><span class="sxs-lookup"><span data-stu-id="9c9dd-104">If `<app_name>` is not unique, you get hello error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="9c9dd-105">Hello par défaut de l’URL de l’application web hello est `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="9c9dd-105">hello default URL of hello web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="9c9dd-106">Lors de l’application hello web a été créée, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9c9dd-106">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="9c9dd-107">Accédez à toohello site toosee votre application web qui vient d’être créé.</span><span class="sxs-lookup"><span data-stu-id="9c9dd-107">Browse toohello site toosee your newly created web app.</span></span>

```bash
http://<app_name>.azurewebsites.net
```
