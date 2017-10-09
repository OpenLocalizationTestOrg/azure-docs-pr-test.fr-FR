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
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="00740-103">Activer les diagnostics dans Azure Cloud Services à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="00740-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="00740-104">Vous pouvez collecter des données de diagnostic tels que les journaux des applications, etc. à partir d’un Service Cloud à l’aide des compteurs de performance hello extension Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="00740-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using hello Azure Diagnostics extension.</span></span> <span data-ttu-id="00740-105">Cet article décrit comment tooenable hello extension Azure Diagnostics pour un Service Cloud à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="00740-105">This article describes how tooenable hello Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="00740-106">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour hello requis pour cet article.</span><span class="sxs-lookup"><span data-stu-id="00740-106">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="00740-107">Activer l’extension de diagnostics lors du déploiement d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="00740-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="00740-108">Cette approche est de type d’intégration toocontinuous applicable de scénarios, où les diagnostics hello extension peut être activée dans le cadre du déploiement hello service cloud.</span><span class="sxs-lookup"><span data-stu-id="00740-108">This approach is applicable toocontinuous integration type of scenarios, where hello diagnostics extension can be enabled as part of deploying hello cloud service.</span></span> <span data-ttu-id="00740-109">Lors de la création d’un nouveau déploiement de Service Cloud vous pouvez activer l’extension de diagnostics hello en passant hello *ExtensionConfiguration* paramètre toohello [New-Azuredeployement](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="00740-109">When creating a new Cloud Service deployment you can enable hello diagnostics extension by passing in hello *ExtensionConfiguration* parameter toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="00740-110">Hello *ExtensionConfiguration* accepte un tableau de configurations de diagnostics qui peuvent être créés à l’aide de hello [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="00740-110">hello *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using hello [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="00740-111">Hello suivant montre comment vous pouvez activer les diagnostics pour un service cloud avec WebRole et WorkerRole, ayant chacun une configuration de différents tests de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="00740-111">hello following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

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

<span data-ttu-id="00740-112">Si le fichier de configuration de diagnostics hello spécifie un `StorageAccount` élément avec un nom de compte de stockage, puis hello `New-AzureServiceDiagnosticsExtensionConfig` applet de commande utilisent automatiquement ce compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="00740-112">If hello diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="00740-113">Pour que cette toowork, compte de stockage hello doit toobe dans hello même abonnement que hello Service Cloud en cours de déploiement.</span><span class="sxs-lookup"><span data-stu-id="00740-113">For this toowork, hello storage account needs toobe in hello same subscription as hello Cloud Service being deployed.</span></span>

