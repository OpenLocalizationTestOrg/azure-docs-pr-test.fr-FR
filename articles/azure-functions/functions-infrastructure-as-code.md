---
title: "Automatiser le déploiement de ressources pour une application de fonction dans Azure Functions | Microsoft Docs"
description: "Découvrez comment créer un modèle Azure Resource Manager qui déploie votre application de fonction."
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
ms.openlocfilehash: 15496e4ab2858b2aa319d53f1c438a259a3d5e49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="29cd6-104">Automatiser le déploiement de ressources pour votre application de fonction dans Azure Functions</span><span class="sxs-lookup"><span data-stu-id="29cd6-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="29cd6-105">Vous pouvez utiliser un modèle Azure Resource Manager pour déployer une application de fonction.</span><span class="sxs-lookup"><span data-stu-id="29cd6-105">You can use an Azure Resource Manager template to deploy a function app.</span></span> <span data-ttu-id="29cd6-106">Cet article présente les ressources et paramètres nécessaires pour effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="29cd6-106">This article outlines the required resources and parameters for doing so.</span></span> <span data-ttu-id="29cd6-107">Vous devrez peut-être déployer des ressources supplémentaires, selon les [déclencheurs et liaisons](functions-triggers-bindings.md) présents dans votre application de fonction.</span><span class="sxs-lookup"><span data-stu-id="29cd6-107">You might need to deploy additional resources, depending on the [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="29cd6-108">Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="29cd6-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="29cd6-109">Pour des exemples de modèles, consultez :</span><span class="sxs-lookup"><span data-stu-id="29cd6-109">For sample templates, see:</span></span>
- <span data-ttu-id="29cd6-110">[Function app on Consumption plan] (Application de fonction dans le plan Consommation)</span><span class="sxs-lookup"><span data-stu-id="29cd6-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="29cd6-111">[Function app on Azure App Service plan] (Application de fonction dans le plan Azure App Service)</span><span class="sxs-lookup"><span data-stu-id="29cd6-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="29cd6-112">Ressources nécessaires</span><span class="sxs-lookup"><span data-stu-id="29cd6-112">Required resources</span></span>

<span data-ttu-id="29cd6-113">Une application de fonction nécessite les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="29cd6-113">A function app requires these resources:</span></span>

* <span data-ttu-id="29cd6-114">Un compte de [stockage Azure](../storage/index.md)</span><span class="sxs-lookup"><span data-stu-id="29cd6-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="29cd6-115">Un plan d’hébergement (plan Consommation ou plan App Service)</span><span class="sxs-lookup"><span data-stu-id="29cd6-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="29cd6-116">Une application de fonction</span><span class="sxs-lookup"><span data-stu-id="29cd6-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="29cd6-117">Compte de stockage</span><span class="sxs-lookup"><span data-stu-id="29cd6-117">Storage account</span></span>

