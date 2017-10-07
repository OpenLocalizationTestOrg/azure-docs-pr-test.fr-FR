---
title: "aaaProvision un Cache Redis à l’aide du Gestionnaire de ressources Azure | Documents Microsoft"
description: "Utilisez le Gestionnaire de ressources Azure modèle toodeploy un cache Azure Redis Cache."
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
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="567b3-103">Créer un cache Redis à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="567b3-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="567b3-104">Dans cette rubrique, vous apprendrez comment toocreate un modèle Azure Resource Manager qui déploie un Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="567b3-104">In this topic, you learn how toocreate an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="567b3-105">cache de Hello peut être utilisé avec un stockage compte tookeep diagnostic des données existantes.</span><span class="sxs-lookup"><span data-stu-id="567b3-105">hello cache can be used with an existing storage account tookeep diagnostic data.</span></span> <span data-ttu-id="567b3-106">Vous apprendrez également comment toodefine les ressources qui sont déployés et comment les paramètres toodefine sont spécifiés lorsque le déploiement de hello est exécutée.</span><span class="sxs-lookup"><span data-stu-id="567b3-106">You also learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="567b3-107">Vous pouvez utiliser ce modèle pour vos propres déploiements, ou personnaliser toomeet vos besoins.</span><span class="sxs-lookup"><span data-stu-id="567b3-107">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="567b3-108">Actuellement, les paramètres de diagnostic sont partagés pour tous les caches Bonjour même région pour un abonnement.</span><span class="sxs-lookup"><span data-stu-id="567b3-108">Currently, diagnostic settings are shared for all caches in hello same region for a subscription.</span></span> <span data-ttu-id="567b3-109">Mise à jour un cache dans la région de hello affecte tous les autres caches dans la région de hello.</span><span class="sxs-lookup"><span data-stu-id="567b3-109">Updating one cache in hello region affects all other caches in hello region.</span></span>

<span data-ttu-id="567b3-110">Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="567b3-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="567b3-111">Pour le modèle complète de hello, consultez [modèle de Cache Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="567b3-111">For hello complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="567b3-112">Modèles de gestionnaire de ressources pour hello nouvelle [niveau Premium](cache-premium-tier-intro.md) sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="567b3-112">Resource Manager templates for hello new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="567b3-113">Créer un cache Redis Premium avec le clustering</span><span class="sxs-lookup"><span data-stu-id="567b3-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="567b3-114">Créer un cache Redis Premium avec la persistance des données</span><span class="sxs-lookup"><span data-stu-id="567b3-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="567b3-115">Créer un cache Redis Premium avec un réseau virtuel et le clustering facultatif</span><span class="sxs-lookup"><span data-stu-id="567b3-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="567b3-116">toocheck pour les derniers modèles de hello, consultez [modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/) et recherchez `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="567b3-116">toocheck for hello latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="567b3-117">Ce que vous allez déployer</span><span class="sxs-lookup"><span data-stu-id="567b3-117">What you will deploy</span></span>
<span data-ttu-id="567b3-118">Dans ce modèle, vous allez déployer un cache Redis Azure qui utilise un compte de stockage existant pour les données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="567b3-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="567b3-119">toorun hello déploiement automatiquement, cliquez sur hello suivant bouton :</span><span class="sxs-lookup"><span data-stu-id="567b3-119">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="567b3-120">[![Déployer tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="567b3-120">[![Deploy tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="567b3-121">Paramètres</span><span class="sxs-lookup"><span data-stu-id="567b3-121">Parameters</span></span>
<span data-ttu-id="567b3-122">Avec Azure Resource Manager, vous définissez des paramètres pour les valeurs souhaitées toospecify lorsque le modèle de hello est déployé.</span><span class="sxs-lookup"><span data-stu-id="567b3-122">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="567b3-123">modèle de Hello inclut une section appelée paramètres qui contient toutes les valeurs de paramètre hello.</span><span class="sxs-lookup"><span data-stu-id="567b3-123">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="567b3-124">Vous devez définir un paramètre pour les valeurs qui varient en fonction de projet que vous déployez hello ou dans l’environnement hello que vous effectuez le déploiement.</span><span class="sxs-lookup"><span data-stu-id="567b3-124">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="567b3-125">Ne définissez pas de paramètres pour les valeurs qui doivent restent hello identiques.</span><span class="sxs-lookup"><span data-stu-id="567b3-125">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="567b3-126">Chaque valeur de paramètre est utilisé dans hello modèle toodefine hello ressources qui sont déployés.</span><span class="sxs-lookup"><span data-stu-id="567b3-126">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="567b3-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="567b3-127">redisCacheLocation</span></span>
<span data-ttu-id="567b3-128">emplacement Hello Hello du Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="567b3-128">hello location of hello Redis Cache.</span></span> <span data-ttu-id="567b3-129">Pour de meilleures performances, utilisez hello même emplacement que hello toobe application utilisé avec le cache de hello.</span><span class="sxs-lookup"><span data-stu-id="567b3-129">For best performance, use hello same location as hello app toobe used with hello cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="567b3-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="567b3-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="567b3-131">nom de Hello de hello toouse du compte stockage existant pour les diagnostics.</span><span class="sxs-lookup"><span data-stu-id="567b3-131">hello name of hello existing storage account toouse for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="567b3-132">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="567b3-132">enableNonSslPort</span></span>
<span data-ttu-id="567b3-133">Valeur booléenne qui indique si tooallow accéder via les ports non-SSL.</span><span class="sxs-lookup"><span data-stu-id="567b3-133">A boolean value that indicates whether tooallow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="567b3-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="567b3-134">diagnosticsStatus</span></span>
<span data-ttu-id="567b3-135">Valeur qui indique si les diagnostics sont activés.</span><span class="sxs-lookup"><span data-stu-id="567b3-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="567b3-136">Utilisez ON ou OFF.</span><span class="sxs-lookup"><span data-stu-id="567b3-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="567b3-137">Ressources toodeploy</span><span class="sxs-lookup"><span data-stu-id="567b3-137">Resources toodeploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="567b3-138">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="567b3-138">Redis Cache</span></span>
<span data-ttu-id="567b3-139">Crée hello du Cache Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="567b3-139">Creates hello Azure Redis Cache.</span></span>

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



## <a name="commands-toorun-deployment"></a><span data-ttu-id="567b3-140">Déploiement de toorun de commandes</span><span class="sxs-lookup"><span data-stu-id="567b3-140">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="567b3-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="567b3-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="567b3-142">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="567b3-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


