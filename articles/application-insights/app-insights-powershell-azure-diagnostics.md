---
title: aaaUsing PowerShell toosetup Application Insights dans Azure | Documents Microsoft
description: Automatiser la configuration des Diagnostics Azure de toopipe tooApplication Insights.
services: application-insights
documentationcenter: .net
author: sbtron
manager: carmonm
ms.assetid: 4ac803a8-f424-4c0c-b18f-4b9c189a64a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/17/2015
ms.author: bwren
ms.openlocfilehash: c48a5d8eb23df162522860935af876063aaa6976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="10506-103">À l’aide de tooset PowerShell d’Application Insights pour une application web Azure</span><span class="sxs-lookup"><span data-stu-id="10506-103">Using PowerShell tooset up Application Insights for an Azure web app</span></span>
<span data-ttu-id="10506-104">[Microsoft Azure](https://azure.com) peut être [de configurer les Diagnostics de Azure toosend](app-insights-azure-diagnostics.md) trop[Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10506-104">[Microsoft Azure](https://azure.com) can be [configured toosend Azure Diagnostics](app-insights-azure-diagnostics.md) too[Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="10506-105">diagnostics de Hello concernent tooAzure les Services de cloud computing et machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="10506-105">hello diagnostics relate tooAzure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="10506-106">Ils permettent de compléter que vous envoyez à partir d’application hello hello Application Insights SDK à l’aide de la télémétrie hello.</span><span class="sxs-lookup"><span data-stu-id="10506-106">They complement hello telemetry that you send from within hello app using hello Application Insights SDK.</span></span> <span data-ttu-id="10506-107">Dans le cadre de l’automatisation des processus hello de création de nouvelles ressources dans Azure, vous pouvez configurer les diagnostics à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="10506-107">As part of automating hello process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="10506-108">Modèle Azure</span><span class="sxs-lookup"><span data-stu-id="10506-108">Azure template</span></span>
<span data-ttu-id="10506-109">Si l’application web hello est dans Azure et créez vos ressources à l’aide d’un modèle Azure Resource Manager, vous pouvez configurer Application Insights en ajoutant ce nœud de ressources toohello :</span><span class="sxs-lookup"><span data-stu-id="10506-109">If hello web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this toohello resources node:</span></span>

    {
      resources: [
        /* Create Application Insights resource */
        {
          "apiVersion": "2015-05-01",
          "type": "microsoft.insights/components",
          "name": "nameOfAIAppResource",
          "location": "centralus",
          "kind": "web",
          "properties": { "ApplicationId": "nameOfAIAppResource" },
          "dependsOn": [
            "[concat('Microsoft.Web/sites/', myWebAppName)]"
          ]
        }
       ]
     } 

* <span data-ttu-id="10506-110">`nameOfAIAppResource`-nom de hello ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="10506-110">`nameOfAIAppResource` - a name for hello Application Insights resource</span></span>
* <span data-ttu-id="10506-111">`myWebAppName`-id hello de hello web app</span><span class="sxs-lookup"><span data-stu-id="10506-111">`myWebAppName` - hello id of hello web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="10506-112">Activer l’extension de diagnostics lors du déploiement d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="10506-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="10506-113">Hello `New-AzureDeployment` applet de commande a un paramètre `ExtensionConfiguration`, qui accepte un tableau de configurations de diagnostics.</span><span class="sxs-lookup"><span data-stu-id="10506-113">hello `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="10506-114">Ils peuvent être créés à l’aide de hello `New-AzureServiceDiagnosticsExtensionConfig` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="10506-114">These can be created using hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="10506-115">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="10506-115">For example:</span></span>

```ps

    $service_package = "CloudService.cspkg"
    $service_config = "ServiceConfiguration.Cloud.cscfg"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

    $primary_storagekey = (Get-AzureStorageKey `
     -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
       -StorageAccountName $diagnostics_storagename `
       -StorageAccountKey $primary_storagekey

    $webrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WebRole" -Storage_context $storageContext `
      -DiagnosticsConfigurationPath $webrole_diagconfigpath
    $workerrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WorkerRole" `
      -StorageContext $storage_context `
      -DiagnosticsConfigurationPath $workerrole_diagconfigpath

    New-AzureDeployment `
      -ServiceName $service_name `
      -Slot Production `
      -Package $service_package `
      -Configuration $service_config `
      -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)

``` 

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="10506-116">Activer l’extension de diagnostics sur un service cloud existant</span><span class="sxs-lookup"><span data-stu-id="10506-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="10506-117">Sur un service existant, utilisez `Set-AzureServiceDiagnosticsExtension`.</span><span class="sxs-lookup"><span data-stu-id="10506-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

```ps

    $service_name = "MyService"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"
    $primary_storagekey = (Get-AzureStorageKey `
         -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
        -StorageAccountName $diagnostics_storagename `
        -StorageAccountKey $primary_storagekey

    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $webrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WebRole" 
    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $workerrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WorkerRole"
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="10506-118">Obtenir la configuration actuelle de l’extension de diagnostics</span><span class="sxs-lookup"><span data-stu-id="10506-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="10506-119">Supprimer l’extension de diagnostics</span><span class="sxs-lookup"><span data-stu-id="10506-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="10506-120">Si vous avez activé l’extension à l’aide des diagnostics hello `Set-AzureServiceDiagnosticsExtension` ou `New-AzureServiceDiagnosticsExtensionConfig` sans paramètre de rôle hello, vous pouvez ensuite supprimer à l’aide d’extension hello `Remove-AzureServiceDiagnosticsExtension` sans paramètre de rôle hello.</span><span class="sxs-lookup"><span data-stu-id="10506-120">If you enabled hello diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without hello Role parameter, then you can remove hello extension using `Remove-AzureServiceDiagnosticsExtension` without hello Role parameter.</span></span> <span data-ttu-id="10506-121">Si le paramètre de rôle hello utilisé lors de l’activation de l’extension de hello puis il doit également être utilisé lors de la suppression d’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="10506-121">If hello Role parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="10506-122">extension des diagnostics hello tooremove à partir de chaque rôle individuel :</span><span class="sxs-lookup"><span data-stu-id="10506-122">tooremove hello diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="10506-123">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="10506-123">See also</span></span>
* [<span data-ttu-id="10506-124">Surveiller les applications Azure Cloud Services avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="10506-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="10506-125">Envoyer des Diagnostics Windows Azure tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="10506-125">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="10506-126">Automatisation de la configuration des alertes</span><span class="sxs-lookup"><span data-stu-id="10506-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

