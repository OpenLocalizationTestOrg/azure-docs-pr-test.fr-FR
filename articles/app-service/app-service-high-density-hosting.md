---
title: "hébergement de densité aaaHigh sur Azure App Service | Documents Microsoft"
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
ms.openlocfilehash: a10cb81ace13ba6992b572a44361061ecf72b266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="6b868-103">Hébergement haute densité sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6b868-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="6b868-104">Lors de l’utilisation du Service d’applications, votre application est dissociée de la capacité de hello allouée tooit par deux concepts :</span><span class="sxs-lookup"><span data-stu-id="6b868-104">When using App Service, your application is decoupled from hello capacity allocated tooit by two concepts:</span></span>

* <span data-ttu-id="6b868-105">**Hello Application :** représente une application hello et sa configuration d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6b868-105">**hello Application:** Represents hello app and its runtime configuration.</span></span> <span data-ttu-id="6b868-106">Par exemple, il inclut hello version de .NET qui hello runtime doit charger, paramètres de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6b868-106">For example, it includes hello version of .NET that hello runtime should load, hello app settings.</span></span>
* <span data-ttu-id="6b868-107">**Hello du Plan App Service :** définit les caractéristiques de hello de capacité de hello, l’ensemble des fonctionnalités disponibles et localité de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6b868-107">**hello App Service Plan:** Defines hello characteristics of hello capacity, available feature set, and locality of hello application.</span></span> <span data-ttu-id="6b868-108">Par exemple, les caractéristiques peuvent être : machines puissantes (quatre cœurs), quatre instances, fonctionnalités Premium pour les États-Unis de l’Est.</span><span class="sxs-lookup"><span data-stu-id="6b868-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="6b868-109">Une application est toujours lié tooan plan App Service, mais un plan App Service peut fournir tooone de capacité ou de plusieurs applications.</span><span class="sxs-lookup"><span data-stu-id="6b868-109">An app is always linked tooan App Service plan, but an App Service plan can provide capacity tooone or more apps.</span></span>

<span data-ttu-id="6b868-110">Par conséquent, plateforme de hello fournit hello flexibilité tooisolate une seule application ou avoir plusieurs applications de partager des ressources à un plan App Service de partage.</span><span class="sxs-lookup"><span data-stu-id="6b868-110">As a result, hello platform provides hello flexibility tooisolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="6b868-111">Toutefois, lorsque plusieurs applications partagent un plan App Service, une instance de cette application sera exécutée sur chaque instance de ce plan App Service.</span><span class="sxs-lookup"><span data-stu-id="6b868-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="6b868-112">Mise à l’échelle par application</span><span class="sxs-lookup"><span data-stu-id="6b868-112">Per app scaling</span></span>
<span data-ttu-id="6b868-113">*La mise à l’échelle par application* est une fonction qui peut être activée au niveau du plan App Service et activée par chaque application.</span><span class="sxs-lookup"><span data-stu-id="6b868-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="6b868-114">La mise à l’échelle par application permet de mettre à l’échelle une application indépendamment du plan App Service qui l’héberge.</span><span class="sxs-lookup"><span data-stu-id="6b868-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="6b868-115">De cette manière, le plan peut être un Service d’application à l’échelle too10 instances, mais une application peut être définie toouse que cinq.</span><span class="sxs-lookup"><span data-stu-id="6b868-115">This way, an App Service plan can be scaled too10 instances, but an app can be set toouse only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="6b868-116">La mise à l’échelle par application est disponible uniquement pour les plans App Service **Premium** de référence</span><span class="sxs-lookup"><span data-stu-id="6b868-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="6b868-117">Mise à l’échelle par application à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b868-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="6b868-118">Vous pouvez créer un plan configuré comme un *par la mise à l’échelle de l’application* plan en passant hello ```-perSiteScaling $true``` attribut toohello ```New-AzureRmAppServicePlan``` applet de commande</span><span class="sxs-lookup"><span data-stu-id="6b868-118">You can create a plan configured as a *Per app scaling* plan by passing in hello ```-perSiteScaling $true``` attribute toohello ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="6b868-119">Si vous voulez tooupdate un Service d’application existant plan toouse cette fonctionnalité :</span><span class="sxs-lookup"><span data-stu-id="6b868-119">If you want tooupdate an existing App Service plan toouse this feature:</span></span> 

