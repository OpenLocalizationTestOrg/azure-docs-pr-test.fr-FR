---
title: "Approvisionner un cache Redis à l’aide d’Azure Resource Manager | Microsoft Docs"
description: "Utilisez un modèle Azure Resource Manager pour déployer un cache Redis Azure."
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: cce5d63e8bad2dd066cb4c28e2a8a9cb16c47953
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="67c35-103">Créer un cache Redis à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="67c35-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="67c35-104">Dans cette rubrique, vous allez apprendre à créer un modèle Azure Resource Manager qui déploie un cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="67c35-104">In this topic, you learn how to create an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="67c35-105">Le cache peut être utilisé avec un compte de stockage existant pour conserver les données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="67c35-105">The cache can be used with an existing storage account to keep diagnostic data.</span></span> <span data-ttu-id="67c35-106">Vous allez également apprendre comment définir les ressources à déployer et configurer les paramètres qui sont spécifiés lors de l’exécution du déploiement.</span><span class="sxs-lookup"><span data-stu-id="67c35-106">You also learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="67c35-107">Vous pouvez utiliser ce modèle pour vos propres déploiements, ou le personnaliser afin qu’il réponde à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="67c35-107">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="67c35-108">Actuellement, les paramètres de diagnostic sont partagés entre tous les caches de la même région d’un abonnement.</span><span class="sxs-lookup"><span data-stu-id="67c35-108">Currently, diagnostic settings are shared for all caches in the same region for a subscription.</span></span> <span data-ttu-id="67c35-109">La mise à jour d’un cache dans la région affecte tous les autres caches dans la région.</span><span class="sxs-lookup"><span data-stu-id="67c35-109">Updating one cache in the region affects all other caches in the region.</span></span>

<span data-ttu-id="67c35-110">Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="67c35-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="67c35-111">Pour le modèle complet, consultez le [modèle de cache Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="67c35-111">For the complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="67c35-112">Des modèles Resource Manager pour le nouveau [niveau Premium](cache-premium-tier-intro.md) sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="67c35-112">Resource Manager templates for the new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="67c35-113">Créer un cache Redis Premium avec le clustering</span><span class="sxs-lookup"><span data-stu-id="67c35-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="67c35-114">Créer un cache Redis Premium avec la persistance des données</span><span class="sxs-lookup"><span data-stu-id="67c35-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="67c35-115">Créer un cache Redis Premium avec un réseau virtuel et le clustering facultatif</span><span class="sxs-lookup"><span data-stu-id="67c35-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="67c35-116">Pour connaître les derniers modèles, consultez [Modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/) et recherchez `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="67c35-116">To check for the latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="67c35-117">Ce que vous allez déployer</span><span class="sxs-lookup"><span data-stu-id="67c35-117">What you will deploy</span></span>
<span data-ttu-id="67c35-118">Dans ce modèle, vous allez déployer un cache Redis Azure qui utilise un compte de stockage existant pour les données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="67c35-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="67c35-119">Pour exécuter automatiquement le déploiement, cliquez sur le bouton ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="67c35-119">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="67c35-120">[![Déploiement sur Azure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="67c35-120">[![Deploy to Azure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="67c35-121">Paramètres</span><span class="sxs-lookup"><span data-stu-id="67c35-121">Parameters</span></span>
<span data-ttu-id="67c35-122">Azure Resource Manager vous permet de définir des paramètres pour les valeurs que vous voulez spécifier lorsque le modèle est déployé.</span><span class="sxs-lookup"><span data-stu-id="67c35-122">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="67c35-123">Ce modèle inclut une section appelée Paramètres, qui contient toutes les valeurs de paramètres.</span><span class="sxs-lookup"><span data-stu-id="67c35-123">The template includes a section called Parameters that contains all of the parameter values.</span></span>
<span data-ttu-id="67c35-124">Vous devez définir un paramètre pour les valeurs qui varient en fonction du projet que vous déployez ou de l’environnement dans lequel vous effectuez le déploiement.</span><span class="sxs-lookup"><span data-stu-id="67c35-124">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="67c35-125">Ne définissez pas de paramètres pour les valeurs qui restent inchangées.</span><span class="sxs-lookup"><span data-stu-id="67c35-125">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="67c35-126">Chaque valeur de paramètre est utilisée dans le modèle pour définir les ressources déployées.</span><span class="sxs-lookup"><span data-stu-id="67c35-126">Each parameter value is used in the template to define the resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="67c35-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="67c35-127">redisCacheLocation</span></span>
<span data-ttu-id="67c35-128">Emplacement du cache Redis.</span><span class="sxs-lookup"><span data-stu-id="67c35-128">The location of the Redis Cache.</span></span> <span data-ttu-id="67c35-129">Pour de meilleures performances, utilisez le même emplacement que l’application à utiliser avec le cache.</span><span class="sxs-lookup"><span data-stu-id="67c35-129">For best performance, use the same location as the app to be used with the cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="67c35-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="67c35-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="67c35-131">Nom du compte de stockage existant à utiliser pour les diagnostics.</span><span class="sxs-lookup"><span data-stu-id="67c35-131">The name of the existing storage account to use for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="67c35-132">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="67c35-132">enableNonSslPort</span></span>
<span data-ttu-id="67c35-133">Valeur booléenne qui indique s’il faut autoriser l’accès via des ports non-SSL.</span><span class="sxs-lookup"><span data-stu-id="67c35-133">A boolean value that indicates whether to allow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="67c35-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="67c35-134">diagnosticsStatus</span></span>
<span data-ttu-id="67c35-135">Valeur qui indique si les diagnostics sont activés.</span><span class="sxs-lookup"><span data-stu-id="67c35-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="67c35-136">Utilisez ON ou OFF.</span><span class="sxs-lookup"><span data-stu-id="67c35-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="67c35-137">Ressources à déployer</span><span class="sxs-lookup"><span data-stu-id="67c35-137">Resources to deploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="67c35-138">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="67c35-138">Redis Cache</span></span>
<span data-ttu-id="67c35-139">Crée le cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="67c35-139">Creates the Azure Redis Cache.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-to-run-deployment"></a><span data-ttu-id="67c35-140">Commandes pour exécuter le déploiement</span><span class="sxs-lookup"><span data-stu-id="67c35-140">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="67c35-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="67c35-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="67c35-142">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="67c35-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


