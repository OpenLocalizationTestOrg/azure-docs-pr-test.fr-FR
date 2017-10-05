---
title: "Créer une application hyperscale dans Azure | Microsoft Docs"
description: "Découvrez comment utiliser différents services Azure pour optimiser les performances d’une application ASP.NET dans Azure."
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
ms.openlocfilehash: eac9c5b0d8d0f7802d88e6f4f27d9d23c406e025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="0f7c1-103">Créer une application hyperscale dans Azure</span><span class="sxs-lookup"><span data-stu-id="0f7c1-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="0f7c1-104">Ce didacticiel vous montre comment faire évoluer une application web ASP.NET dans Azure afin d’optimiser les requêtes d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-104">This tutorial shows you how to scale out an ASP.NET web app in Azure to maximize user requests.</span></span>

<span data-ttu-id="0f7c1-105">Avant de commencer, vérifiez que [l’interface de ligne de commande Azure est installée](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-105">Before starting this tutorial, ensure that [the Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="0f7c1-106">[Visual Studio](https://www.visualstudio.com/vs/) doit par ailleurs exécuter l’exemple d’application sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine to run the sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="0f7c1-107">Étape 1 : obtenir l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="0f7c1-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="0f7c1-108">Cette étape consiste à définir le projet ASP.NET local.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-108">In this step, you set up the local ASP.NET project.</span></span>

### <a name="clone-the-application-repository"></a><span data-ttu-id="0f7c1-109">Cloner le référentiel de l’application</span><span class="sxs-lookup"><span data-stu-id="0f7c1-109">Clone the application repository</span></span>

<span data-ttu-id="0f7c1-110">Ouvrez le terminal de ligne de commande de votre choix et tapez la commande `CD` pointant vers un répertoire de travail.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-110">Open the command-line terminal of your choice and `CD` to a working directory.</span></span> <span data-ttu-id="0f7c1-111">Exécutez ensuite les commandes suivantes pour cloner l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-111">Then, run the following commands to clone the sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-the-sample-application-in-visual-studio"></a><span data-ttu-id="0f7c1-112">Exécuter l’exemple d’application dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0f7c1-112">Run the sample application in Visual Studio</span></span>

<span data-ttu-id="0f7c1-113">Ouvrez la solution dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-113">Open the solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="0f7c1-114">Saisissez `F5` pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-114">Type `F5` to run the application.</span></span>

<span data-ttu-id="0f7c1-115">Cet exemple d’application web ASP.NET est fourni à partir du modèle par défaut, persiste à travers différentes sessions d’utilisateurs et utilise le cache de sortie.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-115">This sample ASP.NET web application comes from the default template, and persists user sessions and uses the output cache.</span></span> <span data-ttu-id="0f7c1-116">Examinons `HighScaleApp\Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="0f7c1-117">La méthode `Index()` ajoute un élément de données à la session.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-117">The `Index()` method adds a piece of data to the session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="0f7c1-118">Quant aux méthodes `About()` et `Contact()`, elles mettent leur sortie en cache.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-118">And the `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-to-azure"></a><span data-ttu-id="0f7c1-119">Étape 2 : déployer dans Azure</span><span class="sxs-lookup"><span data-stu-id="0f7c1-119">Step 2 - Deploy to Azure</span></span>
<span data-ttu-id="0f7c1-120">Lors de cette étape, vous créez une application web Azure et y déployez votre exemple d’application ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-120">In this step, you create an Azure web app and deploy your sample ASP.NET application to it.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="0f7c1-121">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="0f7c1-121">Create a resource group</span></span>   
<span data-ttu-id="0f7c1-122">Utilisez [az groupe create](https://docs.microsoft.com/cli/azure/group#create) pour créer un [groupe de ressources](../azure-resource-manager/resource-group-overview.md) dans la région Europe de l’Ouest.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) to create a [resource group](../azure-resource-manager/resource-group-overview.md) in the West Europe region.</span></span> <span data-ttu-id="0f7c1-123">Un groupe de ressources est un emplacement où vous placez toutes les ressources Azure que vous souhaitez gérer ensemble, telles que l’application web et tout serveur principal SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-123">A resource group is where you put all the Azure resources that you want to manage together, such as the web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="0f7c1-124">Pour connaître les valeurs que vous pouvez utiliser pour `---location`, utilisez la commande [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations).</span><span class="sxs-lookup"><span data-stu-id="0f7c1-124">To see what possible values you can use for `---location`, use the [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="0f7c1-125">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="0f7c1-125">Create an App Service plan</span></span>
<span data-ttu-id="0f7c1-126">Utilisez [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) pour créer un [plan App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) « B1 ».</span><span class="sxs-lookup"><span data-stu-id="0f7c1-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) to create a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="0f7c1-127">Un plan App Service est une unité d’échelle pouvant inclure autant d’applications que vous souhaitez monter en puissance ou en charge sur la même infrastructure App Service.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-127">An App Service plan is a scale unit, which can include any number of apps that you want to scale up or out together over the same App Service infrastructure.</span></span> <span data-ttu-id="0f7c1-128">Chaque plan est également affecté à un [niveau tarifaire](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="0f7c1-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="0f7c1-129">Les niveaux supérieurs incluent un matériel plus performant et des fonctionnalités supplémentaires telles que des instances de montée en puissance parallèle supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="0f7c1-130">Pour ce didacticiel, B1 est le niveau minimal qui permet une augmentation de la taille à trois instances.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-130">For this tutorial, B1 is the minimum tier that enables scale out to three instances.</span></span> <span data-ttu-id="0f7c1-131">Vous pouvez toujours déplacer ultérieurement votre application vers le haut ou vers le bas de l’échelle de tarification en exécutant [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="0f7c1-131">You can always move your app up or down the pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="0f7c1-132">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="0f7c1-132">Create a web app</span></span>
<span data-ttu-id="0f7c1-133">Utilisez [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) pour créer une application web avec un nom unique dans `$appName`.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="0f7c1-134">Définir les informations d’identification de déploiement</span><span class="sxs-lookup"><span data-stu-id="0f7c1-134">Set deployment credentials</span></span>
<span data-ttu-id="0f7c1-135">Utilisez [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) pour définir vos informations d’identification pour le déploiement au niveau des comptes pour App Service.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) to set your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="0f7c1-136">Configuration du déploiement Git</span><span class="sxs-lookup"><span data-stu-id="0f7c1-136">Configure Git deployment</span></span>
<span data-ttu-id="0f7c1-137">Utilisez [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) pour configurer le déploiement de Git local.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="0f7c1-138">Cette commande vous fournit une sortie similaire à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="0f7c1-138">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="0f7c1-139">Utilisez l’URL retournée pour configurer votre Git distant.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-139">Use the returned URL to configure your Git remote.</span></span> <span data-ttu-id="0f7c1-140">La commande suivante utilise l’exemple de sortie précédent.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-140">The following command uses the preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-the-sample-application"></a><span data-ttu-id="0f7c1-141">Déployer l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="0f7c1-141">Deploy the sample application</span></span>
<span data-ttu-id="0f7c1-142">Vous êtes maintenant prêt à déployer votre exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-142">You are now ready to deploy your sample application.</span></span> <span data-ttu-id="0f7c1-143">Exécutez `git push`.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="0f7c1-144">À l’invite de mot de passe, utilisez le mot de passe que vous avez spécifié lors de l’exécution de `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-144">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-azure-web-app"></a><span data-ttu-id="0f7c1-145">Accéder à l’application web Azure</span><span class="sxs-lookup"><span data-stu-id="0f7c1-145">Browse to Azure web app</span></span>
<span data-ttu-id="0f7c1-146">Pour exécuter votre application en temps réel dans Azure, exécutez la commande [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse).</span><span class="sxs-lookup"><span data-stu-id="0f7c1-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-to-redis"></a><span data-ttu-id="0f7c1-147">Étape 3 : connexion à Redis</span><span class="sxs-lookup"><span data-stu-id="0f7c1-147">Step 3 - Connect to Redis</span></span>
<span data-ttu-id="0f7c1-148">Dans cette étape, vous configurez le Cache Redis Azure comme cache externe colocalisé dans votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-148">In this step, you set up Azure Redis Cache as an external, colocated cache to your Azure web app.</span></span> <span data-ttu-id="0f7c1-149">Vous pouvez rapidement utiliser Redis pour mettre en cache la sortie de page.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-149">You can quickly utilize Redis to cache your page output.</span></span> <span data-ttu-id="0f7c1-150">En outre, lorsque vous montez vos applications web en charge par la suite , Redis vous permet de conserver les sessions utilisateur sur plusieurs instances en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="0f7c1-151">Création d'un cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="0f7c1-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="0f7c1-152">Utilisez [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) pour créer un Cache Redis Azure et enregistrer la sortie JSON.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create an Azure Redis Cache and save the JSON output.</span></span> <span data-ttu-id="0f7c1-153">Utilisez un nom unique dans `$cacheName`.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-the-application-to-use-redis"></a><span data-ttu-id="0f7c1-154">Configurer l’application pour utiliser Redis</span><span class="sxs-lookup"><span data-stu-id="0f7c1-154">Configure the application to use Redis</span></span>
<span data-ttu-id="0f7c1-155">Formatez la chaîne de connexion pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-155">Format the connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="0f7c1-156">La deuxième ligne devrait vous donner une sortie qui ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="0f7c1-156">The second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="0f7c1-157">Dans Visual Studio, créez un fichier de configuration web à la racine de votre projet du nom de `redis.config` et collez-y le code suivant.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste the following code into it.</span></span> <span data-ttu-id="0f7c1-158">Dans `value`, utilisez la chaîne de connexion à partir de la sortie de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-158">In `value`, use the connection string from the PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="0f7c1-159">Si vous examinez le fichier `.gitignore` dans votre référentiel Git, vous verrez que ce fichier est exclu du contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-159">If you look at the `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="0f7c1-160">Cela permet de conserver vos informations sensibles en sécurité.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="0f7c1-161">Ouvrez `Web.config`.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-161">Open `Web.config`.</span></span> <span data-ttu-id="0f7c1-162">Vous remarquerez l’élément `<appSettings file="redis.config">`, qui obtient le paramètre que vous avez créé dans `redis.config`.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-162">Notice the `<appSettings file="redis.config">` element, which gets the setting you created in `redis.config`.</span></span> 

<span data-ttu-id="0f7c1-163">Recherchez la section commentée incluant `<sessionState>` et `<caching>`.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-163">Find the commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="0f7c1-164">Supprimez les commentaires de cette section.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="0f7c1-165">Ce code recherche la chaîne de connexion Redis définie dans `RedisConnection`.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-165">This code looks for the Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="0f7c1-166">À présent, votre application utilise Redis pour gérer les sessions et la mise en cache.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-166">Your application now uses Redis to manage sessions and caching.</span></span> <span data-ttu-id="0f7c1-167">Saisissez `F5` pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-167">Type `F5` to run the application.</span></span> <span data-ttu-id="0f7c1-168">Si vous le souhaitez, vous pouvez télécharger un client de gestion Redis pour visualiser les données qui sont désormais enregistrées dans le cache.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-168">If you like, you can download a Redis management client to visualize the data that is now saved to the cache.</span></span>

### <a name="configure-the-connection-string-in-azure"></a><span data-ttu-id="0f7c1-169">Configurer la chaîne de connexion dans Azure</span><span class="sxs-lookup"><span data-stu-id="0f7c1-169">Configure the connection string in Azure</span></span>

<span data-ttu-id="0f7c1-170">Pour que votre application fonctionne dans Azure, vous devez configurer la même chaîne de connexion Redis dans votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-170">For your application to work in Azure, you need to configure the same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="0f7c1-171">Dans la mesure où l’élément `redis.config` n’est pas conservé dans le contrôle de code source, il n’est pas déployé sur Azure lorsque vous exécutez un déploiement Git.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-171">Since `redis.config` is not maintained in source control, it is not deployed to Azure when you run Git deployment.</span></span>

<span data-ttu-id="0f7c1-172">Utilisez [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) pour ajouter la chaîne de connexion avec le même nom (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="0f7c1-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add the connection string with the same name (`RedisConnection`).</span></span>

<span data-ttu-id="0f7c1-173">az appservice web config appsettings update--paramètres « RedisConnection = $connstring »--nom $appName--groupe de ressources myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0f7c1-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="0f7c1-174">N’oubliez pas que `$connstring` contient la chaîne de connexion formatée.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-174">Remember that `$connstring` contains the formatted connection string.</span></span>

### <a name="redeploy-the-application-to-azure"></a><span data-ttu-id="0f7c1-175">Redéployer l’application dans Azure</span><span class="sxs-lookup"><span data-stu-id="0f7c1-175">Redeploy the application to Azure</span></span>
<span data-ttu-id="0f7c1-176">Utilisez les commandes Git pour envoyer vos modifications vers Azure</span><span class="sxs-lookup"><span data-stu-id="0f7c1-176">Use Git commands to push your changes to Azure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="0f7c1-177">À l’invite de mot de passe, utilisez le mot de passe que vous avez spécifié lors de l’exécution de `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-177">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="0f7c1-178">Accéder à l’application web Azure</span><span class="sxs-lookup"><span data-stu-id="0f7c1-178">Browse to the Azure web app</span></span>
<span data-ttu-id="0f7c1-179">Utilisez [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) pour voir les modifications appliquées dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see the changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-to-multiple-instances"></a><span data-ttu-id="0f7c1-180">Étape 4 - mise à l’échelle à plusieurs instances</span><span class="sxs-lookup"><span data-stu-id="0f7c1-180">Step 4 - Scale to multiple instances</span></span>
<span data-ttu-id="0f7c1-181">Le plan App Service est l’unité d’échelle de vos applications web Azure.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-181">The App Service plan is the scale unit for your Azure web apps.</span></span> <span data-ttu-id="0f7c1-182">Pour faire évoluer votre application web, vous faites évoluer le plan App Service.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-182">To scale out your web app, you scale the App Service plan.</span></span>

<span data-ttu-id="0f7c1-183">Utilisez [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) pour faire évoluer le plan App Service en trois instances, qui est le nombre maximal autorisé par le niveau de tarification B1.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale out the App Service plan to three instances, which is the maximum number allowed by the B1 pricing tier.</span></span> <span data-ttu-id="0f7c1-184">N’oubliez pas que B1 est le niveau de tarification que vous avez choisi lorsque vous avez créé le plan App Service.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-184">Remember that B1 is the pricing tier that you chose when you created the App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="0f7c1-185">Étape 5 : mise à échelle géographique</span><span class="sxs-lookup"><span data-stu-id="0f7c1-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="0f7c1-186">Lors de la mise à l’échelle géographique, vous exécutez votre application dans plusieurs régions du cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-186">When scaling geographically, you run your app in multiple regions of the Azure cloud.</span></span> <span data-ttu-id="0f7c1-187">Cette configuration équilibre encore davantage la charge de votre application en fonction de la géographie et réduit le temps de réponse en rapprochant votre application des navigateurs clients.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-187">This setup load-balances your app further based on geography and lowers the response time by placing your app closer to client browsers.</span></span>

<span data-ttu-id="0f7c1-188">Dans cette étape, vous faites évoluer votre application web ASP.NET dans une seconde région avec [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="0f7c1-188">In this step, you scale your ASP.NET web app to a second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="0f7c1-189">Une fois cette étape terminée, l’une de vos applications web sera exécutée en Europe de l’Ouest (déjà créée) et une autre en Asie du Sud-Est (pas encore créée).</span><span class="sxs-lookup"><span data-stu-id="0f7c1-189">At the end of the step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="0f7c1-190">Les deux applications seront traitées par la même URL de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-190">Both apps will be served from the same Traffic Manager URL.</span></span>

### <a name="scale-up-the-europe-app-to-standard-tier"></a><span data-ttu-id="0f7c1-191">Mettre à l’échelle l’application en Europe au niveau Standard</span><span class="sxs-lookup"><span data-stu-id="0f7c1-191">Scale up the Europe app to Standard tier</span></span>
<span data-ttu-id="0f7c1-192">Dans App Service, l’intégration avec Azure Traffic Manager requiert le niveau de tarification Standard.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-192">In App Service, integration with Azure Traffic Manager requires the Standard pricing tier.</span></span> <span data-ttu-id="0f7c1-193">Utilisez [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) pour faire évoluer votre plan App Service vers S1.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale up your App Service plan to S1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="0f7c1-194">Créer un profil Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="0f7c1-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="0f7c1-195">Utilisez [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) pour créer un profil Traffic Manager et l’ajouter à votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) to create a Traffic Manager profile and add it to your resource group.</span></span> <span data-ttu-id="0f7c1-196">Utilisez un nom DNS unique dans $dnsName.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="0f7c1-197">`--routing-method Performance` spécifie que ce profil [dirige le trafic utilisateur vers le point de terminaison le plus proche](../traffic-manager/traffic-manager-routing-methods.md).</span><span class="sxs-lookup"><span data-stu-id="0f7c1-197">`--routing-method Performance` specifies that this profile [routes user traffic to the closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-the-resource-id-of-the-europe-app"></a><span data-ttu-id="0f7c1-198">Obtenir l’ID de ressource de l’application en Europe</span><span class="sxs-lookup"><span data-stu-id="0f7c1-198">Get the resource ID of the Europe app</span></span>
<span data-ttu-id="0f7c1-199">Utilisez [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) pour obtenir l’ID de ressource de votre application web.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-europe-app"></a><span data-ttu-id="0f7c1-200">Ajouter un point de terminaison Traffic Manager pour l’application en Europe</span><span class="sxs-lookup"><span data-stu-id="0f7c1-200">Add a Traffic Manager endpoint for the Europe app</span></span>
<span data-ttu-id="0f7c1-201">Utilisez [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) pour ajouter un point de terminaison à votre profil Traffic Manager et utiliser l’ID de ressource de votre application web comme cible.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add an endpoint to your Traffic Manager profile and use the resource ID of your web app as the target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-the-traffic-manager-endpoint-url"></a><span data-ttu-id="0f7c1-202">Obtenir l’URL du point de terminaison Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="0f7c1-202">Get the Traffic Manager endpoint URL</span></span>
<span data-ttu-id="0f7c1-203">Votre profil Traffic Manager dispose désormais d’un point de terminaison qui pointe vers votre application web existante.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-203">Your Traffic Manager profile now has an endpoint that points to your existing web app.</span></span> <span data-ttu-id="0f7c1-204">Utilisez [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) pour en obtenir l’URL.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) to get its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="0f7c1-205">Copiez la sortie dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-205">Copy the output into your browser.</span></span> <span data-ttu-id="0f7c1-206">Vous devriez voir votre application web à nouveau.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="0f7c1-207">Créer un cache Redis Azure en Asie</span><span class="sxs-lookup"><span data-stu-id="0f7c1-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="0f7c1-208">À présent, vous répliquez votre application web Azure pour la région Asie du Sud-Est.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-208">Now, you replicate your Azure web app to the Southeast Asia region.</span></span> <span data-ttu-id="0f7c1-209">Pour commencer, utilisez [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) pour créer un deuxième Cache Redis Azure en Asie du Sud-Est.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-209">To start, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="0f7c1-210">Ce cache doit être colocalisé avec votre application en Asie.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-210">This cache needs to be colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="0f7c1-211">`--name $cacheName-asia` donne au cache le nom du cache d’Europe de l’ouest, avec le suffixe `-asia`.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-211">`--name $cacheName-asia` gives the cache the name of the West Europe cache, with the `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="0f7c1-212">Créer un plan App Service en Asie</span><span class="sxs-lookup"><span data-stu-id="0f7c1-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="0f7c1-213">Utilisez [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) pour créer un second plan App Service dans la région Asie du Sud-Est à l’aide du même niveau S1 que le plan d’Europe de l’Ouest.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) to create a second App Service plan in the Southeast Asia region, using the same S1 tier as the West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="0f7c1-214">Créer une application web en Asie</span><span class="sxs-lookup"><span data-stu-id="0f7c1-214">Create a web app in Asia</span></span>
<span data-ttu-id="0f7c1-215">Utilisez [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) pour créer une seconde application web.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="0f7c1-216">`--name $appName-asia` donne à l’application le nom de l’application d’Europe de l’Ouest, avec le suffixe `-asia`.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-216">`--name $appName-asia` gives the app the name of the West Europe app, with the `-asia` suffix.</span></span>

### <a name="configure-the-connection-string-for-redis"></a><span data-ttu-id="0f7c1-217">Configurer la chaîne de connexion pour Redis</span><span class="sxs-lookup"><span data-stu-id="0f7c1-217">Configure the connection string for Redis</span></span>
<span data-ttu-id="0f7c1-218">Utilisez [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) pour ajouter la chaîne de connexion à l’application web pour le cache d’Asie du Sud-Est.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add to the web app the connection string for the Southeast Asia cache.</span></span>

<span data-ttu-id="0f7c1-219">az appservice web config appsettings update --paramètres « RedisConnection = $($redis.hostname) : $($redis.sslPort), mot de passe = $($redis.accessKeys.primaryKey), ssl = vrai, abortConnect = faux » --nom $appName-asia --groupe de ressources myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0f7c1-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-the-asia-app"></a><span data-ttu-id="0f7c1-220">Configurez le déploiement Git pour l’application en Asie.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-220">Configure Git deployment for the Asia app.</span></span>
<span data-ttu-id="0f7c1-221">Utilisez [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) pour configurer le déploiement de Git local pour la seconde application web.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment for the second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="0f7c1-222">Cette commande vous fournit une sortie similaire à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="0f7c1-222">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="0f7c1-223">Utilisez l’URL retournée pour configurer un second Git distant pour votre référentiel local.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-223">Use the returned URL to configure a second Git remote for your local repository.</span></span> <span data-ttu-id="0f7c1-224">La commande suivante utilise l’exemple de sortie précédent.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-224">The following command uses the preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="0f7c1-225">Déployer votre exemple d’application</span><span class="sxs-lookup"><span data-stu-id="0f7c1-225">Deploy your sample application</span></span>
<span data-ttu-id="0f7c1-226">Exécutez `git push` pour déployer votre exemple d’application pour le deuxième Git distant.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-226">Run `git push` to deploy your sample application to the second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="0f7c1-227">À l’invite de mot de passe, utilisez le mot de passe que vous avez spécifié lors de l’exécution de `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-227">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-asia-app"></a><span data-ttu-id="0f7c1-228">Accéder à l’application en Asie</span><span class="sxs-lookup"><span data-stu-id="0f7c1-228">Browse to the Asia app</span></span>
<span data-ttu-id="0f7c1-229">Pour vérifier que votre application est exécutée en temps réel dans Azure, utilisez [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse).</span><span class="sxs-lookup"><span data-stu-id="0f7c1-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to verify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-the-resource-id-of-the-asia-app"></a><span data-ttu-id="0f7c1-230">Obtenir l’ID de ressource de l’application en Asie</span><span class="sxs-lookup"><span data-stu-id="0f7c1-230">Get the resource ID of the Asia app</span></span>
<span data-ttu-id="0f7c1-231">Utilisez [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) pour obtenir l’ID de ressource de votre application web en Asie du Sud-Est.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-asia-app"></a><span data-ttu-id="0f7c1-232">Ajouter un point de terminaison Traffic Manager pour l’application en Asie</span><span class="sxs-lookup"><span data-stu-id="0f7c1-232">Add a Traffic Manager endpoint for the Asia app</span></span>
<span data-ttu-id="0f7c1-233">Utilisez [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) pour ajouter un deuxième point de terminaison au profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add a second endpoint to the Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-to-web-apps"></a><span data-ttu-id="0f7c1-234">Ajouter un identificateur de région aux applications web</span><span class="sxs-lookup"><span data-stu-id="0f7c1-234">Add region identifier to web apps</span></span>
<span data-ttu-id="0f7c1-235">Utilisez [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) pour ajouter une variable d’environnement propre à la région.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="0f7c1-236">Votre code d’application utilise déjà ce paramètre d’application.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="0f7c1-237">Examinons `HighScaleApp\Views\Home\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="0f7c1-238">Terminé !</span><span class="sxs-lookup"><span data-stu-id="0f7c1-238">Complete!</span></span>

<span data-ttu-id="0f7c1-239">Essayez à présent d’accéder à l’URL de votre profil Traffic Manager à partir de navigateurs dans différentes régions géographiques.</span><span class="sxs-lookup"><span data-stu-id="0f7c1-239">Now, try to access the URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="0f7c1-240">Les navigateurs clients d’Europe doivent afficher « ASP.NET Europe de l’Ouest », et les navigateurs clients d’Asie doit afficher « ASP.NET Asie du Sud-Est. »</span><span class="sxs-lookup"><span data-stu-id="0f7c1-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="0f7c1-241">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="0f7c1-241">More resources</span></span>
