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
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a>À l’aide de tooset PowerShell d’Application Insights pour une application web Azure
[Microsoft Azure](https://azure.com) peut être [de configurer les Diagnostics de Azure toosend](app-insights-azure-diagnostics.md) trop[Azure Application Insights](app-insights-overview.md). diagnostics de Hello concernent tooAzure les Services de cloud computing et machines virtuelles Azure. Ils permettent de compléter que vous envoyez à partir d’application hello hello Application Insights SDK à l’aide de la télémétrie hello. Dans le cadre de l’automatisation des processus hello de création de nouvelles ressources dans Azure, vous pouvez configurer les diagnostics à l’aide de PowerShell.

## <a name="azure-template"></a>Modèle Azure
Si l’application web hello est dans Azure et créez vos ressources à l’aide d’un modèle Azure Resource Manager, vous pouvez configurer Application Insights en ajoutant ce nœud de ressources toohello :

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

* `nameOfAIAppResource`-nom de hello ressource Application Insights
* `myWebAppName`-id hello de hello web app

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Activer l’extension de diagnostics lors du déploiement d’un service cloud
Hello `New-AzureDeployment` applet de commande a un paramètre `ExtensionConfiguration`, qui accepte un tableau de configurations de diagnostics. Ils peuvent être créés à l’aide de hello `New-AzureServiceDiagnosticsExtensionConfig` applet de commande. Par exemple :

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Activer l’extension de diagnostics sur un service cloud existant
Sur un service existant, utilisez `Set-AzureServiceDiagnosticsExtension`.

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

## <a name="get-current-diagnostics-extension-configuration"></a>Obtenir la configuration actuelle de l’extension de diagnostics
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a>Supprimer l’extension de diagnostics
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Si vous avez activé l’extension à l’aide des diagnostics hello `Set-AzureServiceDiagnosticsExtension` ou `New-AzureServiceDiagnosticsExtensionConfig` sans paramètre de rôle hello, vous pouvez ensuite supprimer à l’aide d’extension hello `Remove-AzureServiceDiagnosticsExtension` sans paramètre de rôle hello. Si le paramètre de rôle hello utilisé lors de l’activation de l’extension de hello puis il doit également être utilisé lors de la suppression d’extension de hello.

extension des diagnostics hello tooremove à partir de chaque rôle individuel :

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a>Voir aussi
* [Surveiller les applications Azure Cloud Services avec Application Insights](app-insights-cloudservices.md)
* [Envoyer des Diagnostics Windows Azure tooApplication Insights](app-insights-azure-diagnostics.md)
* [Automatisation de la configuration des alertes](app-insights-powershell-alerts.md)

