---
title: Utilisation de PowerShell pour configurer Application Insights pour une application web Azure | Microsoft Docs
description: "Automatiser la configuration d’Azure Diagnostics pour envoyer des données vers Application Insights"
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
ms.openlocfilehash: 3b6da89cc33cda713b483a2af3cbb493a03d6bec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="using-powershell-to-set-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="eaaea-103">Utilisation de PowerShell pour configurer Application Insights pour une application web Azure</span><span class="sxs-lookup"><span data-stu-id="eaaea-103">Using PowerShell to set up Application Insights for an Azure web app</span></span>
<span data-ttu-id="eaaea-104">[Microsoft Azure](https://azure.com) peut être [configuré pour envoyer des Diagnostics Azure](app-insights-azure-diagnostics.md) vers [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eaaea-104">[Microsoft Azure](https://azure.com) can be [configured to send Azure Diagnostics](app-insights-azure-diagnostics.md) to [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="eaaea-105">Les tests de diagnostic concernent Azure Cloud Services et les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="eaaea-105">The diagnostics relate to Azure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="eaaea-106">Ils permettent de compléter les données de télémétrie que vous envoyez depuis l’application à l’aide du kit de développement logiciel d’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="eaaea-106">They complement the telemetry that you send from within the app using the Application Insights SDK.</span></span> <span data-ttu-id="eaaea-107">Dans le cadre de l’automatisation du processus de création de nouvelles ressources dans Azure, vous pouvez configurer des diagnostics avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eaaea-107">As part of automating the process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="eaaea-108">Modèle Azure</span><span class="sxs-lookup"><span data-stu-id="eaaea-108">Azure template</span></span>
<span data-ttu-id="eaaea-109">Si l’application web est dans Azure et que vous créez vos ressources à l’aide d’un modèle Azure Resource Manager, vous pouvez configurer Application Insights en ajoutant cela au nœud de ressources :</span><span class="sxs-lookup"><span data-stu-id="eaaea-109">If the web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this to the resources node:</span></span>

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

* <span data-ttu-id="eaaea-110">`nameOfAIAppResource` : nom de la ressource Application Insights</span><span class="sxs-lookup"><span data-stu-id="eaaea-110">`nameOfAIAppResource` - a name for the Application Insights resource</span></span>
* <span data-ttu-id="eaaea-111">`myWebAppName` : ID de l’application web</span><span class="sxs-lookup"><span data-stu-id="eaaea-111">`myWebAppName` - the id of the web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="eaaea-112">Activer l’extension de diagnostics lors du déploiement d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="eaaea-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="eaaea-113">L’applet de commande `New-AzureDeployment` comporte un paramètre `ExtensionConfiguration` qui utilise un tableau de configurations de diagnostics.</span><span class="sxs-lookup"><span data-stu-id="eaaea-113">The `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="eaaea-114">Ces derniers peuvent être créés à l’aide de l’applet de commande `New-AzureServiceDiagnosticsExtensionConfig` .</span><span class="sxs-lookup"><span data-stu-id="eaaea-114">These can be created using the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="eaaea-115">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eaaea-115">For example:</span></span>

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="eaaea-116">Activer l’extension de diagnostics sur un service cloud existant</span><span class="sxs-lookup"><span data-stu-id="eaaea-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="eaaea-117">Sur un service existant, utilisez `Set-AzureServiceDiagnosticsExtension`.</span><span class="sxs-lookup"><span data-stu-id="eaaea-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

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

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="eaaea-118">Obtenir la configuration actuelle de l’extension de diagnostics</span><span class="sxs-lookup"><span data-stu-id="eaaea-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="eaaea-119">Supprimer l’extension de diagnostics</span><span class="sxs-lookup"><span data-stu-id="eaaea-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="eaaea-120">Si vous avez activé l’extension des diagnostics à l’aide de `Set-AzureServiceDiagnosticsExtension` ou de `New-AzureServiceDiagnosticsExtensionConfig` sans paramètre Rôle. Vous pouvez ensuite supprimer l’extension à l’aide de `Remove-AzureServiceDiagnosticsExtension` sans paramètre Rôle.</span><span class="sxs-lookup"><span data-stu-id="eaaea-120">If you enabled the diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without the Role parameter, then you can remove the extension using `Remove-AzureServiceDiagnosticsExtension` without the Role parameter.</span></span> <span data-ttu-id="eaaea-121">Si le paramètre Rôle a été utilisé lors de l’activation de l’extension, il doit également être utilisé au moment de sa suppression.</span><span class="sxs-lookup"><span data-stu-id="eaaea-121">If the Role parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="eaaea-122">Pour supprimer l’extension de diagnostics de chaque rôle individuel :</span><span class="sxs-lookup"><span data-stu-id="eaaea-122">To remove the diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="eaaea-123">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="eaaea-123">See also</span></span>
* [<span data-ttu-id="eaaea-124">Surveiller les applications Azure Cloud Services avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="eaaea-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="eaaea-125">Envoyer des diagnostics Azure vers Application Insights.</span><span class="sxs-lookup"><span data-stu-id="eaaea-125">Send Azure Diagnostics to Application Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="eaaea-126">Automatisation de la configuration des alertes</span><span class="sxs-lookup"><span data-stu-id="eaaea-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