<span data-ttu-id="00740-114">À partir de Azure SDK 2.6 publier des fichiers de configuration d’extension hello ultérieur générés par hello MSBuild sortie cible les nom de compte de stockage hello en fonction de la chaîne de configuration de diagnostics hello spécifié dans le fichier de configuration de service hello (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="00740-114">From Azure SDK 2.6 onward hello extension configuration files generated by hello MSBuild publish target output will include hello storage account name based on hello diagnostics configuration string specified in hello service configuration file (.cscfg).</span></span> <span data-ttu-id="00740-115">script Hello ci-dessous vous montre comment tooparse hello Extension des fichiers de configuration hello la sortie de la cible de publication et configurer l’extension diagnostics pour chaque rôle lors du déploiement de service de cloud computing hello.</span><span class="sxs-lookup"><span data-stu-id="00740-115">hello script below shows you how tooparse hello Extension configuration files from hello publish target output and configure diagnostics extension for each role when deploying hello cloud service.</span></span>

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

<span data-ttu-id="00740-116">Visual Studio Online utilise une approche similaire pour des déploiements automatisés de Services Cloud avec l’extension de diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="00740-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with hello diagnostics extension.</span></span> <span data-ttu-id="00740-117">Consultez [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) pour obtenir un exemple complet.</span><span class="sxs-lookup"><span data-stu-id="00740-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="00740-118">Si aucun `StorageAccount` a été spécifié dans la configuration des diagnostics hello, vous devez toopass Bonjour *StorageAccountName* paramètre toohello applet de commande.</span><span class="sxs-lookup"><span data-stu-id="00740-118">If no `StorageAccount` was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="00740-119">Si hello *StorageAccountName* paramètre est spécifié, puis applet de commande hello sera toujours utiliser le compte de stockage hello est spécifié dans le paramètre hello et pas hello qui est spécifié dans le fichier de configuration des diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="00740-119">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="00740-120">Si les diagnostics hello compte de stockage est dans un autre abonnement hello Service Cloud, vous devez tooexplicitly passez hello *StorageAccountName* et *StorageAccountKey* paramètres applet de commande toohello.</span><span class="sxs-lookup"><span data-stu-id="00740-120">If hello diagnostics storage account is in a different subscription from hello Cloud Service, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="00740-121">Hello *StorageAccountKey* paramètre n’est pas nécessaire lorsque les diagnostics hello compte de stockage est dans hello même abonnement, car l’applet de commande hello peut automatiquement de requête et définir la valeur de clé hello lors de l’activation de l’extension de diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="00740-121">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="00740-122">Toutefois, si hello compte de stockage de diagnostics est dans un autre abonnement, puis hello applet de commande peuvent ne pas être automatiquement clé de hello tooget en mesure, vous devez tooexplicitly spécifiez clé hello via hello *StorageAccountKey* paramètre.</span><span class="sxs-lookup"><span data-stu-id="00740-122">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="00740-123">Activer l’extension de diagnostics sur un service cloud existant</span><span class="sxs-lookup"><span data-stu-id="00740-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="00740-124">Vous pouvez utiliser hello [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) applet de commande tooenable ou mise à jour de configuration des diagnostics sur un Service Cloud qui est déjà en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="00740-124">You can use hello [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="00740-125">Obtenir la configuration actuelle de l’extension de diagnostics</span><span class="sxs-lookup"><span data-stu-id="00740-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="00740-126">Hello d’utilisation [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) applet de commande tooget hello configuration des diagnostics pour un service cloud.</span><span class="sxs-lookup"><span data-stu-id="00740-126">Use hello [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget hello current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="00740-127">Supprimer l’extension de diagnostics</span><span class="sxs-lookup"><span data-stu-id="00740-127">Remove diagnostics extension</span></span>
<span data-ttu-id="00740-128">tooturn désactiver les tests de diagnostic sur un cloud service que vous pouvez utiliser hello [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="00740-128">tooturn off diagnostics on a cloud service you can use hello [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="00740-129">Si vous avez activé l’extension à l’aide des diagnostics hello *Set-AzureServiceDiagnosticsExtension* ou hello *New-AzureServiceDiagnosticsExtensionConfig* sans hello *rôle* paramètre, vous pouvez supprimer hello extension à l’aide *Remove-AzureServiceDiagnosticsExtension* sans hello *rôle* paramètre.</span><span class="sxs-lookup"><span data-stu-id="00740-129">If you enabled hello diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or hello *New-AzureServiceDiagnosticsExtensionConfig* without hello *Role* parameter then you can remove hello extension using *Remove-AzureServiceDiagnosticsExtension* without hello *Role* parameter.</span></span> <span data-ttu-id="00740-130">Si hello *rôle* paramètre a été utilisé lors de l’activation d’extension de hello, puis il doit également être utilisé lors de la suppression d’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="00740-130">If hello *Role* parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="00740-131">extension des diagnostics hello tooremove à partir de chaque rôle individuel :</span><span class="sxs-lookup"><span data-stu-id="00740-131">tooremove hello diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="00740-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="00740-132">Next Steps</span></span>
* <span data-ttu-id="00740-133">Pour plus d’informations sur l’utilisation de diagnostics Azure et autres problèmes de tootroubleshoot techniques, consultez [activation des Diagnostics dans Azure Cloud Services et Machines virtuelles](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="00740-133">For additional guidance on using Azure diagnostics and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="00740-134">Hello [schéma de Configuration de Diagnostics](https://msdn.microsoft.com/library/azure/dn782207.aspx) explique hello diverses configurations xml options pour l’extension de diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="00740-134">hello [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains hello various xml configurations options for hello diagnostics extension.</span></span>
* <span data-ttu-id="00740-135">toolearn extension de diagnostics tooenable hello pour les ordinateurs virtuels, voir [créer une machine virtuelle Windows avec l’analyse et de diagnostics à l’aide du modèle de gestionnaire de ressources Azure](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="00740-135">toolearn how tooenable hello diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
