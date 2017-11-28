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
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="71849-103">Créer une application hyperscale dans Azure</span><span class="sxs-lookup"><span data-stu-id="71849-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="71849-104">Ce didacticiel vous montre comment les demandes tooscale à une application web ASP.NET Azure toomaximize utilisateur.</span><span class="sxs-lookup"><span data-stu-id="71849-104">This tutorial shows you how tooscale out an ASP.NET web app in Azure toomaximize user requests.</span></span>

<span data-ttu-id="71849-105">Avant de commencer ce didacticiel, assurez-vous que [hello CLI d’Azure est installée](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="71849-105">Before starting this tutorial, ensure that [hello Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="71849-106">En outre, vous devez [Visual Studio](https://www.visualstudio.com/vs/) sur votre exemple d’application hello toorun ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="71849-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine toorun hello sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="71849-107">Étape 1 : obtenir l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="71849-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="71849-108">Dans cette étape, vous définir un projet ASP.NET local hello.</span><span class="sxs-lookup"><span data-stu-id="71849-108">In this step, you set up hello local ASP.NET project.</span></span>

### <a name="clone-hello-application-repository"></a><span data-ttu-id="71849-109">Référentiel d’application hello clone</span><span class="sxs-lookup"><span data-stu-id="71849-109">Clone hello application repository</span></span>

<span data-ttu-id="71849-110">Terminal de ligne de commande de hello ouverte de votre choix et `CD` répertoire de travail tooa.</span><span class="sxs-lookup"><span data-stu-id="71849-110">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span> <span data-ttu-id="71849-111">Ensuite, suivante d’exécution hello commandes tooclone hello exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="71849-111">Then, run hello following commands tooclone hello sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a><span data-ttu-id="71849-112">Exécutez l’exemple d’application hello dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="71849-112">Run hello sample application in Visual Studio</span></span>

<span data-ttu-id="71849-113">Ouvrez la solution de hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71849-113">Open hello solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="71849-114">Type `F5` application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="71849-114">Type `F5` toorun hello application.</span></span>

<span data-ttu-id="71849-115">Cet exemple d’application web ASP.NET provient d’un modèle par défaut de hello et persiste du cache de sortie hello sessions et utilise des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="71849-115">This sample ASP.NET web application comes from hello default template, and persists user sessions and uses hello output cache.</span></span> <span data-ttu-id="71849-116">Examinons `HighScaleApp\Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="71849-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="71849-117">Hello `Index()` méthode ajoute un élément de session toohello de données.</span><span class="sxs-lookup"><span data-stu-id="71849-117">hello `Index()` method adds a piece of data toohello session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="71849-118">Et hello `About()` et `Contact()` méthodes cache leur sortie.</span><span class="sxs-lookup"><span data-stu-id="71849-118">And hello `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a><span data-ttu-id="71849-119">Étape 2 : déployer tooAzure</span><span class="sxs-lookup"><span data-stu-id="71849-119">Step 2 - Deploy tooAzure</span></span>
<span data-ttu-id="71849-120">Dans cette étape, vous créez une application web Azure et déployez votre tooit d’application exemple ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="71849-120">In this step, you create an Azure web app and deploy your sample ASP.NET application tooit.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="71849-121">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="71849-121">Create a resource group</span></span>   
<span data-ttu-id="71849-122">Utilisez [création de groupe de az](https://docs.microsoft.com/cli/azure/group#create) toocreate un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) dans la région Europe de l’ouest hello.</span><span class="sxs-lookup"><span data-stu-id="71849-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) toocreate a [resource group](../azure-resource-manager/resource-group-overview.md) in hello West Europe region.</span></span> <span data-ttu-id="71849-123">Un groupe de ressources est l’endroit où vous placez tous les hello ressources Azure que vous souhaitez toomanage ensemble, telles que l’application web hello et une base de données SQL back-end.</span><span class="sxs-lookup"><span data-stu-id="71849-123">A resource group is where you put all hello Azure resources that you want toomanage together, such as hello web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="71849-124">toosee quel possible les valeurs que vous pouvez utiliser pour `---location`, utilisez hello [Liste emplacements az app service](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) commande.</span><span class="sxs-lookup"><span data-stu-id="71849-124">toosee what possible values you can use for `---location`, use hello [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="71849-125">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="71849-125">Create an App Service plan</span></span>
<span data-ttu-id="71849-126">Utilisez [création d’un plan de az](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate une « B1 » [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="71849-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="71849-127">Un plan App Service est une unité d’échelle, ce qui peut inclure n’importe quel nombre d’applications que vous souhaitez tooscale les ou out ensemble over hello même infrastructure de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="71849-127">An App Service plan is a scale unit, which can include any number of apps that you want tooscale up or out together over hello same App Service infrastructure.</span></span> <span data-ttu-id="71849-128">Chaque plan est également affecté à un [niveau tarifaire](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="71849-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="71849-129">Les niveaux supérieurs incluent un matériel plus performant et des fonctionnalités supplémentaires telles que des instances de montée en puissance parallèle supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="71849-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="71849-130">Pour ce didacticiel, B1 est niveau minimale hello qui permet de réduire les instances de toothree.</span><span class="sxs-lookup"><span data-stu-id="71849-130">For this tutorial, B1 is hello minimum tier that enables scale out toothree instances.</span></span> <span data-ttu-id="71849-131">Vous pouvez déplacer votre application vers le haut ou vers le bas hello tarification ultérieurement en exécutant [mise à jour de plan de service d’applications az](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="71849-131">You can always move your app up or down hello pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="71849-132">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="71849-132">Create a web app</span></span>
<span data-ttu-id="71849-133">Utilisez [web du service d’applications az créer](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate une application web avec un nom unique dans `$appName`.</span><span class="sxs-lookup"><span data-stu-id="71849-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="71849-134">Définir les informations d’identification de déploiement</span><span class="sxs-lookup"><span data-stu-id="71849-134">Set deployment credentials</span></span>
<span data-ttu-id="71849-135">Utilisez [az app service web utilisateur de déploiement défini](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset informations d’identification de votre déploiement au niveau des comptes de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="71849-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="71849-136">Configuration du déploiement Git</span><span class="sxs-lookup"><span data-stu-id="71849-136">Configure Git deployment</span></span>
<span data-ttu-id="71849-137">Utilisez [contrôle de code source liée à un web de service d’applications dans az-config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure un déploiement Git local.</span><span class="sxs-lookup"><span data-stu-id="71849-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="71849-138">Cette commande vous donne une sortie ressemblant à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="71849-138">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="71849-139">Hello d’utilisation retourné les votre Git URL tooconfigure à distance.</span><span class="sxs-lookup"><span data-stu-id="71849-139">Use hello returned URL tooconfigure your Git remote.</span></span> <span data-ttu-id="71849-140">Hello commande suivante utilise hello précédant l’exemple de sortie.</span><span class="sxs-lookup"><span data-stu-id="71849-140">hello following command uses hello preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a><span data-ttu-id="71849-141">Déployer l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="71849-141">Deploy hello sample application</span></span>
<span data-ttu-id="71849-142">Vous est désormais prêt toodeploy votre exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="71849-142">You are now ready toodeploy your sample application.</span></span> <span data-ttu-id="71849-143">Exécutez `git push`.</span><span class="sxs-lookup"><span data-stu-id="71849-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="71849-144">À l’invite de mot de passe, utilisez un mot de passe hello que vous avez spécifié lors de l’exécution `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="71849-144">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-tooazure-web-app"></a><span data-ttu-id="71849-145">Parcourir l’application web tooAzure</span><span class="sxs-lookup"><span data-stu-id="71849-145">Browse tooAzure web app</span></span>
<span data-ttu-id="71849-146">Utilisez [Parcourir de az app service web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee votre application en cours d’exécution en direct dans Azure, exécutez la commande.</span><span class="sxs-lookup"><span data-stu-id="71849-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a><span data-ttu-id="71849-147">Étape 3 : connecter tooRedis</span><span class="sxs-lookup"><span data-stu-id="71849-147">Step 3 - Connect tooRedis</span></span>
<span data-ttu-id="71849-148">Dans cette étape, vous définir le Cache Redis Azure sous forme d’application web Azure de tooyour cache colocalisés externe.</span><span class="sxs-lookup"><span data-stu-id="71849-148">In this step, you set up Azure Redis Cache as an external, colocated cache tooyour Azure web app.</span></span> <span data-ttu-id="71849-149">Vous pouvez rapidement utiliser Redis toocache votre sortie de la page.</span><span class="sxs-lookup"><span data-stu-id="71849-149">You can quickly utilize Redis toocache your page output.</span></span> <span data-ttu-id="71849-150">En outre, lorsque vous montez vos applications web en charge par la suite , Redis vous permet de conserver les sessions utilisateur sur plusieurs instances en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="71849-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="71849-151">Création d'un cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="71849-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="71849-152">Utilisez [redis de az créer](https://docs.microsoft.com/en-us/cli/azure/redis#create) mettre en Cache un Redis Azure toocreate et enregistrer hello JSON de sortie.</span><span class="sxs-lookup"><span data-stu-id="71849-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate an Azure Redis Cache and save hello JSON output.</span></span> <span data-ttu-id="71849-153">Utilisez un nom unique dans `$cacheName`.</span><span class="sxs-lookup"><span data-stu-id="71849-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a><span data-ttu-id="71849-154">Configurer l’application de hello toouse Redis</span><span class="sxs-lookup"><span data-stu-id="71849-154">Configure hello application toouse Redis</span></span>
<span data-ttu-id="71849-155">Format hello une chaîne de connexion pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="71849-155">Format hello connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="71849-156">deuxième ligne de Hello doit vous donner une sortie ressemblant à ceci :</span><span class="sxs-lookup"><span data-stu-id="71849-156">hello second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="71849-157">Dans Visual Studio, créez un fichier de configuration web racine du projet appelé `redis.config` et coller hello après le code dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="71849-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste hello following code into it.</span></span> <span data-ttu-id="71849-158">Dans `value`, utilisez la chaîne de connexion hello hello sortie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="71849-158">In `value`, use hello connection string from hello PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="71849-159">Si vous examinez hello `.gitignore` fichier dans votre référentiel Git, vous verrez que ce fichier est exclu du contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="71849-159">If you look at hello `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="71849-160">Cela permet de conserver vos informations sensibles en sécurité.</span><span class="sxs-lookup"><span data-stu-id="71849-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="71849-161">Ouvrez `Web.config`.</span><span class="sxs-lookup"><span data-stu-id="71849-161">Open `Web.config`.</span></span> <span data-ttu-id="71849-162">Hello d’avis `<appSettings file="redis.config">` élément, qui obtient le paramètre hello vous avez créé dans `redis.config`.</span><span class="sxs-lookup"><span data-stu-id="71849-162">Notice hello `<appSettings file="redis.config">` element, which gets hello setting you created in `redis.config`.</span></span> 

<span data-ttu-id="71849-163">Trouver hello commenté section inclut `<sessionState>` et `<caching>`.</span><span class="sxs-lookup"><span data-stu-id="71849-163">Find hello commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="71849-164">Supprimez les commentaires de cette section.</span><span class="sxs-lookup"><span data-stu-id="71849-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="71849-165">Ce code recherche de chaîne de connexion Redis hello défini dans `RedisConnection`.</span><span class="sxs-lookup"><span data-stu-id="71849-165">This code looks for hello Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="71849-166">Votre application utilise Redis toomanage sessions et mise en cache.</span><span class="sxs-lookup"><span data-stu-id="71849-166">Your application now uses Redis toomanage sessions and caching.</span></span> <span data-ttu-id="71849-167">Type `F5` application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="71849-167">Type `F5` toorun hello application.</span></span> <span data-ttu-id="71849-168">Si vous le souhaitez, vous pouvez télécharger une Redis gestion toovisualize hello les données client sont désormais enregistrées toohello cache.</span><span class="sxs-lookup"><span data-stu-id="71849-168">If you like, you can download a Redis management client toovisualize hello data that is now saved toohello cache.</span></span>

### <a name="configure-hello-connection-string-in-azure"></a><span data-ttu-id="71849-169">Configurer la chaîne de connexion hello dans Azure</span><span class="sxs-lookup"><span data-stu-id="71849-169">Configure hello connection string in Azure</span></span>

<span data-ttu-id="71849-170">Pour toowork de votre application dans Azure, vous devez tooconfigure hello même chaîne de connexion Redis dans votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="71849-170">For your application toowork in Azure, you need tooconfigure hello same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="71849-171">Étant donné que `redis.config` n’est pas conservé dans le contrôle de code source, il n’est pas déployée tooAzure lorsque vous exécutez le déploiement Git.</span><span class="sxs-lookup"><span data-stu-id="71849-171">Since `redis.config` is not maintained in source control, it is not deployed tooAzure when you run Git deployment.</span></span>

<span data-ttu-id="71849-172">Utilisez [az app service web configuration appsettings mettre à jour](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd hello de chaîne de connexion avec hello même nom (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="71849-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd hello connection string with hello same name (`RedisConnection`).</span></span>

<span data-ttu-id="71849-173">az appservice web config appsettings update--paramètres « RedisConnection = $connstring »--nom $appName--groupe de ressources myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="71849-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="71849-174">N’oubliez pas que `$connstring` contient la chaîne de connexion hello mis en forme.</span><span class="sxs-lookup"><span data-stu-id="71849-174">Remember that `$connstring` contains hello formatted connection string.</span></span>

### <a name="redeploy-hello-application-tooazure"></a><span data-ttu-id="71849-175">Redéployer hello application tooAzure</span><span class="sxs-lookup"><span data-stu-id="71849-175">Redeploy hello application tooAzure</span></span>
<span data-ttu-id="71849-176">Utiliser Git commandes toopush votre tooAzure de modifications</span><span class="sxs-lookup"><span data-stu-id="71849-176">Use Git commands toopush your changes tooAzure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="71849-177">À l’invite de mot de passe, utilisez un mot de passe hello que vous avez spécifié lors de l’exécution `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="71849-177">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="71849-178">Parcourir toohello Azure web app</span><span class="sxs-lookup"><span data-stu-id="71849-178">Browse toohello Azure web app</span></span>
<span data-ttu-id="71849-179">Utilisez [Parcourir de az app service web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello les résultats dans Azure.</span><span class="sxs-lookup"><span data-stu-id="71849-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a><span data-ttu-id="71849-180">Étape 4 - instances toomultiple de mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="71849-180">Step 4 - Scale toomultiple instances</span></span>
<span data-ttu-id="71849-181">Hello plan App Service est l’unité d’échelle hello pour vos applications web Azure.</span><span class="sxs-lookup"><span data-stu-id="71849-181">hello App Service plan is hello scale unit for your Azure web apps.</span></span> <span data-ttu-id="71849-182">tooscale à votre application web, vous mettez à l’échelle hello plan App Service.</span><span class="sxs-lookup"><span data-stu-id="71849-182">tooscale out your web app, you scale hello App Service plan.</span></span>

<span data-ttu-id="71849-183">Utilisez [mise à jour de plan de service d’applications az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale des instances de toothree du plan de Service d’applications de hello, qui est hello nombre maximal autorisé par hello B1 niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="71849-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale out hello App Service plan toothree instances, which is hello maximum number allowed by hello B1 pricing tier.</span></span> <span data-ttu-id="71849-184">N’oubliez pas que B1 est hello tarification que vous avez choisi lors de la création de hello précédemment le plan App Service.</span><span class="sxs-lookup"><span data-stu-id="71849-184">Remember that B1 is hello pricing tier that you chose when you created hello App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="71849-185">Étape 5 : mise à échelle géographique</span><span class="sxs-lookup"><span data-stu-id="71849-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="71849-186">Lors de la mise à l’échelle géographiquement, vous exécutez votre application dans plusieurs régions de hello cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="71849-186">When scaling geographically, you run your app in multiple regions of hello Azure cloud.</span></span> <span data-ttu-id="71849-187">Ce programme d’installation équilibre la charge de votre application plus basée sur la géographie et réduit le temps de réponse hello en plaçant des navigateurs tooclient plus proche de votre application.</span><span class="sxs-lookup"><span data-stu-id="71849-187">This setup load-balances your app further based on geography and lowers hello response time by placing your app closer tooclient browsers.</span></span>

<span data-ttu-id="71849-188">Dans cette étape, vous mettez à l’échelle votre ASP.NET web application tooa deuxième région avec [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="71849-188">In this step, you scale your ASP.NET web app tooa second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="71849-189">Vous devez à fin hello d’étape de hello, une application web en cours d’exécution en Europe de l’Ouest (déjà créés) et une application web en cours d’exécution en Asie du Sud-est (pas encore créé).</span><span class="sxs-lookup"><span data-stu-id="71849-189">At hello end of hello step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="71849-190">Les deux applications seront traitées par hello même URL du Gestionnaire de trafic.</span><span class="sxs-lookup"><span data-stu-id="71849-190">Both apps will be served from hello same Traffic Manager URL.</span></span>

### <a name="scale-up-hello-europe-app-toostandard-tier"></a><span data-ttu-id="71849-191">Montée en puissance hello couche de tooStandard Europe de l’application</span><span class="sxs-lookup"><span data-stu-id="71849-191">Scale up hello Europe app tooStandard tier</span></span>
<span data-ttu-id="71849-192">Dans le Service d’application, l’intégration avec Azure Traffic Manager nécessite la tarification Standard hello.</span><span class="sxs-lookup"><span data-stu-id="71849-192">In App Service, integration with Azure Traffic Manager requires hello Standard pricing tier.</span></span> <span data-ttu-id="71849-193">Utilisez [mise à jour de plan de service d’applications az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale de votre tooS1 de plan de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="71849-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale up your App Service plan tooS1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="71849-194">Créer un profil Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="71849-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="71849-195">Utilisez [az réseau-du profil traffic manager créer](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate Gestionnaire de trafic de profil et d’ajouter le groupe de ressources tooyour.</span><span class="sxs-lookup"><span data-stu-id="71849-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate a Traffic Manager profile and add it tooyour resource group.</span></span> <span data-ttu-id="71849-196">Utilisez un nom DNS unique dans $dnsName.</span><span class="sxs-lookup"><span data-stu-id="71849-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="71849-197">`--routing-method Performance`Spécifie que ce profil [achemine le point de terminaison le plus proche de la toohello d’utilisateur trafic](../traffic-manager/traffic-manager-routing-methods.md).</span><span class="sxs-lookup"><span data-stu-id="71849-197">`--routing-method Performance` specifies that this profile [routes user traffic toohello closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-hello-resource-id-of-hello-europe-app"></a><span data-ttu-id="71849-198">Obtenir l’ID de ressources hello de hello Europe de l’application</span><span class="sxs-lookup"><span data-stu-id="71849-198">Get hello resource ID of hello Europe app</span></span>
<span data-ttu-id="71849-199">Utilisez [afficher de az app service web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget ID de ressource hello de votre application web.</span><span class="sxs-lookup"><span data-stu-id="71849-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a><span data-ttu-id="71849-200">Ajouter un point de terminaison Traffic Manager pour hello Europe de l’application</span><span class="sxs-lookup"><span data-stu-id="71849-200">Add a Traffic Manager endpoint for hello Europe app</span></span>
<span data-ttu-id="71849-201">Utilisez [créer de point de terminaison Gestionnaire de trafic de réseau az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd un tooyour de point de terminaison du profil Traffic Manager et l’ID de ressource hello utilisation de votre application web en tant que cible de hello.</span><span class="sxs-lookup"><span data-stu-id="71849-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd an endpoint tooyour Traffic Manager profile and use hello resource ID of your web app as hello target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a><span data-ttu-id="71849-202">Obtenir l’URL de point de terminaison de Traffic Manager hello</span><span class="sxs-lookup"><span data-stu-id="71849-202">Get hello Traffic Manager endpoint URL</span></span>
<span data-ttu-id="71849-203">Cette application web existante de points tooyour, votre profil Traffic Manager a maintenant un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="71849-203">Your Traffic Manager profile now has an endpoint that points tooyour existing web app.</span></span> <span data-ttu-id="71849-204">Utilisez [az réseau Gestionnaire de trafic profil afficher](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget son URL.</span><span class="sxs-lookup"><span data-stu-id="71849-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="71849-205">Copier la sortie de hello dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="71849-205">Copy hello output into your browser.</span></span> <span data-ttu-id="71849-206">Vous devriez voir votre application web à nouveau.</span><span class="sxs-lookup"><span data-stu-id="71849-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="71849-207">Créer un cache Redis Azure en Asie</span><span class="sxs-lookup"><span data-stu-id="71849-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="71849-208">Maintenant, vous répliquez la région d’Asie du Sud-est toohello de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="71849-208">Now, you replicate your Azure web app toohello Southeast Asia region.</span></span> <span data-ttu-id="71849-209">toostart, utilisez [redis de az créer](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate un deuxième Cache Redis Azure Asie du Sud-est.</span><span class="sxs-lookup"><span data-stu-id="71849-209">toostart, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="71849-210">Ce cache doit toobe colocalisé avec votre application en Asie.</span><span class="sxs-lookup"><span data-stu-id="71849-210">This cache needs toobe colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="71849-211">`--name $cacheName-asia`donne hello nom hello de cache de hello cache d’Europe de l’ouest, avec hello `-asia` suffixe.</span><span class="sxs-lookup"><span data-stu-id="71849-211">`--name $cacheName-asia` gives hello cache hello name of hello West Europe cache, with hello `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="71849-212">Créer un plan App Service en Asie</span><span class="sxs-lookup"><span data-stu-id="71849-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="71849-213">Utilisez [création d’un plan de az](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate une deuxième application de Service de planification dans la région Asie du Sud-est hello, à l’aide de hello S1 même niveau en tant que plan d’Europe de l’ouest hello.</span><span class="sxs-lookup"><span data-stu-id="71849-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate a second App Service plan in hello Southeast Asia region, using hello same S1 tier as hello West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="71849-214">Créer une application web en Asie</span><span class="sxs-lookup"><span data-stu-id="71849-214">Create a web app in Asia</span></span>
<span data-ttu-id="71849-215">Utilisez [web du service d’applications az créer](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate deuxième application web.</span><span class="sxs-lookup"><span data-stu-id="71849-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="71849-216">`--name $appName-asia`donne hello nom de l’application hello d’application d’Europe de l’ouest hello, avec hello `-asia` suffixe.</span><span class="sxs-lookup"><span data-stu-id="71849-216">`--name $appName-asia` gives hello app hello name of hello West Europe app, with hello `-asia` suffix.</span></span>

### <a name="configure-hello-connection-string-for-redis"></a><span data-ttu-id="71849-217">Configurer la chaîne de connexion hello pour Redis</span><span class="sxs-lookup"><span data-stu-id="71849-217">Configure hello connection string for Redis</span></span>
<span data-ttu-id="71849-218">Utilisez [az app service web configuration appsettings mettre à jour](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web application hello chaîne de connexion pour hello cache d’Asie du Sud-est.</span><span class="sxs-lookup"><span data-stu-id="71849-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web app hello connection string for hello Southeast Asia cache.</span></span>

<span data-ttu-id="71849-219">az appservice web config appsettings update --paramètres « RedisConnection = $($redis.hostname) : $($redis.sslPort), mot de passe = $($redis.accessKeys.primaryKey), ssl = vrai, abortConnect = faux » --nom $appName-asia --groupe de ressources myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="71849-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-hello-asia-app"></a><span data-ttu-id="71849-220">Configurer le déploiement Git pour hello Asie de l’application.</span><span class="sxs-lookup"><span data-stu-id="71849-220">Configure Git deployment for hello Asia app.</span></span>
<span data-ttu-id="71849-221">Utilisez [contrôle de code source liée à un web de service d’applications dans az-config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure le déploiement Git local pour l’application web de la deuxième hello.</span><span class="sxs-lookup"><span data-stu-id="71849-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment for hello second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="71849-222">Cette commande vous donne une sortie ressemblant à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="71849-222">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="71849-223">Hello d’utilisation retourné un deuxième Git URL tooconfigure à distance pour votre référentiel local.</span><span class="sxs-lookup"><span data-stu-id="71849-223">Use hello returned URL tooconfigure a second Git remote for your local repository.</span></span> <span data-ttu-id="71849-224">Hello commande suivante utilise hello précédant l’exemple de sortie.</span><span class="sxs-lookup"><span data-stu-id="71849-224">hello following command uses hello preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="71849-225">Déployer votre exemple d’application</span><span class="sxs-lookup"><span data-stu-id="71849-225">Deploy your sample application</span></span>
<span data-ttu-id="71849-226">Exécutez `git push` toodeploy votre Git de deuxième exemple application toohello distant.</span><span class="sxs-lookup"><span data-stu-id="71849-226">Run `git push` toodeploy your sample application toohello second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="71849-227">À l’invite de mot de passe, utilisez un mot de passe hello que vous avez spécifié lors de l’exécution `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="71849-227">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-asia-app"></a><span data-ttu-id="71849-228">Parcourir toohello Asie de l’application</span><span class="sxs-lookup"><span data-stu-id="71849-228">Browse toohello Asia app</span></span>
<span data-ttu-id="71849-229">Utilisez [Parcourir de az app service web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify votre application est en cours d’exécution en direct dans Azure.</span><span class="sxs-lookup"><span data-stu-id="71849-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a><span data-ttu-id="71849-230">Obtenir l’ID de ressources hello de hello Asie de l’application</span><span class="sxs-lookup"><span data-stu-id="71849-230">Get hello resource ID of hello Asia app</span></span>
<span data-ttu-id="71849-231">Utilisez [afficher de az app service web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget ID de ressource hello de votre application web, Asie du Sud-est.</span><span class="sxs-lookup"><span data-stu-id="71849-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a><span data-ttu-id="71849-232">Ajouter un point de terminaison Traffic Manager pour hello Asie de l’application</span><span class="sxs-lookup"><span data-stu-id="71849-232">Add a Traffic Manager endpoint for hello Asia app</span></span>
<span data-ttu-id="71849-233">Utilisez [créer de point de terminaison Gestionnaire de trafic de réseau az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd une deuxième toohello de point de terminaison du profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="71849-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd a second endpoint toohello Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a><span data-ttu-id="71849-234">Ajouter des applications de tooweb identificateur de région</span><span class="sxs-lookup"><span data-stu-id="71849-234">Add region identifier tooweb apps</span></span>
<span data-ttu-id="71849-235">Utilisez [az app service web configuration appsettings mettre à jour](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd une variable d’environnement spécifiques à la région.</span><span class="sxs-lookup"><span data-stu-id="71849-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="71849-236">Votre code d’application utilise déjà ce paramètre d’application.</span><span class="sxs-lookup"><span data-stu-id="71849-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="71849-237">Examinons `HighScaleApp\Views\Home\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="71849-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="71849-238">Terminé !</span><span class="sxs-lookup"><span data-stu-id="71849-238">Complete!</span></span>

<span data-ttu-id="71849-239">À présent, essayez d’URL de hello tooaccess de votre profil Traffic Manager à partir de navigateurs dans différentes régions géographiques.</span><span class="sxs-lookup"><span data-stu-id="71849-239">Now, try tooaccess hello URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="71849-240">Les navigateurs clients d’Europe doivent afficher « ASP.NET Europe de l’Ouest », et les navigateurs clients d’Asie doit afficher « ASP.NET Asie du Sud-Est. »</span><span class="sxs-lookup"><span data-stu-id="71849-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="71849-241">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="71849-241">More resources</span></span>
