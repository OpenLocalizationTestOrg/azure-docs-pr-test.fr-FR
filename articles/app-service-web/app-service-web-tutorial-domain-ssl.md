---
title: "application web de domaine personnalisé d’aaaAdd et SSL tooan Azure | Documents Microsoft"
description: "Découvrez comment tooprepare votre Azure web production de toogo application en ajoutant la marque de votre société. Mapper hello domaine personnalisé nom (domaine personnel) tooyour web app et sécurisez-le avec un certificat SSL personnalisé."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/29/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2679ed8b2dbbeba0b128c1a3ec01148f97c35342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a>Ajouter des domaines personnalisés et SSL tooan Azure web app

Ce didacticiel vous montre comment tooquickly mapper une application web Azure de domaine personnalisé nom tooyour et sécuriser avec un certificat SSL personnalisé. 

## <a name="before-you-begin"></a>Avant de commencer

Avant d’exécuter cet exemple, installez hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) localement.

Vous devez également la page de configuration d’un accès administratif toohello DNS pour votre fournisseur de leur domaine respectif. Par exemple, tooadd `www.contoso.com`, vous devez toobe tooconfigure en mesure des entrées DNS pour `contoso.com`.

Enfin, vous devez valide. Le fichier PFX _et_ son mot de passe pour le certificat SSL de hello souhaité tooupload et établir une liaison. Ce certificat SSL doit être le nom de domaine personnalisé configuré toosecure hello souhaité. Bonjour exemple ci-dessus, votre certificat SSL doit sécuriser `www.contoso.com`. 

## <a name="step-1---create-an-azure-web-app"></a>Étape 1 : Créer une application web Azure

