
Créer un [application API](../articles/app-service-api/app-service-api-apps-why-best-platform.md) Bonjour `myAppServicePlan` plan App Service avec hello [az webapp créer](/cli/azure/appservice/web#create) commande. 

Hello web application fournit un espace d’hébergement de votre API et fournit une application hello déployé de tooview URL.

Bonjour suivant de commande, remplacez  *\<nom_application >* avec un nom unique. Si `<app_name>` est n’est pas unique, vous obtenez le message d’erreur hello « Site Web nommé < nom_application > existe déjà. » Hello par défaut de l’URL de l’application web hello est `https://<app_name>.azurewebsites.net`. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Lors de l’application hello web a été créée, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant :

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