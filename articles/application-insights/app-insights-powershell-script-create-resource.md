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
# <a name="powershell-script-toocreate-an-application-insights-resource"></a><span data-ttu-id="e0f81-103">Toocreate de script PowerShell une ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="e0f81-103">PowerShell script toocreate an Application Insights resource</span></span>


<span data-ttu-id="e0f81-104">Lorsque vous souhaitez toomonitor une nouvelle application - ou une nouvelle version d’une application - avec [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), vous définissez une nouvelle ressource dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e0f81-104">When you want toomonitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="e0f81-105">Cette ressource est où les données de télémétrie hello à partir de votre application sont analysées et affichées.</span><span class="sxs-lookup"><span data-stu-id="e0f81-105">This resource is where hello telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="e0f81-106">Vous pouvez automatiser la création d’une nouvelle ressource hello à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0f81-106">You can automate hello creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="e0f81-107">Par exemple, si vous développez une application pour appareil mobile, il est probable qu’à tout moment, plusieurs versions publiées de votre application soient utilisées par vos clients.</span><span class="sxs-lookup"><span data-stu-id="e0f81-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="e0f81-108">Vous ne voulez pas résultats de télémétrie hello tooget à partir de différentes versions confondues.</span><span class="sxs-lookup"><span data-stu-id="e0f81-108">You don't want tooget hello telemetry results from different versions mixed up.</span></span> <span data-ttu-id="e0f81-109">Par conséquent, vous obtenez votre toocreate de processus de génération une ressource pour chaque build.</span><span class="sxs-lookup"><span data-stu-id="e0f81-109">So you get your build process toocreate a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="e0f81-110">Si vous voulez toocreate un ensemble de ressources en hello même temps, envisagez de [création de ressources hello à l’aide d’un modèle Azure](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e0f81-110">If you want toocreate a set of resources all at hello same time, consider [creating hello resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a><span data-ttu-id="e0f81-111">Script toocreate une ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="e0f81-111">Script toocreate an Application Insights resource</span></span>
<span data-ttu-id="e0f81-112">Consultez les spécifications d’applet de commande appropriée de hello :</span><span class="sxs-lookup"><span data-stu-id="e0f81-112">See hello relevant cmdlet specs:</span></span>

* [<span data-ttu-id="e0f81-113">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="e0f81-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="e0f81-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="e0f81-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="e0f81-115">*Script PowerShell*</span><span class="sxs-lookup"><span data-stu-id="e0f81-115">*PowerShell Script*</span></span>  

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

## <a name="what-toodo-with-hello-ikey"></a><span data-ttu-id="e0f81-116">Quelles toodo avec hello iKey</span><span class="sxs-lookup"><span data-stu-id="e0f81-116">What toodo with hello iKey</span></span>
<span data-ttu-id="e0f81-117">Chaque ressource est identifiée par sa clé d’instrumentation (iKey).</span><span class="sxs-lookup"><span data-stu-id="e0f81-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="e0f81-118">Hello iKey est une sortie du script de création de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="e0f81-118">hello iKey is an output of hello resource creation script.</span></span> <span data-ttu-id="e0f81-119">Votre script de compilation doit fournir toohello d’iKey hello Qu'application Insights SDK incorporé dans votre application.</span><span class="sxs-lookup"><span data-stu-id="e0f81-119">Your build script should provide hello iKey toohello Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="e0f81-120">Il existe deux façons toomake hello iKey disponible toohello SDK :</span><span class="sxs-lookup"><span data-stu-id="e0f81-120">There are two ways toomake hello iKey available toohello SDK:</span></span>

* <span data-ttu-id="e0f81-121">Dans [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="e0f81-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="e0f81-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="e0f81-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="e0f81-123">Ou dans le [code d’initialisation](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="e0f81-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="e0f81-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="e0f81-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="e0f81-125">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="e0f81-125">See also</span></span>
* [<span data-ttu-id="e0f81-126">Créer des ressources Application Insights et de test Web  templates à partir de modèles (en anglais)</span><span class="sxs-lookup"><span data-stu-id="e0f81-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="e0f81-127">Configurer la surveillance de diagnostics Azure avec PowerShell (en anglais</span><span class="sxs-lookup"><span data-stu-id="e0f81-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="e0f81-128">Définition d’alertes à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0f81-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

