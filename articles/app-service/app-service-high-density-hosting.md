---
title: "Hébergement haute densité sur Azure App Service | Microsoft Docs"
description: "Hébergement haute densité sur Azure App Service"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: a903cb78-4927-47b0-8427-56412c4e3e64
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: byvinyal
ms.openlocfilehash: 459a310a719695f6366470976d857ec2f9d6f4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="eb796-103">Hébergement haute densité sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="eb796-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="eb796-104">Lorsque vous utilisez App Service, votre application est découplée à partir de la capacité allouée par deux concepts :</span><span class="sxs-lookup"><span data-stu-id="eb796-104">When using App Service, your application is decoupled from the capacity allocated to it by two concepts:</span></span>

* <span data-ttu-id="eb796-105">**L’Application :** représente l’application et sa configuration lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="eb796-105">**The Application:** Represents the app and its runtime configuration.</span></span> <span data-ttu-id="eb796-106">Par exemple, elle inclut la version de .NET que le runtime doit charger, les paramètres de l’application, etc.</span><span class="sxs-lookup"><span data-stu-id="eb796-106">For example, it includes the version of .NET that the runtime should load, the app settings.</span></span>
* <span data-ttu-id="eb796-107">**Le plan App Service :** définit les caractéristiques de capacité, l’ensemble des fonctionnalités disponibles et la localité de l’application.</span><span class="sxs-lookup"><span data-stu-id="eb796-107">**The App Service Plan:** Defines the characteristics of the capacity, available feature set, and locality of the application.</span></span> <span data-ttu-id="eb796-108">Par exemple, les caractéristiques peuvent être : machines puissantes (quatre cœurs), quatre instances, fonctionnalités Premium pour les États-Unis de l’Est.</span><span class="sxs-lookup"><span data-stu-id="eb796-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="eb796-109">Une application est toujours liée à un plan App Service, mais un Plan App Service peut fournir de la capacité à une ou plusieurs applications.</span><span class="sxs-lookup"><span data-stu-id="eb796-109">An app is always linked to an App Service plan, but an App Service plan can provide capacity to one or more apps.</span></span>

<span data-ttu-id="eb796-110">Par conséquent, la plateforme fournit la flexibilité nécessaire pour isoler une application unique, ou partager les ressources entre plusieurs applications avec un plan App Service commun.</span><span class="sxs-lookup"><span data-stu-id="eb796-110">As a result, the platform provides the flexibility to isolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="eb796-111">Toutefois, lorsque plusieurs applications partagent un plan App Service, une instance de cette application sera exécutée sur chaque instance de ce plan App Service.</span><span class="sxs-lookup"><span data-stu-id="eb796-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="eb796-112">Mise à l’échelle par application</span><span class="sxs-lookup"><span data-stu-id="eb796-112">Per app scaling</span></span>
<span data-ttu-id="eb796-113">*La mise à l’échelle par application* est une fonction qui peut être activée au niveau du plan App Service et activée par chaque application.</span><span class="sxs-lookup"><span data-stu-id="eb796-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="eb796-114">La mise à l’échelle par application permet de mettre à l’échelle une application indépendamment du plan App Service qui l’héberge.</span><span class="sxs-lookup"><span data-stu-id="eb796-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="eb796-115">De cette manière, un plan App Service peut passer à 10 instances, mais une application peut être définie de manière à n’en utiliser que cinq.</span><span class="sxs-lookup"><span data-stu-id="eb796-115">This way, an App Service plan can be scaled to 10 instances, but an app can be set to use only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="eb796-116">La mise à l’échelle par application est disponible uniquement pour les plans App Service **Premium** de référence</span><span class="sxs-lookup"><span data-stu-id="eb796-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="eb796-117">Mise à l’échelle par application à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="eb796-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="eb796-118">Vous pouvez créer un plan configuré comme plan de *mise à l’échelle par application* en passant l’attribut ```-perSiteScaling $true``` dans l’applet de commande ```New-AzureRmAppServicePlan```.</span><span class="sxs-lookup"><span data-stu-id="eb796-118">You can create a plan configured as a *Per app scaling* plan by passing in the ```-perSiteScaling $true``` attribute to the ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="eb796-119">Si vous souhaitez mettre à jour un plan App Service existant pour utiliser cette fonctionnalité :</span><span class="sxs-lookup"><span data-stu-id="eb796-119">If you want to update an existing App Service plan to use this feature:</span></span> 