### <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Nous sommes maintenant continu toouse hello Azure CLI 2.0 dans un fenêtre de terminal toocreate hello des ressources nécessaires toohost notre application Node.js dans Azure.  Connectez-vous à tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran. 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a>Créer un groupe de ressources   
Créer un groupe de ressources avec hello [az groupe créer](/cli/azure/group#create). Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure comme les applications web, les bases de données et les comptes de stockage sont déployées et gérées. 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

toosee quel possible les valeurs que vous pouvez utiliser pour `---location`, utilisez hello `az appservice list-locations` commande CLI d’Azure.

## <a name="create-an-app-service-plan"></a>Créer un plan App Service

Créer un plan App Service avec hello [création d’un plan de az](/cli/azure/appservice/plan#create) commande. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Hello exemple suivant crée un plan App Service nommé `myAppServicePlan` à l’aide de hello **base** niveau tarifaire.

az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1

Lorsque hello plan App Service a été créé, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant. 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a>Créer une application web

Maintenant qu’un plan App Service a été créé, créez une application web au sein de hello `myAppServicePlan` plan App Service. fournit les application Hello web vous êtes un hébergement toodeploy d’espace de votre code et fournit aussi une URL pour vous tooview hello déployé l’application. Hello d’utilisation [web du service d’applications az créer](/cli/azure/appservice/web#create) commande toocreate hello web app. 

Dans la commande de hello ci-dessous, remplacez par votre propre nom d’application unique dans lequel vous consultez hello `<app_name>` espace réservé. Ce nom unique servira en tant que partie hello hello par défaut du nom de domaine pour l’application web de hello, par conséquent, le nom de hello doit toobe unique entre toutes les applications dans Azure. Vous pouvez mapper plus tard de n’importe quelle application web du toohello personnalisée DNS entrée avant de vous exposez tooyour utilisateurs. 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

Lorsque l’application hello web a été créée, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant. 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

À partir de la sortie JSON, de hello `defaultHostName` affiche le nom de domaine par défaut de votre application web. Dans votre navigateur, accédez à toothis adresse.

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a>Étape 2 : Configurer le mappage DNS

Dans cette étape, vous ajoutez un mappage de nom de domaine tooyour de domaine personnalisé d’une application de web par défaut, `<app_name>.azurewebsites.net`. En général, vous effectuez cette étape sur le site web du fournisseur de votre domaine. Comme le site web de chaque bureau d’enregistrement des domaines est légèrement différent, vous devez consulter la documentation de votre fournisseur. Voici néanmoins quelques recommandations générales. 

### <a name="navigate-tootoodns-management-page"></a>Parcourir la page de gestion tootooDNS

Tout d’abord, ouvrez une session dans le site Web de tooyour de domaines.  

Recherchez la page de hello pour la gestion des enregistrements DNS. Recherchez des liens ou des zones du site hello étiqueté **nom de domaine**, **DNS**, ou **gestion des noms de serveur**. Souvent, vous pouvez trouver hello lien en affichant les informations de votre compte et puis recherchez un lien comme **mes domaines**.

Une fois que vous avez trouvé la page, recherchez un lien vous permettant d’ajouter ou de modifier des enregistrements DNS. Il s’agit probablement d’un lien de **fichier de zone** ou d’**enregistrements DNS**, ou encore d’un lien de **configuration avancé**.

### <a name="create-a-cname-record"></a>Créer un enregistrement CNAME

Ajoutez un enregistrement CNAME qui mappe le nom de domaine hello sous-domaine souhaitée nom tooyour l’application web par défaut (`<app_name>.azurewebsites.net`, où `<app_name>` est le nom unique de votre application).

Pourquoi `www.contoso.com` exemple, vous créez un enregistrement CNAME qui mappe hello `www` nom d’hôte trop`<app_name>.azurewebsites.net`.

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a>Étape 3 : configurer un domaine personnalisé de hello sur votre application web

Lorsque vous avez terminé la configuration d’une correspondance de nom d’hôte hello dans le site Web du fournisseur de votre domaine, vous êtes domaine personnalisé de prêt tooconfigure hello sur votre application web. Hello d’utilisation [az app service web config hostname ajouter](/cli/azure/appservice/web/config/hostname#add) commande tooadd cette configuration. 

Dans la commande hello ci-dessous, remplacez `<app_name>` avec votre nom d’application unique et < your_custom_domain > avec le nom de domaine personnalisé complet hello (par exemple, `www.contoso.com`). 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

domaine personnalisé de Hello est maintenant entièrement mappé tooyour l’application web. Dans votre navigateur, accédez à nom de domaine personnalisé toohello. Par exemple :

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a>Étape 4 : lier une application du web tooyour de certificat SSL personnalisée

Vous disposez maintenant d’une application web Azure, avec le nom de domaine hello souhaité dans la barre d’adresses du navigateur hello. Toutefois, si vous accédez toohello `https://<your_custom_domain>` maintenant, vous obtenez une erreur de certificat. 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

Cette erreur est due au fait que votre application web ne dispose pas encore d’une liaison de certificat SSL correspondant à votre nom de domaine personnalisé. Toutefois, vous n’obtenez une erreur si vous accédez trop`https://<app_name>.azurewebsites.net`. C’est parce que votre application, ainsi que toutes les applications de Service d’applications Azure, est sécurisé avec un certificat SSL pour hello hello `*.azurewebsites.net` domaine générique par défaut. 

Dans commande tooaccess votre application web par le nom de votre domaine personnalisé, vous devez certificat SSL de hello toobind pour votre application web de toohello domaine personnalisé. Vous le ferez lors de cette étape. 

### <a name="upload-hello-ssl-certificate"></a>Télécharger le certificat SSL de hello

Télécharger le certificat SSL de hello pour votre application web de tooyour domaine personnalisé à l’aide de hello [le téléchargement ssl config az app service web](/cli/azure/appservice/web/config/ssl#upload) commande.

Dans la commande hello ci-dessous, remplacez `<app_name>` avec le nom de votre application unique, `<path_to_ptx_file>` avec tooyour de chemin d’accès hello. Le fichier PFX, et `<password>` avec mot de passe de votre certificat. 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

Lorsque le certificat de hello est téléchargé, hello CLI d’Azure s’affiche des informations similaires toohello est l’exemple suivant :

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

À partir de la sortie JSON, de hello `thumbprint` affiche l’empreinte numérique de votre certificat téléchargé. Copiez sa valeur pour l’étape suivante de hello.

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a>Lier l’application web toohello hello téléchargé SSL certificat

Votre application web a maintenant le nom de domaine personnalisé hello souhaité, et il possède également un certificat SSL qui sécurise de ce domaine personnalisé. Bonjour chose uniquement les toodo gauche est l’application web toohello toobind hello certificat téléchargé. Pour cela, vous devez utiliser hello [liaison ssl de az app service web config](/cli/azure/appservice/web/config/ssl#bind) commande.

Dans la commande hello ci-dessous, remplacez `<app_name>` avec le nom de votre application unique et `<thumbprint-from-previous-output>` avec l’empreinte numérique du certificat hello que vous obtenez à partir de la commande précédente hello. 

az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI

Lorsque les certificats hello sont lié tooyour web app, hello CLI d’Azure s’affiche des informations similaires toohello est l’exemple suivant :

{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }

Dans votre navigateur, accédez à tooHTTPS de point de terminaison de votre nom de domaine personnalisé. Par exemple :

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a>Autres ressources

[Acheter et configurer un nom de domaine personnalisé dans Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[acheter et configurer un certificat SSL pour votre service Azure App Service](web-sites-purchase-ssl-web-site.md)
