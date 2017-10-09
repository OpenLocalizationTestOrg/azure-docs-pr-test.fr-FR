---
title: "script d’aaaPowerShell toocreate une ressource Application Insights | Documents Microsoft"
description: "Automatisez la création des ressources Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: f0082c9b-43ad-4576-a417-4ea8e0daf3d9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/19/2016
ms.author: bwren
ms.openlocfilehash: 2ac00376d38026d64c2c5deabfaca60588924510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-script-toocreate-an-application-insights-resource"></a>Toocreate de script PowerShell une ressource Application Insights


Lorsque vous souhaitez toomonitor une nouvelle application - ou une nouvelle version d’une application - avec [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), vous définissez une nouvelle ressource dans Microsoft Azure. Cette ressource est où les données de télémétrie hello à partir de votre application sont analysées et affichées. 

Vous pouvez automatiser la création d’une nouvelle ressource hello à l’aide de PowerShell.

Par exemple, si vous développez une application pour appareil mobile, il est probable qu’à tout moment, plusieurs versions publiées de votre application soient utilisées par vos clients. Vous ne voulez pas résultats de télémétrie hello tooget à partir de différentes versions confondues. Par conséquent, vous obtenez votre toocreate de processus de génération une ressource pour chaque build.

> [!NOTE]
> Si vous voulez toocreate un ensemble de ressources en hello même temps, envisagez de [création de ressources hello à l’aide d’un modèle Azure](app-insights-powershell.md).
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a>Script toocreate une ressource Application Insights
Consultez les spécifications d’applet de commande appropriée de hello :

* [New-AzureRmResource](https://msdn.microsoft.com/library/mt652510.aspx)
* [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt678995.aspx)

*Script PowerShell*  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before hello first 
# execution toologin toohello Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set hello name of hello Application Insights Resource

$appInsightsName = "TestApp"

# Set hello application name used for hello value of hello Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set hello name of hello Resource Group toouse.  
# Default is hello application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create hello Resource and Output hello name and iKey
###################################################

# Select hello azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create hello App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access toohello team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-toodo-with-hello-ikey"></a>Quelles toodo avec hello iKey
Chaque ressource est identifiée par sa clé d’instrumentation (iKey). Hello iKey est une sortie du script de création de ressources hello. Votre script de compilation doit fournir toohello d’iKey hello Qu'application Insights SDK incorporé dans votre application.

Il existe deux façons toomake hello iKey disponible toohello SDK :

* Dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md): 
  * `<instrumentationkey>`*ikey*`</instrumentationkey>`
* Ou dans le [code d’initialisation](app-insights-api-custom-events-metrics.md): 
  * `Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`

## <a name="see-also"></a>Voir aussi
* [Créer des ressources Application Insights et de test Web  templates à partir de modèles (en anglais)](app-insights-powershell.md)
* [Configurer la surveillance de diagnostics Azure avec PowerShell (en anglais](app-insights-powershell-azure-diagnostics.md) 
* [Définition d’alertes à l’aide de PowerShell](app-insights-powershell-alerts.md)

