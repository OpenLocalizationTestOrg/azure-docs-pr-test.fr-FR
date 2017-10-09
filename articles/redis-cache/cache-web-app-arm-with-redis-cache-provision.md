---
title: aaaProvision application Web avec le Cache Redis
description: "Utilisez Azure Resource Manager modèle toodeploy l’application web avec le Cache Redis."
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
ms.openlocfilehash: b95b5e230dc40c1157940c2017cba836975b6930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="ef21a-103">Création d’une application web avec le cache Redis à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="ef21a-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="ef21a-104">Dans cette rubrique, vous allez apprendre comment toocreate un modèle Azure Resource Manager qui déploie une application Web de Azure avec le cache Redis.</span><span class="sxs-lookup"><span data-stu-id="ef21a-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="ef21a-105">Vous allez apprendre comment toodefine les ressources qui sont déployés et comment les paramètres toodefine sont spécifiés lorsque le déploiement de hello est exécutée.</span><span class="sxs-lookup"><span data-stu-id="ef21a-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="ef21a-106">Vous pouvez utiliser ce modèle pour vos propres déploiements, ou personnaliser toomeet vos besoins.</span><span class="sxs-lookup"><span data-stu-id="ef21a-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="ef21a-107">Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ef21a-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="ef21a-108">Pour le modèle complète de hello, consultez [application Web avec le modèle de Cache Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="ef21a-108">For hello complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="ef21a-109">Ce que vous allez déployer</span><span class="sxs-lookup"><span data-stu-id="ef21a-109">What you will deploy</span></span>
<span data-ttu-id="ef21a-110">Dans ce modèle, vous allez déployer :</span><span class="sxs-lookup"><span data-stu-id="ef21a-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="ef21a-111">Application web Azure</span><span class="sxs-lookup"><span data-stu-id="ef21a-111">Azure Web App</span></span>
* <span data-ttu-id="ef21a-112">Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="ef21a-112">Azure Redis Cache.</span></span>

<span data-ttu-id="ef21a-113">toorun hello déploiement automatiquement, cliquez sur hello suivant bouton :</span><span class="sxs-lookup"><span data-stu-id="ef21a-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="ef21a-114">[![Déployer tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="ef21a-114">[![Deploy tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-toospecify"></a><span data-ttu-id="ef21a-115">Paramètres toospecify</span><span class="sxs-lookup"><span data-stu-id="ef21a-115">Parameters toospecify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="ef21a-116">Variables pour les noms</span><span class="sxs-lookup"><span data-stu-id="ef21a-116">Variables for names</span></span>
<span data-ttu-id="ef21a-117">Ce modèle utilise des noms de tooconstruct de variables pour les ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="ef21a-117">This template uses variables tooconstruct names for hello resources.</span></span> <span data-ttu-id="ef21a-118">Il utilise hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) tooconstruct une valeur basée sur l’id de groupe de ressources de la fonction.</span><span class="sxs-lookup"><span data-stu-id="ef21a-118">It uses hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function tooconstruct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-toodeploy"></a><span data-ttu-id="ef21a-119">Ressources toodeploy</span><span class="sxs-lookup"><span data-stu-id="ef21a-119">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="ef21a-120">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="ef21a-120">Redis Cache</span></span>
<span data-ttu-id="ef21a-121">Crée hello du Cache Redis Azure qui est utilisé avec l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="ef21a-121">Creates hello Azure Redis Cache that is used with hello web app.</span></span> <span data-ttu-id="ef21a-122">nom de Hello du cache de hello est spécifié dans hello **cacheName** variable.</span><span class="sxs-lookup"><span data-stu-id="ef21a-122">hello name of hello cache is specified in hello **cacheName** variable.</span></span>

<span data-ttu-id="ef21a-123">modèle de Hello crée un cache de hello Bonjour même emplacement que le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="ef21a-123">hello template creates hello cache in hello same location as hello resource group.</span></span>

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


### <a name="web-app"></a><span data-ttu-id="ef21a-124">Application web</span><span class="sxs-lookup"><span data-stu-id="ef21a-124">Web app</span></span>
<span data-ttu-id="ef21a-125">Crée l’application hello web avec le nom spécifié dans hello **webSiteName** variable.</span><span class="sxs-lookup"><span data-stu-id="ef21a-125">Creates hello web app with name specified in hello **webSiteName** variable.</span></span>

<span data-ttu-id="ef21a-126">Notez que l’application hello web est configurée avec application de définir des propriétés qui lui toowork avec hello du Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="ef21a-126">Notice that hello web app is configured with app setting properties that enable it toowork with hello Redis Cache.</span></span> <span data-ttu-id="ef21a-127">Ces paramètres sont créés de façon dynamique en fonction des valeurs fournies lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="ef21a-127">This app settings are dynamically created based on values provided during deployment.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="ef21a-128">Déploiement de toorun de commandes</span><span class="sxs-lookup"><span data-stu-id="ef21a-128">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="ef21a-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef21a-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="ef21a-130">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="ef21a-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