- <span data-ttu-id="eb796-120">Obtenez le plan cible ```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="eb796-120">get the target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="eb796-121">Modifiez la propriété localement ```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="eb796-121">modifying the property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="eb796-122">Validez les modifications vers Azure ```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="eb796-122">posting your changes back to azure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get the new App Service Plan and modify the "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify the local copy to use "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back to azure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="eb796-123">Au niveau de l’application, nous devons configurer le nombre d’instances que l’application peut utiliser dans le plan App Service.</span><span class="sxs-lookup"><span data-stu-id="eb796-123">At the app level, we need to configure the number of instances the app can use in the app service plan.</span></span>

<span data-ttu-id="eb796-124">Dans l’exemple ci-dessous, l’application est limitée à deux instances quel que soit le nombre d’instances mis à l’échelle pour le plan App Service sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="eb796-124">In the example below, the app is limited to two instances regardless of how many instances the underlying app service plan scales out to.</span></span>

```
# Get the app we want to configure to use "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify the NumberOfWorkers setting to the desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back to azure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="eb796-125">$newapp.SiteConfig.NumberOfWorkers est différent de $newapp.MaxNumberOfWorkers.</span><span class="sxs-lookup"><span data-stu-id="eb796-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="eb796-126">La mise à l’échelle par application utilise $newapp. SiteConfig.NumberOfWorkers pour déterminer les caractéristiques de mise à l’échelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="eb796-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers to determine the scale characteristics of the app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="eb796-127">Mise à l’échelle par application avec Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="eb796-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="eb796-128">Le *modèle Azure Resource Manager* ci-dessous crée les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="eb796-128">The following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="eb796-129">Un plan App Service réparti sur 10 instances</span><span class="sxs-lookup"><span data-stu-id="eb796-129">An App Service plan that's scaled out to 10 instances</span></span>
- <span data-ttu-id="eb796-130">Une application configurée pour une mise à l’échelle vers un maximum de cinq instances.</span><span class="sxs-lookup"><span data-stu-id="eb796-130">an app that's configured to scale to a max of five instances.</span></span>

<span data-ttu-id="eb796-131">Le plan App Service définit la propriété **PerSiteScaling** sur true ```"perSiteScaling": true```.</span><span class="sxs-lookup"><span data-stu-id="eb796-131">The App Service plan is setting the **PerSiteScaling** property to true ```"perSiteScaling": true```.</span></span> <span data-ttu-id="eb796-132">L’application définit le **nombre de Workers** à utiliser sur 5 ```"properties": { "numberOfWorkers": "5" }```.</span><span class="sxs-lookup"><span data-stu-id="eb796-132">The app is setting the **number of workers** to use to 5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

