---
title: "aaaBuild une application une évolutivité dans Azure | Documents Microsoft"
description: "Découvrez comment toouse différents services Azure toomaximize hello les performances d’une application ASP.NET dans Azure."
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a>Créer une application hyperscale dans Azure

Ce didacticiel vous montre comment les demandes tooscale à une application web ASP.NET Azure toomaximize utilisateur.

Avant de commencer ce didacticiel, assurez-vous que [hello CLI d’Azure est installée](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) sur votre ordinateur. En outre, vous devez [Visual Studio](https://www.visualstudio.com/vs/) sur votre exemple d’application hello toorun ordinateur local.

## <a name="step-1---get-sample-application"></a>Étape 1 : obtenir l’exemple d’application
Dans cette étape, vous définir un projet ASP.NET local hello.

### <a name="clone-hello-application-repository"></a>Référentiel d’application hello clone

Terminal de ligne de commande de hello ouverte de votre choix et `CD` répertoire de travail tooa. Ensuite, suivante d’exécution hello commandes tooclone hello exemple d’application. 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a>Exécutez l’exemple d’application hello dans Visual Studio

Ouvrez la solution de hello dans Visual Studio.

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

Type `F5` application hello de toorun.

Cet exemple d’application web ASP.NET provient d’un modèle par défaut de hello et persiste du cache de sortie hello sessions et utilise des utilisateurs. Examinons `HighScaleApp\Controllers\HomeController.cs`. Hello `Index()` méthode ajoute un élément de session toohello de données.

```csharp
Session.Add("visited", "true"); 
```

Et hello `About()` et `Contact()` méthodes cache leur sortie.

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a>Étape 2 : déployer tooAzure
Dans cette étape, vous créez une application web Azure et déployez votre tooit d’application exemple ASP.NET.

### <a name="create-a-resource-group"></a>Créer un groupe de ressources   
Utilisez [création de groupe de az](https://docs.microsoft.com/cli/azure/group#create) toocreate un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) dans la région Europe de l’ouest hello. Un groupe de ressources est l’endroit où vous placez tous les hello ressources Azure que vous souhaitez toomanage ensemble, telles que l’application web hello et une base de données SQL back-end.

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

toosee quel possible les valeurs que vous pouvez utiliser pour `---location`, utilisez hello [Liste emplacements az app service](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) commande.

### <a name="create-an-app-service-plan"></a>Créer un plan App Service
Utilisez [création d’un plan de az](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate une « B1 » [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

Un plan App Service est une unité d’échelle, ce qui peut inclure n’importe quel nombre d’applications que vous souhaitez tooscale les ou out ensemble over hello même infrastructure de Service d’applications. Chaque plan est également affecté à un [niveau tarifaire](https://azure.microsoft.com/en-us/pricing/details/app-service/). Les niveaux supérieurs incluent un matériel plus performant et des fonctionnalités supplémentaires telles que des instances de montée en puissance parallèle supplémentaires.

Pour ce didacticiel, B1 est niveau minimale hello qui permet de réduire les instances de toothree. Vous pouvez déplacer votre application vers le haut ou vers le bas hello tarification ultérieurement en exécutant [mise à jour de plan de service d’applications az](https://docs.microsoft.com/cli/azure/appservice/plan#update). 

### <a name="create-a-web-app"></a>Créer une application web
Utilisez [web du service d’applications az créer](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate une application web avec un nom unique dans `$appName`.

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a>Définir les informations d’identification de déploiement
Utilisez [az app service web utilisateur de déploiement défini](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset informations d’identification de votre déploiement au niveau des comptes de Service d’applications.

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a>Configuration du déploiement Git
Utilisez [contrôle de code source liée à un web de service d’applications dans az-config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure un déploiement Git local.

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

Cette commande vous donne une sortie ressemblant à hello suivantes :

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

Hello d’utilisation retourné les votre Git URL tooconfigure à distance. Hello commande suivante utilise hello précédant l’exemple de sortie.

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a>Déployer l’exemple d’application hello
Vous est désormais prêt toodeploy votre exemple d’application. Exécutez `git push`.

```powershell
git push azure master
```

À l’invite de mot de passe, utilisez un mot de passe hello que vous avez spécifié lors de l’exécution `az appservice web deployment user set`.

### <a name="browse-tooazure-web-app"></a>Parcourir l’application web tooAzure
Utilisez [Parcourir de az app service web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee votre application en cours d’exécution en direct dans Azure, exécutez la commande.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a>Étape 3 : connecter tooRedis
Dans cette étape, vous définir le Cache Redis Azure sous forme d’application web Azure de tooyour cache colocalisés externe. Vous pouvez rapidement utiliser Redis toocache votre sortie de la page. En outre, lorsque vous montez vos applications web en charge par la suite , Redis vous permet de conserver les sessions utilisateur sur plusieurs instances en toute sécurité.

### <a name="create-an-azure-redis-cache"></a>Création d'un cache Redis Azure
Utilisez [redis de az créer](https://docs.microsoft.com/en-us/cli/azure/redis#create) mettre en Cache un Redis Azure toocreate et enregistrer hello JSON de sortie. Utilisez un nom unique dans `$cacheName`.

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a>Configurer l’application de hello toouse Redis
Format hello une chaîne de connexion pour votre cache.

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

deuxième ligne de Hello doit vous donner une sortie ressemblant à ceci :

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

Dans Visual Studio, créez un fichier de configuration web racine du projet appelé `redis.config` et coller hello après le code dans celui-ci. Dans `value`, utilisez la chaîne de connexion hello hello sortie PowerShell.

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

Si vous examinez hello `.gitignore` fichier dans votre référentiel Git, vous verrez que ce fichier est exclu du contrôle de code source. Cela permet de conserver vos informations sensibles en sécurité. 

Ouvrez `Web.config`. Hello d’avis `<appSettings file="redis.config">` élément, qui obtient le paramètre hello vous avez créé dans `redis.config`. 

Trouver hello commenté section inclut `<sessionState>` et `<caching>`. Supprimez les commentaires de cette section.

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

Ce code recherche de chaîne de connexion Redis hello défini dans `RedisConnection`. 

Votre application utilise Redis toomanage sessions et mise en cache. Type `F5` application hello de toorun. Si vous le souhaitez, vous pouvez télécharger une Redis gestion toovisualize hello les données client sont désormais enregistrées toohello cache.

### <a name="configure-hello-connection-string-in-azure"></a>Configurer la chaîne de connexion hello dans Azure

Pour toowork de votre application dans Azure, vous devez tooconfigure hello même chaîne de connexion Redis dans votre application web Azure. Étant donné que `redis.config` n’est pas conservé dans le contrôle de code source, il n’est pas déployée tooAzure lorsque vous exécutez le déploiement Git.

Utilisez [az app service web configuration appsettings mettre à jour](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd hello de chaîne de connexion avec hello même nom (`RedisConnection`).

az appservice web config appsettings update--paramètres « RedisConnection = $connstring »--nom $appName--groupe de ressources myResourceGroup

N’oubliez pas que `$connstring` contient la chaîne de connexion hello mis en forme.

### <a name="redeploy-hello-application-tooazure"></a>Redéployer hello application tooAzure
Utiliser Git commandes toopush votre tooAzure de modifications

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

À l’invite de mot de passe, utilisez un mot de passe hello que vous avez spécifié lors de l’exécution `az appservice web deployment user set`.

### <a name="browse-toohello-azure-web-app"></a>Parcourir toohello Azure web app
Utilisez [Parcourir de az app service web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello les résultats dans Azure.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a>Étape 4 - instances toomultiple de mise à l’échelle
Hello plan App Service est l’unité d’échelle hello pour vos applications web Azure. tooscale à votre application web, vous mettez à l’échelle hello plan App Service.

Utilisez [mise à jour de plan de service d’applications az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale des instances de toothree du plan de Service d’applications de hello, qui est hello nombre maximal autorisé par hello B1 niveau tarifaire. N’oubliez pas que B1 est hello tarification que vous avez choisi lors de la création de hello précédemment le plan App Service. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a>Étape 5 : mise à échelle géographique
Lors de la mise à l’échelle géographiquement, vous exécutez votre application dans plusieurs régions de hello cloud Azure. Ce programme d’installation équilibre la charge de votre application plus basée sur la géographie et réduit le temps de réponse hello en plaçant des navigateurs tooclient plus proche de votre application.

Dans cette étape, vous mettez à l’échelle votre ASP.NET web application tooa deuxième région avec [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/). Vous devez à fin hello d’étape de hello, une application web en cours d’exécution en Europe de l’Ouest (déjà créés) et une application web en cours d’exécution en Asie du Sud-est (pas encore créé). Les deux applications seront traitées par hello même URL du Gestionnaire de trafic.

### <a name="scale-up-hello-europe-app-toostandard-tier"></a>Montée en puissance hello couche de tooStandard Europe de l’application
Dans le Service d’application, l’intégration avec Azure Traffic Manager nécessite la tarification Standard hello. Utilisez [mise à jour de plan de service d’applications az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale de votre tooS1 de plan de Service d’applications. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a>Créer un profil Traffic Manager 
Utilisez [az réseau-du profil traffic manager créer](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate Gestionnaire de trafic de profil et d’ajouter le groupe de ressources tooyour. Utilisez un nom DNS unique dans $dnsName.

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> `--routing-method Performance`Spécifie que ce profil [achemine le point de terminaison le plus proche de la toohello d’utilisateur trafic](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="get-hello-resource-id-of-hello-europe-app"></a>Obtenir l’ID de ressources hello de hello Europe de l’application
Utilisez [afficher de az app service web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget ID de ressource hello de votre application web.

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a>Ajouter un point de terminaison Traffic Manager pour hello Europe de l’application
Utilisez [créer de point de terminaison Gestionnaire de trafic de réseau az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd un tooyour de point de terminaison du profil Traffic Manager et l’ID de ressource hello utilisation de votre application web en tant que cible de hello.

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a>Obtenir l’URL de point de terminaison de Traffic Manager hello
Cette application web existante de points tooyour, votre profil Traffic Manager a maintenant un point de terminaison. Utilisez [az réseau Gestionnaire de trafic profil afficher](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget son URL. 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

Copier la sortie de hello dans votre navigateur. Vous devriez voir votre application web à nouveau.

### <a name="create-an-azure-redis-cache-in-asia"></a>Créer un cache Redis Azure en Asie
Maintenant, vous répliquez la région d’Asie du Sud-est toohello de votre application web Azure. toostart, utilisez [redis de az créer](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate un deuxième Cache Redis Azure Asie du Sud-est. Ce cache doit toobe colocalisé avec votre application en Asie.

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

`--name $cacheName-asia`donne hello nom hello de cache de hello cache d’Europe de l’ouest, avec hello `-asia` suffixe.

### <a name="create-an-app-service-plan-in-asia"></a>Créer un plan App Service en Asie
Utilisez [création d’un plan de az](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate une deuxième application de Service de planification dans la région Asie du Sud-est hello, à l’aide de hello S1 même niveau en tant que plan d’Europe de l’ouest hello.

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a>Créer une application web en Asie
Utilisez [web du service d’applications az créer](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate deuxième application web.

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

`--name $appName-asia`donne hello nom de l’application hello d’application d’Europe de l’ouest hello, avec hello `-asia` suffixe.

### <a name="configure-hello-connection-string-for-redis"></a>Configurer la chaîne de connexion hello pour Redis
Utilisez [az app service web configuration appsettings mettre à jour](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web application hello chaîne de connexion pour hello cache d’Asie du Sud-est.

az appservice web config appsettings update --paramètres « RedisConnection = $($redis.hostname) : $($redis.sslPort), mot de passe = $($redis.accessKeys.primaryKey), ssl = vrai, abortConnect = faux » --nom $appName-asia --groupe de ressources myResourceGroup

### <a name="configure-git-deployment-for-hello-asia-app"></a>Configurer le déploiement Git pour hello Asie de l’application.
Utilisez [contrôle de code source liée à un web de service d’applications dans az-config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure le déploiement Git local pour l’application web de la deuxième hello.

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

Cette commande vous donne une sortie ressemblant à hello suivantes :

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

Hello d’utilisation retourné un deuxième Git URL tooconfigure à distance pour votre référentiel local. Hello commande suivante utilise hello précédant l’exemple de sortie.

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a>Déployer votre exemple d’application
Exécutez `git push` toodeploy votre Git de deuxième exemple application toohello distant. 

```bash
git push azure-asia master
```

À l’invite de mot de passe, utilisez un mot de passe hello que vous avez spécifié lors de l’exécution `az appservice web deployment user set`.

### <a name="browse-toohello-asia-app"></a>Parcourir toohello Asie de l’application
Utilisez [Parcourir de az app service web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify votre application est en cours d’exécution en direct dans Azure.

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a>Obtenir l’ID de ressources hello de hello Asie de l’application
Utilisez [afficher de az app service web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget ID de ressource hello de votre application web, Asie du Sud-est.

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a>Ajouter un point de terminaison Traffic Manager pour hello Asie de l’application
Utilisez [créer de point de terminaison Gestionnaire de trafic de réseau az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd une deuxième toohello de point de terminaison du profil Traffic Manager.

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a>Ajouter des applications de tooweb identificateur de région
Utilisez [az app service web configuration appsettings mettre à jour](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd une variable d’environnement spécifiques à la région.

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

Votre code d’application utilise déjà ce paramètre d’application. Examinons `HighScaleApp\Views\Home\Index.cshtml`.

### <a name="complete"></a>Terminé !

À présent, essayez d’URL de hello tooaccess de votre profil Traffic Manager à partir de navigateurs dans différentes régions géographiques. Les navigateurs clients d’Europe doivent afficher « ASP.NET Europe de l’Ouest », et les navigateurs clients d’Asie doit afficher « ASP.NET Asie du Sud-Est. »

## <a name="more-resources"></a>Autres ressources
