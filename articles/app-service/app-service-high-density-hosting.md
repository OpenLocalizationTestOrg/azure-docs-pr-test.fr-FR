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
# <a name="high-density-hosting-on-azure-app-service"></a>Hébergement haute densité sur Azure App Service
Lors de l’utilisation du Service d’applications, votre application est dissociée de la capacité de hello allouée tooit par deux concepts :

* **Hello Application :** représente une application hello et sa configuration d’exécution. Par exemple, il inclut hello version de .NET qui hello runtime doit charger, paramètres de l’application hello.
* **Hello du Plan App Service :** définit les caractéristiques de hello de capacité de hello, l’ensemble des fonctionnalités disponibles et localité de l’application hello. Par exemple, les caractéristiques peuvent être : machines puissantes (quatre cœurs), quatre instances, fonctionnalités Premium pour les États-Unis de l’Est.

Une application est toujours lié tooan plan App Service, mais un plan App Service peut fournir tooone de capacité ou de plusieurs applications.

Par conséquent, plateforme de hello fournit hello flexibilité tooisolate une seule application ou avoir plusieurs applications de partager des ressources à un plan App Service de partage.

Toutefois, lorsque plusieurs applications partagent un plan App Service, une instance de cette application sera exécutée sur chaque instance de ce plan App Service.

## <a name="per-app-scaling"></a>Mise à l’échelle par application
*La mise à l’échelle par application* est une fonction qui peut être activée au niveau du plan App Service et activée par chaque application.

La mise à l’échelle par application permet de mettre à l’échelle une application indépendamment du plan App Service qui l’héberge. De cette manière, le plan peut être un Service d’application à l’échelle too10 instances, mais une application peut être définie toouse que cinq.

   >[!NOTE]
   >La mise à l’échelle par application est disponible uniquement pour les plans App Service **Premium** de référence
   >

### <a name="per-app-scaling-using-powershell"></a>Mise à l’échelle par application à l’aide de PowerShell

Vous pouvez créer un plan configuré comme un *par la mise à l’échelle de l’application* plan en passant hello ```-perSiteScaling $true``` attribut toohello ```New-AzureRmAppServicePlan``` applet de commande

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

Si vous voulez tooupdate un Service d’application existant plan toouse cette fonctionnalité : 

- obtenir le plan cible de hello```Get-AzureRmAppServicePlan```
- modification de propriété hello localement```$newASP.PerSiteScaling = $true```
- validation de votre tooazure arrière de modifications```Set-AzureRmAppServicePlan``` 

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

Au niveau d’application hello, nous devons nombre de hello tooconfigure d’instances d’application hello peut utiliser dans le plan de service d’application hello.

Dans l’exemple hello ci-dessous, application hello est instances tootwo limitée, quelle que soit le nombre d’instances hello sous-jacent app service plan échelles out à.

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> $newapp.SiteConfig.NumberOfWorkers est différent de $newapp.MaxNumberOfWorkers. Par application mise à l’échelle utilise $newapp. Caractéristiques de mise à l’échelle hello SiteConfig.NumberOfWorkers toodetermine de l’application hello.

### <a name="per-app-scaling-using-azure-resource-manager"></a>Mise à l’échelle par application avec Azure Resource Manager

suivant de Hello *modèle Azure Resource Manager* crée :

- Un plan de Service d’applications est mis à l’échelle des instances de too10
- une application qui a configuré tooscale tooa maximum cinq instances.

Hello plan App Service est paramètre hello **PerSiteScaling** propriété tootrue ```"perSiteScaling": true```. application Hello est paramètre hello **nombre de travailleurs** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.

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

## <a name="recommended-configuration-for-high-density-hosting"></a>Configuration recommandée pour l’hébergement haute densité
La fonctionnalité de mise à l’échelle par application est activée dans les régions Azure et les environnements App Service globaux. Toutefois, hello recommandé stratégie consiste à utiliser parti de tootake les environnements App Service de leurs fonctionnalités avancées et des pools plus volumineux de hello de capacité.  

Suivez ces étapes tooconfigure haute densité d’hébergement pour vos applications :

1. Configurer l’environnement App Service de hello et choisissez un pool de travail qui est dédié toohello haute densité scénario d’hébergement.
1. Créer un plan de Service d’applications unique et mettre à l’échelle toouse tous hello capacité disponible dans le pool de travail hello.
1. Définir hello PerSiteScaling indicateur tootrue sur hello plan App Service.
1. De nouvelles applications sont créées et affectées toothat le plan App Service avec le **numberOfWorkers** propriété trop**1**. À l’aide de cette configuration génère hello plus grande densité possible sur ce pool de travail.
1. le nombre de traitements Hello peut être configuré indépendamment par des ressources application toogrant supplémentaires en fonction des besoins. Par exemple :
    - Une application forte utilisation peut définir **numberOfWorkers** trop**3** toohave plus la capacité pour cette application de traitement. 
    - Applications de faible utilisation définiriez **numberOfWorkers** trop**1**.

## <a name="next-steps"></a>Étapes suivantes

- [Présentation détaillée des plans Azure App Service](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [Introduction tooApp environnement de Service](../app-service-web/app-service-app-service-environment-intro.md)