```
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters":{
        "appServicePlanName": { "type": "string" },
        "appName": { "type": "string" }
        },
    "resources": [
    {
        "comments": "App Service Plan with per site perSiteScaling = true",
        "type": "Microsoft.Web/serverFarms",
        "sku": {
            "name": "P1",
            "tier": "Premium",
            "size": "P1",
            "family": "P",
            "capacity": 10
            },
        "name": "[parameters('appServicePlanName')]",
        "apiVersion": "2015-08-01",
        "location": "West US",
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "perSiteScaling": true
        }
    },
    {
        "type": "Microsoft.Web/sites",
        "name": "[parameters('appName')]",
        "apiVersion": "2015-08-01-preview",
        "location": "West US",
        "dependsOn": [ "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" ],
        "properties": { "serverFarmId": "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" },
        "resources": [ {
                "comments": "",
                "type": "config",
                "name": "web",
                "apiVersion": "2015-08-01",
                "location": "West US",
                "dependsOn": [ "[resourceId('Microsoft.Web/Sites', parameters('appName'))]" ],
                "properties": { "numberOfWorkers": "5" }
            } ]
        }]
}
```

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="eb796-133">Configuration recommandée pour l’hébergement haute densité</span><span class="sxs-lookup"><span data-stu-id="eb796-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="eb796-134">La fonctionnalité de mise à l’échelle par application est activée dans les régions Azure et les environnements App Service globaux.</span><span class="sxs-lookup"><span data-stu-id="eb796-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="eb796-135">Toutefois, la stratégie recommandée consiste à utiliser des environnements App Service pour tirer parti de leurs fonctionnalités avancées et des pools de capacité supérieure.</span><span class="sxs-lookup"><span data-stu-id="eb796-135">However, the recommended strategy is to use App Service Environments to take advantage of their advanced features and the larger pools of capacity.</span></span>  

<span data-ttu-id="eb796-136">Suivez ces étapes pour configurer un hébergement haute densité pour vos applications :</span><span class="sxs-lookup"><span data-stu-id="eb796-136">Follow these steps to configure high density hosting for your apps:</span></span>

1. <span data-ttu-id="eb796-137">Configurez l’environnement App Service et choisissez un pool de Workers consacré au scénario d’hébergement haute densité.</span><span class="sxs-lookup"><span data-stu-id="eb796-137">Configure the App Service Environment and choose a worker pool that is dedicated to the high density hosting scenario.</span></span>
1. <span data-ttu-id="eb796-138">Créez un seul plan App Service et mettez-le à l’échelle pour utiliser toute la capacité disponible sur le pool de Workers.</span><span class="sxs-lookup"><span data-stu-id="eb796-138">Create a single App Service plan, and scale it to use all the available capacity on the worker pool.</span></span>
1. <span data-ttu-id="eb796-139">Définissez l’indicateur PerSiteScaling sur true dans le plan App Service.</span><span class="sxs-lookup"><span data-stu-id="eb796-139">Set the PerSiteScaling flag to true on the App Service plan.</span></span>
1. <span data-ttu-id="eb796-140">Les nouvelles applications sont créées et attribuées à ce plan App Service avec la propriété **numberOfWorkers** définie sur **1**.</span><span class="sxs-lookup"><span data-stu-id="eb796-140">New apps are created and assigned to that App Service plan with the **numberOfWorkers** property set to **1**.</span></span> <span data-ttu-id="eb796-141">Cela donne la densité la plus élevée possible sur ce pool de Workers.</span><span class="sxs-lookup"><span data-stu-id="eb796-141">Using this configuration yields the highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="eb796-142">Le nombre de Workers peut être configuré indépendamment par application pour accorder des ressources supplémentaires en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="eb796-142">The number of workers can be configured independently per app to grant additional resources as needed.</span></span> <span data-ttu-id="eb796-143">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eb796-143">For example:</span></span>
    - <span data-ttu-id="eb796-144">Une application à haut niveau d’utilisation peut définir **numberOfWorkers** sur **3** pour accroître la capacité de traitement de cette application.</span><span class="sxs-lookup"><span data-stu-id="eb796-144">A high-use app can set **numberOfWorkers** to **3** to have more processing capacity for that app.</span></span> 
    - <span data-ttu-id="eb796-145">Les applications à faible niveau d’utilisation définiraient **numberOfWorkers** sur **1**.</span><span class="sxs-lookup"><span data-stu-id="eb796-145">Low-use apps would set **numberOfWorkers** to **1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb796-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eb796-146">Next Steps</span></span>

- [<span data-ttu-id="eb796-147">Présentation détaillée des plans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="eb796-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="eb796-148">Présentation de l'environnement App Service</span><span class="sxs-lookup"><span data-stu-id="eb796-148">Introduction to App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)