<span data-ttu-id="29cd6-118">Un compte de stockage Azure est nécessaire pour une application de fonction.</span><span class="sxs-lookup"><span data-stu-id="29cd6-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="29cd6-119">Vous avez besoin d’un compte à usage général qui prend en charge les objets blob, les tables, les files d’attente et les fichiers.</span><span class="sxs-lookup"><span data-stu-id="29cd6-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="29cd6-120">Pour plus d’informations, consultez [Configuration requise du compte de stockage Azure Functions](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="29cd6-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

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

<span data-ttu-id="29cd6-121">En outre, les propriétés `AzureWebJobsStorage` et `AzureWebJobsDashboard` doivent être spécifiées comme paramètres d’application dans la configuration du site.</span><span class="sxs-lookup"><span data-stu-id="29cd6-121">In addition, the properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in the site configuration.</span></span> <span data-ttu-id="29cd6-122">Le runtime d’Azure Functions utilise la chaîne de connexion `AzureWebJobsStorage` pour créer des files d’attente internes.</span><span class="sxs-lookup"><span data-stu-id="29cd6-122">The Azure Functions runtime uses the `AzureWebJobsStorage` connection string to create internal queues.</span></span> <span data-ttu-id="29cd6-123">La chaîne de connexion `AzureWebJobsDashboard` est utilisée pour la connexion au stockage de table Azure et l’alimentation de l’onglet **Surveiller** du portail.</span><span class="sxs-lookup"><span data-stu-id="29cd6-123">The connection string `AzureWebJobsDashboard` is used to log to Azure Table storage and power the **Monitor** tab in the portal.</span></span>

<span data-ttu-id="29cd6-124">Ces propriétés sont spécifiées dans la collection `appSettings` de l’objet `siteConfig` :</span><span class="sxs-lookup"><span data-stu-id="29cd6-124">These properties are specified in the `appSettings` collection in the `siteConfig` object:</span></span>

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

### <a name="hosting-plan"></a><span data-ttu-id="29cd6-125">Plan d’hébergement</span><span class="sxs-lookup"><span data-stu-id="29cd6-125">Hosting plan</span></span>

<span data-ttu-id="29cd6-126">La définition du plan d’hébergement varie, selon que vous utilisez un plan Consommation ou un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="29cd6-126">The definition of the hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="29cd6-127">Consultez [Déployer une application de fonction dans le plan Consommation](#consumption) et [Déployer une application de fonction dans le plan App Service](#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="29cd6-127">See [Deploy a function app on the Consumption plan](#consumption) and [Deploy a function app on the App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="29cd6-128">Conteneur de fonctions</span><span class="sxs-lookup"><span data-stu-id="29cd6-128">Function app</span></span>

<span data-ttu-id="29cd6-129">La ressource d’application de fonction est définie à l’aide d’une ressource de type **Microsoft.Web/Site** et de genre **functionapp** :</span><span class="sxs-lookup"><span data-stu-id="29cd6-129">The function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

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

## <a name="deploy-a-function-app-on-the-consumption-plan"></a><span data-ttu-id="29cd6-130">Déployer une application de fonction dans le plan Consommation</span><span class="sxs-lookup"><span data-stu-id="29cd6-130">Deploy a function app on the Consumption plan</span></span>

<span data-ttu-id="29cd6-131">Vous pouvez exécuter une application de fonction dans deux modes différents : le plan Consommation et le plan App Service.</span><span class="sxs-lookup"><span data-stu-id="29cd6-131">You can run a function app in two different modes: the Consumption plan and the App Service plan.</span></span> <span data-ttu-id="29cd6-132">Le plan Consommation alloue automatiquement la puissance de calcul pendant l’exécution du code, augmente la taille des instances quand c’est nécessaire pour gérer la charge, puis descend en puissance quand le code n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="29cd6-132">The Consumption plan automatically allocates compute power when your code is running, scales out as necessary to handle load, and then scales down when code is not running.</span></span> <span data-ttu-id="29cd6-133">Vous n’avez donc pas à payer pour des machines virtuelles inactives ni à disposer d’une capacité de réserve à l’avance.</span><span class="sxs-lookup"><span data-stu-id="29cd6-133">So, you don't have to pay for idle VMs, and you don't have to reserve capacity in advance.</span></span> <span data-ttu-id="29cd6-134">Pour en savoir plus sur les plans d’hébergement, consultez [Plans Consommation et App Service d’Azure Functions](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="29cd6-134">To learn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="29cd6-135">Pour un exemple de modèle Azure Resource Manager, consultez [Function app on Consumption plan] (Application de fonction dans le plan Consommation).</span><span class="sxs-lookup"><span data-stu-id="29cd6-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="29cd6-136">Créer un plan Consommation</span><span class="sxs-lookup"><span data-stu-id="29cd6-136">Create a Consumption plan</span></span>

<span data-ttu-id="29cd6-137">Un plan Consommation est un type spécial de ressource « serverfarm ».</span><span class="sxs-lookup"><span data-stu-id="29cd6-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="29cd6-138">Vous le spécifiez en utilisant la valeur `Dynamic` pour les propriétés `computeMode` et `sku` :</span><span class="sxs-lookup"><span data-stu-id="29cd6-138">You specify it by using the `Dynamic` value for the `computeMode` and `sku` properties:</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="29cd6-139">Créer une application de fonction</span><span class="sxs-lookup"><span data-stu-id="29cd6-139">Create a function app</span></span>

<span data-ttu-id="29cd6-140">En outre, un plan Consommation nécessite deux paramètres supplémentaires dans la configuration du site : `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` et `WEBSITE_CONTENTSHARE`.</span><span class="sxs-lookup"><span data-stu-id="29cd6-140">In addition, a Consumption plan requires two additional settings in the site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="29cd6-141">Ces propriétés configurent le compte de stockage et le chemin de fichier où le code de l’application de fonction et la configuration sont stockés.</span><span class="sxs-lookup"><span data-stu-id="29cd6-141">These properties configure the storage account and file path where the function app code and configuration are stored.</span></span>

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

## <a name="deploy-a-function-app-on-the-app-service-plan"></a><span data-ttu-id="29cd6-142">Déployer une application de fonction dans le plan App Service</span><span class="sxs-lookup"><span data-stu-id="29cd6-142">Deploy a function app on the App Service plan</span></span>

<span data-ttu-id="29cd6-143">Dans le plan App Service, vos applications de fonction sont exécutées sur des machines virtuelles dédiées sur des références de base, Standard et Premium, à l’instar des applications web.</span><span class="sxs-lookup"><span data-stu-id="29cd6-143">In the App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar to web apps.</span></span> <span data-ttu-id="29cd6-144">Pour plus d’informations sur le fonctionnement du plan App Service, consultez l’article [Présentation détaillée des plans d’Azure App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="29cd6-144">For details about how the App Service plan works, see the [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="29cd6-145">Pour un exemple de modèle Azure Resource Manager, consultez [Function app on Azure App Service plan] (Application de fonction dans le plan Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="29cd6-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="29cd6-146">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="29cd6-146">Create an App Service plan</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="29cd6-147">Créer une application de fonction</span><span class="sxs-lookup"><span data-stu-id="29cd6-147">Create a function app</span></span> 

<span data-ttu-id="29cd6-148">Une fois que vous avez sélectionné une option de mise à l’échelle, créez une application de fonction.</span><span class="sxs-lookup"><span data-stu-id="29cd6-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="29cd6-149">L’application est le conteneur regroupant toutes vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="29cd6-149">The app is the container that holds all your functions.</span></span>

<span data-ttu-id="29cd6-150">Une application de fonction dispose de nombreuses ressources enfant que vous pouvez utiliser dans votre développement, notamment les paramètres de l’application et les options de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="29cd6-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="29cd6-151">Vous pouvez également choisir de supprimer la ressource enfant **sourcecontrols** et utiliser une autre [option de déploiement](functions-continuous-deployment.md) à la place.</span><span class="sxs-lookup"><span data-stu-id="29cd6-151">You also might choose to remove the **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29cd6-152">Il est important de comprendre comment les ressources sont déployées dans Azure pour déployer correctement votre application en utilisant Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="29cd6-152">To successfully deploy your application by using Azure Resource Manager, it's important to understand how resources are deployed in Azure.</span></span> <span data-ttu-id="29cd6-153">Dans l’exemple suivant, les configurations de niveau supérieur sont appliquées à l’aide de **siteConfig**.</span><span class="sxs-lookup"><span data-stu-id="29cd6-153">In the following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="29cd6-154">Il est important de définir ces configurations à un niveau supérieur, car elles fournissent des informations au moteur de déploiement et au runtime Functions.</span><span class="sxs-lookup"><span data-stu-id="29cd6-154">It's important to set these configurations at a top level, because they convey information to the Functions runtime and deployment engine.</span></span> <span data-ttu-id="29cd6-155">Des informations de niveau supérieur sont requises avant que la ressource enfant **sourcecontrols/web** soit appliquée.</span><span class="sxs-lookup"><span data-stu-id="29cd6-155">Top-level information is required before the child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="29cd6-156">Bien qu’il soit possible de configurer ces paramètres dans la ressource **configuration/appSettings** au niveau enfant, dans certains cas, votre application de fonction doit être déployée *avant* que la ressource **configuration/appSettings** soit appliquée.</span><span class="sxs-lookup"><span data-stu-id="29cd6-156">Although it's possible to configure these settings in the child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="29cd6-157">Par exemple, quand vous utilisez des fonctions avec [Logic Apps](../logic-apps/index.md), vos fonctions sont une dépendance d’une autre ressource.</span><span class="sxs-lookup"><span data-stu-id="29cd6-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

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
> <span data-ttu-id="29cd6-158">Dans ce modèle, la valeur du paramètre d’application [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file), qui définit le répertoire de base dans lequel le moteur de déploiement de fonctions (Kudu) recherche le code pouvant être déployé, est utilisée.</span><span class="sxs-lookup"><span data-stu-id="29cd6-158">This template uses the [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets the base directory in which the Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="29cd6-159">Dans notre référentiel, nos fonctions se trouvent dans un sous-dossier du dossier **src**.</span><span class="sxs-lookup"><span data-stu-id="29cd6-159">In our repository, our functions are in a subfolder of the **src** folder.</span></span> <span data-ttu-id="29cd6-160">Par conséquent, dans l’exemple précédent, nous définissons la valeur de paramètres d’application sur `src`.</span><span class="sxs-lookup"><span data-stu-id="29cd6-160">So, in the preceding example, we set the app settings value to `src`.</span></span> <span data-ttu-id="29cd6-161">Si vos fonctions sont à la racine de votre référentiel, ou si vous ne déployez pas de contrôle de code source, vous pouvez supprimer cette valeur de paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="29cd6-161">If your functions are in the root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="29cd6-162">Déployer votre modèle</span><span class="sxs-lookup"><span data-stu-id="29cd6-162">Deploy your template</span></span>

<span data-ttu-id="29cd6-163">Vous pouvez utiliser une des méthodes suivantes pour déployer votre modèle :</span><span class="sxs-lookup"><span data-stu-id="29cd6-163">You can use any of the following ways to deploy your template:</span></span>

* [<span data-ttu-id="29cd6-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="29cd6-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="29cd6-165">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="29cd6-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="29cd6-166">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="29cd6-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="29cd6-167">API REST</span><span class="sxs-lookup"><span data-stu-id="29cd6-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-to-azure-button"></a><span data-ttu-id="29cd6-168">Bouton Déployer dans Azure</span><span class="sxs-lookup"><span data-stu-id="29cd6-168">Deploy to Azure button</span></span>

<span data-ttu-id="29cd6-169">Remplacez ```<url-encoded-path-to-azuredeploy-json>``` par une version [d’URL encodée](https://www.bing.com/search?q=url+encode) du chemin brut de votre fichier `azuredeploy.json` dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="29cd6-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of the raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="29cd6-170">Voici un exemple qui utilise markdown :</span><span class="sxs-lookup"><span data-stu-id="29cd6-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="29cd6-171">Voici un exemple qui utilise HTML :</span><span class="sxs-lookup"><span data-stu-id="29cd6-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="29cd6-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29cd6-172">Next steps</span></span>

<span data-ttu-id="29cd6-173">En savoir plus sur le développement et la configuration d’Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="29cd6-173">Learn more about how to develop and configure Azure Functions.</span></span>

* [<span data-ttu-id="29cd6-174">Informations de référence pour les développeurs sur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="29cd6-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="29cd6-175">Guide pratique pour configurer les paramètres d’application de fonction Azure</span><span class="sxs-lookup"><span data-stu-id="29cd6-175">How to configure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="29cd6-176">Créer votre première fonction Azure</span><span class="sxs-lookup"><span data-stu-id="29cd6-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[Function app on Consumption plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json (Application de fonction dans le plan Consommation)
[Function app on Azure App Service plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json (Application de fonction dans le plan Azure App Service)
