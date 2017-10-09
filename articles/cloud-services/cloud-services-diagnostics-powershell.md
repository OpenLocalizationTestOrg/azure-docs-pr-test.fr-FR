---
title: "aaaEnable des diagnostics dans Azure Cloud Services à l’aide de PowerShell | Documents Microsoft"
description: "Découvrez comment tooenable des diagnostics pour cloud services à l’aide de PowerShell"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 66e08754-8639-4022-ae18-4237749ba17d
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/06/2016
ms.author: adegeo
ms.openlocfilehash: 7c7444df13edc8d7f5663e20ec7558d36aac45d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a>Activer les diagnostics dans Azure Cloud Services à l’aide de PowerShell
Vous pouvez collecter des données de diagnostic tels que les journaux des applications, etc. à partir d’un Service Cloud à l’aide des compteurs de performance hello extension Azure Diagnostics. Cet article décrit comment tooenable hello extension Azure Diagnostics pour un Service Cloud à l’aide de PowerShell.  Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour hello requis pour cet article.

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Activer l’extension de diagnostics lors du déploiement d’un service cloud
Cette approche est de type d’intégration toocontinuous applicable de scénarios, où les diagnostics hello extension peut être activée dans le cadre du déploiement hello service cloud. Lors de la création d’un nouveau déploiement de Service Cloud vous pouvez activer l’extension de diagnostics hello en passant hello *ExtensionConfiguration* paramètre toohello [New-Azuredeployement](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) applet de commande. Hello *ExtensionConfiguration* accepte un tableau de configurations de diagnostics qui peuvent être créés à l’aide de hello [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) applet de commande.

Hello suivant montre comment vous pouvez activer les diagnostics pour un service cloud avec WebRole et WorkerRole, ayant chacun une configuration de différents tests de diagnostic.

```powershell
$service_name = "MyService"
$service_package = "CloudService.cspkg"
$service_config = "ServiceConfiguration.Cloud.cscfg"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)
```

Si le fichier de configuration de diagnostics hello spécifie un `StorageAccount` élément avec un nom de compte de stockage, puis hello `New-AzureServiceDiagnosticsExtensionConfig` applet de commande utilisent automatiquement ce compte de stockage. Pour que cette toowork, compte de stockage hello doit toobe dans hello même abonnement que hello Service Cloud en cours de déploiement.

À partir de Azure SDK 2.6 publier des fichiers de configuration d’extension hello ultérieur générés par hello MSBuild sortie cible les nom de compte de stockage hello en fonction de la chaîne de configuration de diagnostics hello spécifié dans le fichier de configuration de service hello (.cscfg). script Hello ci-dessous vous montre comment tooparse hello Extension des fichiers de configuration hello la sortie de la cible de publication et configurer l’extension diagnostics pour chaque rôle lors du déploiement de service de cloud computing hello.

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find hello Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find hello RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
    $roleName = ""
    $roles = $extPath -split ".",0,"simplematch"
    if ($roles -is [system.array] -and $roles.Length -gt 1)
    {
        $roleName = $roles[1]
        $x = 2
        while ($x -le $roles.Length)
            {
               if ($roles[$x] -ne "PubConfig")
                {
                    $roleName = $roleName + "." + $roles[$x]
                }
                else
                {
                    break
                }
                $x++
            }
        $fullExtPath = Join-Path -path $extensionsSearchPath -ChildPath $extPath
        $diagnosticsconfig = New-AzureServiceDiagnosticsExtensionConfig -Role $roleName -DiagnosticsConfigurationPath $fullExtPath
        $diagnosticsConfigurations += $diagnosticsconfig
    }
}
New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration $diagnosticsConfigurations
```

Visual Studio Online utilise une approche similaire pour des déploiements automatisés de Services Cloud avec l’extension de diagnostics hello. Consultez [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) pour obtenir un exemple complet.

Si aucun `StorageAccount` a été spécifié dans la configuration des diagnostics hello, vous devez toopass Bonjour *StorageAccountName* paramètre toohello applet de commande. Si hello *StorageAccountName* paramètre est spécifié, puis applet de commande hello sera toujours utiliser le compte de stockage hello est spécifié dans le paramètre hello et pas hello qui est spécifié dans le fichier de configuration des diagnostics hello.

Si les diagnostics hello compte de stockage est dans un autre abonnement hello Service Cloud, vous devez tooexplicitly passez hello *StorageAccountName* et *StorageAccountKey* paramètres applet de commande toohello. Hello *StorageAccountKey* paramètre n’est pas nécessaire lorsque les diagnostics hello compte de stockage est dans hello même abonnement, car l’applet de commande hello peut automatiquement de requête et définir la valeur de clé hello lors de l’activation de l’extension de diagnostics hello. Toutefois, si hello compte de stockage de diagnostics est dans un autre abonnement, puis hello applet de commande peuvent ne pas être automatiquement clé de hello tooget en mesure, vous devez tooexplicitly spécifiez clé hello via hello *StorageAccountKey* paramètre.

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Activer l’extension de diagnostics sur un service cloud existant
Vous pouvez utiliser hello [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) applet de commande tooenable ou mise à jour de configuration des diagnostics sur un Service Cloud qui est déjà en cours d’exécution.

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a>Obtenir la configuration actuelle de l’extension de diagnostics
Hello d’utilisation [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) applet de commande tooget hello configuration des diagnostics pour un service cloud.

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a>Supprimer l’extension de diagnostics
tooturn désactiver les tests de diagnostic sur un cloud service que vous pouvez utiliser hello [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) applet de commande.

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Si vous avez activé l’extension à l’aide des diagnostics hello *Set-AzureServiceDiagnosticsExtension* ou hello *New-AzureServiceDiagnosticsExtensionConfig* sans hello *rôle* paramètre, vous pouvez supprimer hello extension à l’aide *Remove-AzureServiceDiagnosticsExtension* sans hello *rôle* paramètre. Si hello *rôle* paramètre a été utilisé lors de l’activation d’extension de hello, puis il doit également être utilisé lors de la suppression d’extension de hello.

extension des diagnostics hello tooremove à partir de chaque rôle individuel :

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur l’utilisation de diagnostics Azure et autres problèmes de tootroubleshoot techniques, consultez [activation des Diagnostics dans Azure Cloud Services et Machines virtuelles](cloud-services-dotnet-diagnostics.md).
* Hello [schéma de Configuration de Diagnostics](https://msdn.microsoft.com/library/azure/dn782207.aspx) explique hello diverses configurations xml options pour l’extension de diagnostics hello.
* toolearn extension de diagnostics tooenable hello pour les ordinateurs virtuels, voir [créer une machine virtuelle Windows avec l’analyse et de diagnostics à l’aide du modèle de gestionnaire de ressources Azure](../virtual-machines/windows/extensions-diagnostics-template.md)