- <span data-ttu-id="6b868-120">obtenir le plan cible de hello```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="6b868-120">get hello target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="6b868-121">modification de propriété hello localement```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="6b868-121">modifying hello property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="6b868-122">validation de votre tooazure arrière de modifications```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="6b868-122">posting your changes back tooazure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get hello new App Service Plan and modify hello "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify hello local copy toouse "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back tooazure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="6b868-123">Au niveau d’application hello, nous devons nombre de hello tooconfigure d’instances d’application hello peut utiliser dans le plan de service d’application hello.</span><span class="sxs-lookup"><span data-stu-id="6b868-123">At hello app level, we need tooconfigure hello number of instances hello app can use in hello app service plan.</span></span>

<span data-ttu-id="6b868-124">Dans l’exemple hello ci-dessous, application hello est instances tootwo limitée, quelle que soit le nombre d’instances hello sous-jacent app service plan échelles out à.</span><span class="sxs-lookup"><span data-stu-id="6b868-124">In hello example below, hello app is limited tootwo instances regardless of how many instances hello underlying app service plan scales out to.</span></span>

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="6b868-125">$newapp.SiteConfig.NumberOfWorkers est différent de $newapp.MaxNumberOfWorkers.</span><span class="sxs-lookup"><span data-stu-id="6b868-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="6b868-126">Par application mise à l’échelle utilise $newapp. Caractéristiques de mise à l’échelle hello SiteConfig.NumberOfWorkers toodetermine de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="6b868-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers toodetermine hello scale characteristics of hello app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="6b868-127">Mise à l’échelle par application avec Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6b868-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="6b868-128">suivant de Hello *modèle Azure Resource Manager* crée :</span><span class="sxs-lookup"><span data-stu-id="6b868-128">hello following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="6b868-129">Un plan de Service d’applications est mis à l’échelle des instances de too10</span><span class="sxs-lookup"><span data-stu-id="6b868-129">An App Service plan that's scaled out too10 instances</span></span>
- <span data-ttu-id="6b868-130">une application qui a configuré tooscale tooa maximum cinq instances.</span><span class="sxs-lookup"><span data-stu-id="6b868-130">an app that's configured tooscale tooa max of five instances.</span></span>

<span data-ttu-id="6b868-131">Hello plan App Service est paramètre hello **PerSiteScaling** propriété tootrue ```"perSiteScaling": true```.</span><span class="sxs-lookup"><span data-stu-id="6b868-131">hello App Service plan is setting hello **PerSiteScaling** property tootrue ```"perSiteScaling": true```.</span></span> <span data-ttu-id="6b868-132">application Hello est paramètre hello **nombre de travailleurs** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span><span class="sxs-lookup"><span data-stu-id="6b868-132">hello app is setting hello **number of workers** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

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

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="6b868-133">Configuration recommandée pour l’hébergement haute densité</span><span class="sxs-lookup"><span data-stu-id="6b868-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="6b868-134">La fonctionnalité de mise à l’échelle par application est activée dans les régions Azure et les environnements App Service globaux.</span><span class="sxs-lookup"><span data-stu-id="6b868-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="6b868-135">Toutefois, hello recommandé stratégie consiste à utiliser parti de tootake les environnements App Service de leurs fonctionnalités avancées et des pools plus volumineux de hello de capacité.</span><span class="sxs-lookup"><span data-stu-id="6b868-135">However, hello recommended strategy is to use App Service Environments tootake advantage of their advanced features and hello larger pools of capacity.</span></span>  

<span data-ttu-id="6b868-136">Suivez ces étapes tooconfigure haute densité d’hébergement pour vos applications :</span><span class="sxs-lookup"><span data-stu-id="6b868-136">Follow these steps tooconfigure high density hosting for your apps:</span></span>

1. <span data-ttu-id="6b868-137">Configurer l’environnement App Service de hello et choisissez un pool de travail qui est dédié toohello haute densité scénario d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="6b868-137">Configure hello App Service Environment and choose a worker pool that is dedicated toohello high density hosting scenario.</span></span>
1. <span data-ttu-id="6b868-138">Créer un plan de Service d’applications unique et mettre à l’échelle toouse tous hello capacité disponible dans le pool de travail hello.</span><span class="sxs-lookup"><span data-stu-id="6b868-138">Create a single App Service plan, and scale it toouse all hello available capacity on hello worker pool.</span></span>
1. <span data-ttu-id="6b868-139">Définir hello PerSiteScaling indicateur tootrue sur hello plan App Service.</span><span class="sxs-lookup"><span data-stu-id="6b868-139">Set hello PerSiteScaling flag tootrue on hello App Service plan.</span></span>
1. <span data-ttu-id="6b868-140">De nouvelles applications sont créées et affectées toothat le plan App Service avec le **numberOfWorkers** propriété trop**1**.</span><span class="sxs-lookup"><span data-stu-id="6b868-140">New apps are created and assigned toothat App Service plan with the **numberOfWorkers** property set too**1**.</span></span> <span data-ttu-id="6b868-141">À l’aide de cette configuration génère hello plus grande densité possible sur ce pool de travail.</span><span class="sxs-lookup"><span data-stu-id="6b868-141">Using this configuration yields hello highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="6b868-142">le nombre de traitements Hello peut être configuré indépendamment par des ressources application toogrant supplémentaires en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="6b868-142">hello number of workers can be configured independently per app toogrant additional resources as needed.</span></span> <span data-ttu-id="6b868-143">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6b868-143">For example:</span></span>
    - <span data-ttu-id="6b868-144">Une application forte utilisation peut définir **numberOfWorkers** trop**3** toohave plus la capacité pour cette application de traitement.</span><span class="sxs-lookup"><span data-stu-id="6b868-144">A high-use app can set **numberOfWorkers** too**3** toohave more processing capacity for that app.</span></span> 
    - <span data-ttu-id="6b868-145">Applications de faible utilisation définiriez **numberOfWorkers** trop**1**.</span><span class="sxs-lookup"><span data-stu-id="6b868-145">Low-use apps would set **numberOfWorkers** too**1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b868-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6b868-146">Next Steps</span></span>

- [<span data-ttu-id="6b868-147">Présentation détaillée des plans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6b868-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="6b868-148">Introduction tooApp environnement de Service</span><span class="sxs-lookup"><span data-stu-id="6b868-148">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
