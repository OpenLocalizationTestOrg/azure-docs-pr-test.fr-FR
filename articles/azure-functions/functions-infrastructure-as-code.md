---
title: "déploiement de ressources aaaAutomate pour une application de la fonction dans les fonctions de Azure | Documents Microsoft"
description: "Découvrez comment toobuild un modèle Azure Resource Manager qui déploie votre application de la fonction."
services: Functions
documtationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Azure Functions, fonctions, architecture sans serveur, infrastructure sous forme code, azure resource manager
ms.assetid: d20743e3-aab6-442c-a836-9bcea09bfd32
ms.server: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: b0df0d4ef9fe93213f7b1cb1d1e6b4e14f8b3a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="fb675-104">Automatiser le déploiement de ressources pour votre application de fonction dans Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fb675-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="fb675-105">Vous pouvez utiliser un toodeploy de modèle Azure Resource Manager une application de la fonction.</span><span class="sxs-lookup"><span data-stu-id="fb675-105">You can use an Azure Resource Manager template toodeploy a function app.</span></span> <span data-ttu-id="fb675-106">Cet article présente les ressources de hello requis et les paramètres pour ce faire.</span><span class="sxs-lookup"><span data-stu-id="fb675-106">This article outlines hello required resources and parameters for doing so.</span></span> <span data-ttu-id="fb675-107">Vous devrez peut-être toodeploy des ressources supplémentaires, en fonction de hello [les déclencheurs et les liaisons](functions-triggers-bindings.md) dans votre application de la fonction.</span><span class="sxs-lookup"><span data-stu-id="fb675-107">You might need toodeploy additional resources, depending on hello [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="fb675-108">Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fb675-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="fb675-109">Pour des exemples de modèles, consultez :</span><span class="sxs-lookup"><span data-stu-id="fb675-109">For sample templates, see:</span></span>
- <span data-ttu-id="fb675-110">[Function app on Consumption plan] (Application de fonction dans le plan Consommation)</span><span class="sxs-lookup"><span data-stu-id="fb675-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="fb675-111">[Function app on Azure App Service plan] (Application de fonction dans le plan Azure App Service)</span><span class="sxs-lookup"><span data-stu-id="fb675-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="fb675-112">Ressources nécessaires</span><span class="sxs-lookup"><span data-stu-id="fb675-112">Required resources</span></span>

<span data-ttu-id="fb675-113">Une application de fonction nécessite les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="fb675-113">A function app requires these resources:</span></span>

* <span data-ttu-id="fb675-114">Un compte de [stockage Azure](../storage/index.md)</span><span class="sxs-lookup"><span data-stu-id="fb675-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="fb675-115">Un plan d’hébergement (plan Consommation ou plan App Service)</span><span class="sxs-lookup"><span data-stu-id="fb675-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="fb675-116">Une application de fonction</span><span class="sxs-lookup"><span data-stu-id="fb675-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="fb675-117">Compte de stockage</span><span class="sxs-lookup"><span data-stu-id="fb675-117">Storage account</span></span>

<span data-ttu-id="fb675-118">Un compte de stockage Azure est nécessaire pour une application de fonction.</span><span class="sxs-lookup"><span data-stu-id="fb675-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="fb675-119">Vous avez besoin d’un compte à usage général qui prend en charge les objets blob, les tables, les files d’attente et les fichiers.</span><span class="sxs-lookup"><span data-stu-id="fb675-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="fb675-120">Pour plus d’informations, consultez [Configuration requise du compte de stockage Azure Functions](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="fb675-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
        "accountType": "[parameters('storageAccountType')]"
    }
}
```

<span data-ttu-id="fb675-121">Hello en outre, les propriétés `AzureWebJobsStorage` et `AzureWebJobsDashboard` doivent être spécifiés comme paramètres d’application dans la configuration du site hello.</span><span class="sxs-lookup"><span data-stu-id="fb675-121">In addition, hello properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in hello site configuration.</span></span> <span data-ttu-id="fb675-122">exécution de fonctions d’Azure Hello utilise hello `AzureWebJobsStorage` toocreate les files d’attente interne de chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="fb675-122">hello Azure Functions runtime uses hello `AzureWebJobsStorage` connection string toocreate internal queues.</span></span> <span data-ttu-id="fb675-123">Hello la chaîne de connexion `AzureWebJobsDashboard` est utilisé toolog tooAzure Table stockage et la puissance hello **moniteur** hello portail.</span><span class="sxs-lookup"><span data-stu-id="fb675-123">hello connection string `AzureWebJobsDashboard` is used toolog tooAzure Table storage and power hello **Monitor** tab in hello portal.</span></span>

<span data-ttu-id="fb675-124">Ces propriétés sont spécifiées dans hello `appSettings` collection Bonjour `siteConfig` objet :</span><span class="sxs-lookup"><span data-stu-id="fb675-124">These properties are specified in hello `appSettings` collection in hello `siteConfig` object:</span></span>

```json
"appSettings": [
    {
        "name": "AzureWebJobsStorage",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    },
    {
        "name": "AzureWebJobsDashboard",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    }
```    

### <a name="hosting-plan"></a><span data-ttu-id="fb675-125">Plan d’hébergement</span><span class="sxs-lookup"><span data-stu-id="fb675-125">Hosting plan</span></span>

<span data-ttu-id="fb675-126">définition de Hello Hello plan d’hébergement varie selon que vous utilisez un plan de la consommation ou du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="fb675-126">hello definition of hello hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="fb675-127">Consultez [déployer une application de fonction sur le plan de la consommation hello](#consumption) et [déployer une application de fonction sur hello plan App Service](#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="fb675-127">See [Deploy a function app on hello Consumption plan](#consumption) and [Deploy a function app on hello App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="fb675-128">Conteneur de fonctions</span><span class="sxs-lookup"><span data-stu-id="fb675-128">Function app</span></span>

<span data-ttu-id="fb675-129">ressources d’application Hello fonction est définie à l’aide d’une ressource de type **Microsoft.Web/Site** et type **functionapp**:</span><span class="sxs-lookup"><span data-stu-id="fb675-129">hello function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ]
```

<a name="consumption"></a>

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a><span data-ttu-id="fb675-130">Déployer une application de fonction sur le plan de la consommation de hello</span><span class="sxs-lookup"><span data-stu-id="fb675-130">Deploy a function app on hello Consumption plan</span></span>

<span data-ttu-id="fb675-131">Vous pouvez exécuter une application de la fonction dans deux modes différents : hello du plan de la consommation et hello plan App Service.</span><span class="sxs-lookup"><span data-stu-id="fb675-131">You can run a function app in two different modes: hello Consumption plan and hello App Service plan.</span></span> <span data-ttu-id="fb675-132">plan de la consommation Hello alloue automatiquement la puissance de calcul lorsque votre code est en cours d’exécution, peut évoluer en tant que charge de toohandle nécessaires, puis met à l’échelle vers le bas lorsque le code n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="fb675-132">hello Consumption plan automatically allocates compute power when your code is running, scales out as necessary toohandle load, and then scales down when code is not running.</span></span> <span data-ttu-id="fb675-133">Par conséquent, vous n’avez pas toopay pour les machines virtuelles inactives, et vous n’avez pas la capacité de tooreserve à l’avance.</span><span class="sxs-lookup"><span data-stu-id="fb675-133">So, you don't have toopay for idle VMs, and you don't have tooreserve capacity in advance.</span></span> <span data-ttu-id="fb675-134">toolearn en savoir plus sur l’hébergement des plans, consultez [plans de consommation de fonctions d’Azure et le Service application](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="fb675-134">toolearn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="fb675-135">Pour un exemple de modèle Azure Resource Manager, consultez [Function app on Consumption plan] (Application de fonction dans le plan Consommation).</span><span class="sxs-lookup"><span data-stu-id="fb675-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="fb675-136">Créer un plan Consommation</span><span class="sxs-lookup"><span data-stu-id="fb675-136">Create a Consumption plan</span></span>

<span data-ttu-id="fb675-137">Un plan Consommation est un type spécial de ressource « serverfarm ».</span><span class="sxs-lookup"><span data-stu-id="fb675-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="fb675-138">Vous la spécifiez à l’aide de hello `Dynamic` valeur hello `computeMode` et `sku` propriétés :</span><span class="sxs-lookup"><span data-stu-id="fb675-138">You specify it by using hello `Dynamic` value for hello `computeMode` and `sku` properties:</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

### <a name="create-a-function-app"></a><span data-ttu-id="fb675-139">Créer une Function App</span><span class="sxs-lookup"><span data-stu-id="fb675-139">Create a function app</span></span>

<span data-ttu-id="fb675-140">En outre, un plan de la consommation nécessite deux paramètres supplémentaires dans la configuration du site hello : `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` et `WEBSITE_CONTENTSHARE`.</span><span class="sxs-lookup"><span data-stu-id="fb675-140">In addition, a Consumption plan requires two additional settings in hello site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="fb675-141">Ces propriétés configurer hello stockage compte et le fichier de chemin d’accès où le code d’application hello fonction et la configuration sont stockés.</span><span class="sxs-lookup"><span data-stu-id="fb675-141">These properties configure hello storage account and file path where hello function app code and configuration are stored.</span></span>

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ],
    "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "siteConfig": {
            "appSettings": [
                {
                    "name": "AzureWebJobsDashboard",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "AzureWebJobsStorage",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTSHARE",
                    "value": "[toLower(variables('functionAppName'))]"
                },
                {
                    "name": "FUNCTIONS_EXTENSION_VERSION",
                    "value": "~1"
                }
            ]
        }
    }
}
```                    

<a name="app-service-plan"></a> 

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a><span data-ttu-id="fb675-142">Déployer une application de fonction sur hello plan App Service</span><span class="sxs-lookup"><span data-stu-id="fb675-142">Deploy a function app on hello App Service plan</span></span>

<span data-ttu-id="fb675-143">Bonjour plan App Service, votre application de la fonction s’exécute sur des machines virtuelles dédiées sur Basic, Standard et Premium SKU, les applications tooweb similaire.</span><span class="sxs-lookup"><span data-stu-id="fb675-143">In hello App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar tooweb apps.</span></span> <span data-ttu-id="fb675-144">Pour plus d’informations sur le fonctionne de hello plan App Service, consultez hello [vue d’ensemble approfondie des plans de Service d’applications Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fb675-144">For details about how hello App Service plan works, see hello [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="fb675-145">Pour un exemple de modèle Azure Resource Manager, consultez [Function app on Azure App Service plan] (Application de fonction dans le plan Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="fb675-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="fb675-146">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="fb675-146">Create an App Service plan</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="create-a-function-app"></a><span data-ttu-id="fb675-147">Créer une application de fonction</span><span class="sxs-lookup"><span data-stu-id="fb675-147">Create a function app</span></span> 

<span data-ttu-id="fb675-148">Une fois que vous avez sélectionné une option de mise à l’échelle, créez une application de fonction.</span><span class="sxs-lookup"><span data-stu-id="fb675-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="fb675-149">application Hello est un conteneur hello qui contient toutes vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="fb675-149">hello app is hello container that holds all your functions.</span></span>

<span data-ttu-id="fb675-150">Une application de fonction dispose de nombreuses ressources enfant que vous pouvez utiliser dans votre développement, notamment les paramètres de l’application et les options de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="fb675-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="fb675-151">Vous pouvez également choisir tooremove hello **sourcecontrols** ressource enfant et utilisez une autre [l’option de déploiement](functions-continuous-deployment.md) à la place.</span><span class="sxs-lookup"><span data-stu-id="fb675-151">You also might choose tooremove hello **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb675-152">toosuccessfully déployer votre application à l’aide du Gestionnaire de ressources Azure, il est important toounderstand comment les ressources sont déployées dans Azure.</span><span class="sxs-lookup"><span data-stu-id="fb675-152">toosuccessfully deploy your application by using Azure Resource Manager, it's important toounderstand how resources are deployed in Azure.</span></span> <span data-ttu-id="fb675-153">Bonjour l’exemple suivant, les configurations de niveau supérieur sont appliquées à l’aide de **configuration**.</span><span class="sxs-lookup"><span data-stu-id="fb675-153">In hello following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="fb675-154">Il est important tooset ces configurations à un haut niveau, car ils fournissent des informations toohello fonctions runtime et le déploiement du moteur.</span><span class="sxs-lookup"><span data-stu-id="fb675-154">It's important tooset these configurations at a top level, because they convey information toohello Functions runtime and deployment engine.</span></span> <span data-ttu-id="fb675-155">Informations de niveau supérieur sont requis avant les enfants hello **sourcecontrols/web** ressource est appliquée.</span><span class="sxs-lookup"><span data-stu-id="fb675-155">Top-level information is required before hello child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="fb675-156">Bien qu’il soit possible de tooconfigure ces paramètres dans hello niveau enfant **configuration/appSettings** ressource, dans certains cas, votre application de la fonction doit être déployée *avant* **configuration/appSettings**  est appliqué.</span><span class="sxs-lookup"><span data-stu-id="fb675-156">Although it's possible tooconfigure these settings in hello child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="fb675-157">Par exemple, quand vous utilisez des fonctions avec [Logic Apps](../logic-apps/index.md), vos fonctions sont une dépendance d’une autre ressource.</span><span class="sxs-lookup"><span data-stu-id="fb675-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> <span data-ttu-id="fb675-158">Ce modèle utilise hello [projet](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) valeur de paramètres d’application qui définit le répertoire de base hello dans le hello moteur de déploiement de fonctions (Kudu) recherche de code pouvant être déployée.</span><span class="sxs-lookup"><span data-stu-id="fb675-158">This template uses hello [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets hello base directory in which hello Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="fb675-159">Dans notre référentiel, nos fonctions se trouvent dans un sous-dossier de hello **src** dossier.</span><span class="sxs-lookup"><span data-stu-id="fb675-159">In our repository, our functions are in a subfolder of hello **src** folder.</span></span> <span data-ttu-id="fb675-160">Par conséquent, dans hello précédent exemple, nous avons défini valeur de paramètres d’application hello trop`src`.</span><span class="sxs-lookup"><span data-stu-id="fb675-160">So, in hello preceding example, we set hello app settings value too`src`.</span></span> <span data-ttu-id="fb675-161">Si vos fonctions se trouvent dans votre référentiel racine hello, ou si vous ne déployez pas de contrôle de code source, vous pouvez supprimer cette valeur de paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="fb675-161">If your functions are in hello root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="fb675-162">Déployer votre modèle</span><span class="sxs-lookup"><span data-stu-id="fb675-162">Deploy your template</span></span>

<span data-ttu-id="fb675-163">Vous pouvez utiliser les Hello suivant façons toodeploy votre modèle :</span><span class="sxs-lookup"><span data-stu-id="fb675-163">You can use any of hello following ways toodeploy your template:</span></span>

* [<span data-ttu-id="fb675-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb675-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="fb675-165">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="fb675-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="fb675-166">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="fb675-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="fb675-167">API REST</span><span class="sxs-lookup"><span data-stu-id="fb675-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a><span data-ttu-id="fb675-168">TooAzure bouton déployer</span><span class="sxs-lookup"><span data-stu-id="fb675-168">Deploy tooAzure button</span></span>

<span data-ttu-id="fb675-169">Remplacez ```<url-encoded-path-to-azuredeploy-json>``` avec un [encodé en URL](https://www.bing.com/search?q=url+encode) version du chemin d’accès brutes de hello de votre `azuredeploy.json` fichier dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="fb675-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of hello raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="fb675-170">Voici un exemple qui utilise markdown :</span><span class="sxs-lookup"><span data-stu-id="fb675-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="fb675-171">Voici un exemple qui utilise HTML :</span><span class="sxs-lookup"><span data-stu-id="fb675-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="fb675-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fb675-172">Next steps</span></span>

<span data-ttu-id="fb675-173">En savoir plus sur la façon de toodevelop et configurer les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="fb675-173">Learn more about how toodevelop and configure Azure Functions.</span></span>

* [<span data-ttu-id="fb675-174">Référence du développeur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fb675-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="fb675-175">Fonctionnement des paramètres de l’application tooconfigure Azure</span><span class="sxs-lookup"><span data-stu-id="fb675-175">How tooconfigure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="fb675-176">Créer votre première fonction Azure</span><span class="sxs-lookup"><span data-stu-id="fb675-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[Function app on Consumption plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json (Application de fonction dans le plan Consommation)
[Function app on Azure App Service plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json (Application de fonction dans le plan Azure App Service)
