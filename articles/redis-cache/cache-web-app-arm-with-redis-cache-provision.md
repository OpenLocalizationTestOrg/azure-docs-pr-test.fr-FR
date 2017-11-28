---
title: "Approvisionnement de l’application web avec le cache Redis"
description: "Utilisez un modèle Azure Resource Manager pour déployer une application web Azure avec le cache Redis."
services: app-service
documentationcenter: 
author: steved0x
manager: erickson-doug
editor: 
ms.assetid: 6e99c71f-ef8e-4570-a307-e4c059e60c35
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: 810c1cedd4fe0bd6ecdf9bd32dfb241f5f345300
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="8050f-103">Création d’une application web avec le cache Redis à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="8050f-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="8050f-104">Dans cette rubrique, vous allez apprendre à créer un modèle Azure Resource Manager qui déploie une application web Azure avec le cache Redis.</span><span class="sxs-lookup"><span data-stu-id="8050f-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="8050f-105">Vous allez apprendre comment définir les ressources à déployer et configurer les paramètres qui sont spécifiés lors de l’exécution du déploiement.</span><span class="sxs-lookup"><span data-stu-id="8050f-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="8050f-106">Vous pouvez utiliser ce modèle pour vos propres déploiements, ou le personnaliser afin qu’il réponde à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="8050f-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="8050f-107">Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8050f-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="8050f-108">Pour le modèle complet, consultez la page [Modèle d’application web avec le cache Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="8050f-108">For the complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="8050f-109">Ce que vous allez déployer</span><span class="sxs-lookup"><span data-stu-id="8050f-109">What you will deploy</span></span>
<span data-ttu-id="8050f-110">Dans ce modèle, vous allez déployer :</span><span class="sxs-lookup"><span data-stu-id="8050f-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="8050f-111">Application web Azure</span><span class="sxs-lookup"><span data-stu-id="8050f-111">Azure Web App</span></span>
* <span data-ttu-id="8050f-112">Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="8050f-112">Azure Redis Cache.</span></span>

<span data-ttu-id="8050f-113">Pour exécuter automatiquement le déploiement, cliquez sur le bouton ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8050f-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="8050f-114">[![Déploiement sur Azure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="8050f-114">[![Deploy to Azure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-to-specify"></a><span data-ttu-id="8050f-115">Paramètres à spécifier</span><span class="sxs-lookup"><span data-stu-id="8050f-115">Parameters to specify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="8050f-116">Variables pour les noms</span><span class="sxs-lookup"><span data-stu-id="8050f-116">Variables for names</span></span>
<span data-ttu-id="8050f-117">Ce modèle utilise des variables afin de créer des noms pour les ressources.</span><span class="sxs-lookup"><span data-stu-id="8050f-117">This template uses variables to construct names for the resources.</span></span> <span data-ttu-id="8050f-118">Il utilise la fonction [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) pour construire une valeur basée sur l’identifiant du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8050f-118">It uses the [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function to construct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-to-deploy"></a><span data-ttu-id="8050f-119">Ressources à déployer</span><span class="sxs-lookup"><span data-stu-id="8050f-119">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="8050f-120">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="8050f-120">Redis Cache</span></span>
<span data-ttu-id="8050f-121">Crée le cache Redis Azure utilisé avec l'application web.</span><span class="sxs-lookup"><span data-stu-id="8050f-121">Creates the Azure Redis Cache that is used with the web app.</span></span> <span data-ttu-id="8050f-122">Le nom du cache est spécifié dans la variable **cacheName** .</span><span class="sxs-lookup"><span data-stu-id="8050f-122">The name of the cache is specified in the **cacheName** variable.</span></span>

<span data-ttu-id="8050f-123">Le modèle crée le cache au même emplacement que le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8050f-123">The template creates the cache in the same location as the resource group.</span></span>

    {
      "name": "[variables('cacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[resourceGroup().location]",
      "apiVersion": "2015-08-01",
      "dependsOn": [ ],
      "tags": {
        "displayName": "cache"
      },
      "properties": {
        "sku": {
          "name": "[parameters('cacheSKUName')]",
          "family": "[parameters('cacheSKUFamily')]",
          "capacity": "[parameters('cacheSKUCapacity')]"
        }
      }
    }


### <a name="web-app"></a><span data-ttu-id="8050f-124">Application web</span><span class="sxs-lookup"><span data-stu-id="8050f-124">Web app</span></span>
<span data-ttu-id="8050f-125">Crée l’application web avec le nom spécifié dans la variable **webSiteName** .</span><span class="sxs-lookup"><span data-stu-id="8050f-125">Creates the web app with name specified in the **webSiteName** variable.</span></span>

<span data-ttu-id="8050f-126">Notez que l’application web est configurée selon des paramètres qui lui permettent d’utiliser le cache Redis.</span><span class="sxs-lookup"><span data-stu-id="8050f-126">Notice that the web app is configured with app setting properties that enable it to work with the Redis Cache.</span></span> <span data-ttu-id="8050f-127">Ces paramètres sont créés de façon dynamique en fonction des valeurs fournies lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="8050f-127">This app settings are dynamically created based on values provided during deployment.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[variables('webSiteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Web/serverFarms/', variables('hostingPlanName'))]",
        "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
      ],
      "tags": {
        "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', variables('hostingPlanName'))]": "empty",
        "displayName": "Website"
      },
      "properties": {
        "name": "[variables('webSiteName')]",
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "type": "config",
          "name": "appsettings",
          "dependsOn": [
            "[concat('Microsoft.Web/Sites/', variables('webSiteName'))]",
            "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
          ],
          "properties": {
            "CacheConnection": "[concat(variables('cacheName'),'.redis.cache.windows.net,abortConnect=false,ssl=true,password=', listKeys(resourceId('Microsoft.Cache/Redis', variables('cacheName')), '2015-08-01').primaryKey)]"
          }
        }
      ]
    }

## <a name="commands-to-run-deployment"></a><span data-ttu-id="8050f-128">Commandes pour l’exécution du déploiement</span><span class="sxs-lookup"><span data-stu-id="8050f-128">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="8050f-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8050f-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="8050f-130">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="8050f-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
