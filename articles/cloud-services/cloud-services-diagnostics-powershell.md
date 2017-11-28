---
title: "Activer les diagnostics dans Azure Cloud Services à l’aide de PowerShell | Microsoft Docs"
description: "Découvrez comment activer les diagnostics pour les services cloud à l’aide de PowerShell"
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
ms.openlocfilehash: 8dd9724981860c9cd4ccc443cc2bfdc465811e7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="a0965-103">Activer les diagnostics dans Azure Cloud Services à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0965-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="a0965-104">Vous pouvez collecter des données de diagnostic telles que les journaux des applications, les compteurs de performances, etc. à partir d’un service cloud à l’aide de l’extension de diagnostics Azure.</span><span class="sxs-lookup"><span data-stu-id="a0965-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using the Azure Diagnostics extension.</span></span> <span data-ttu-id="a0965-105">Cet article décrit comment activer l’extension Diagnostics Azure pour un service cloud à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a0965-105">This article describes how to enable the Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="a0965-106">Consultez [Installer et configurer Azure PowerShell Azure](/powershell/azure/overview) pour connaître les conditions requises pour cet article.</span><span class="sxs-lookup"><span data-stu-id="a0965-106">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="a0965-107">Activer l’extension de diagnostics lors du déploiement d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="a0965-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="a0965-108">Cette approche peut s’appliquer aux scénarios d’intégration continue où l’extension de diagnostics peut être activée dans le cadre du déploiement d’un service cloud.</span><span class="sxs-lookup"><span data-stu-id="a0965-108">This approach is applicable to continuous integration type of scenarios, where the diagnostics extension can be enabled as part of deploying the cloud service.</span></span> <span data-ttu-id="a0965-109">Lorsque vous créez un nouveau déploiement de service cloud, vous pouvez activer l’extension de diagnostics en transmettant le paramètre *ExtensionConfiguration* à l’applet de commande [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="a0965-109">When creating a new Cloud Service deployment you can enable the diagnostics extension by passing in the *ExtensionConfiguration* parameter to the [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="a0965-110">Le paramètre *ExtensionConfiguration* prend un tableau de configurations de diagnostics qui peut être créé à l’aide de l’applet de commande [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="a0965-110">The *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using the [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="a0965-111">L’exemple suivant montre comment vous pouvez activer les diagnostics pour un service cloud avec un rôle web et un rôle de travail possédant chacun sa propre configuration de diagnostics.</span><span class="sxs-lookup"><span data-stu-id="a0965-111">The following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

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

<span data-ttu-id="a0965-112">Si le fichier de configuration des diagnostics spécifie un élément `StorageAccount` avec un nom de compte de stockage, l’applet de commande `New-AzureServiceDiagnosticsExtensionConfig` utilise automatiquement ce compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a0965-112">If the diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="a0965-113">Pour que cela fonctionne, le compte de stockage doit appartenir au même abonnement que le service cloud déployé.</span><span class="sxs-lookup"><span data-stu-id="a0965-113">For this to work, the storage account needs to be in the same subscription as the Cloud Service being deployed.</span></span>

<span data-ttu-id="a0965-114">À partir d’Azure SDK 2.6, les fichiers de configuration de l’extension générés par la sortie cible de publication MSBuild incluent le nom du compte de stockage en fonction de la chaîne de configuration des diagnostics spécifiée dans le fichier de configuration de service (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="a0965-114">From Azure SDK 2.6 onward the extension configuration files generated by the MSBuild publish target output will include the storage account name based on the diagnostics configuration string specified in the service configuration file (.cscfg).</span></span> <span data-ttu-id="a0965-115">Le script ci-dessous vous montre comment analyser les fichiers de configuration de l’extension à partir de la sortie cible de publication, et comment configurer l’extension de diagnostics pour chaque rôle lorsque vous déployez le service cloud.</span><span class="sxs-lookup"><span data-stu-id="a0965-115">The script below shows you how to parse the Extension configuration files from the publish target output and configure diagnostics extension for each role when deploying the cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find the Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find the RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
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

<span data-ttu-id="a0965-116">Visual Studio Online utilise une approche similaire pour les déploiements automatisés de services cloud avec l’extension de diagnostics.</span><span class="sxs-lookup"><span data-stu-id="a0965-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with the diagnostics extension.</span></span> <span data-ttu-id="a0965-117">Consultez [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) pour obtenir un exemple complet.</span><span class="sxs-lookup"><span data-stu-id="a0965-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="a0965-118">Si aucun `StorageAccount` n’a été spécifié dans la configuration des diagnostics, vous devez transmettre le paramètre *StorageAccountName* à l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a0965-118">If no `StorageAccount` was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="a0965-119">Si le paramètre *StorageAccountName* est spécifié, l’applet de commande utilise toujours le compte de stockage spécifié dans le paramètre et non celui spécifié dans le fichier de configuration des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="a0965-119">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="a0965-120">Si le compte de stockage de diagnostics appartient à un autre abonnement que celui du service cloud, vous devez transmettre explicitement les paramètres *StorageAccountName* et *StorageAccountKey* à l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a0965-120">If the diagnostics storage account is in a different subscription from the Cloud Service, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="a0965-121">Le paramètre *StorageAccountKey* n’est pas nécessaire lorsque le compte de stockage de diagnostics appartient au même abonnement si l’applet de commande peut interroger et définir automatiquement la valeur clé lors de l’activation de l’extension de diagnostics.</span><span class="sxs-lookup"><span data-stu-id="a0965-121">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="a0965-122">Toutefois, si le compte de stockage de diagnostics appartient à un autre abonnement, l’applet de commande n’est peut-être pas en mesure d’obtenir automatiquement la clé, et vous devez explicitement spécifier celle-ci par le biais du paramètre *StorageAccountKey* .</span><span class="sxs-lookup"><span data-stu-id="a0965-122">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="a0965-123">Activer l’extension de diagnostics sur un service cloud existant</span><span class="sxs-lookup"><span data-stu-id="a0965-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="a0965-124">Vous pouvez utiliser l’applet de commande [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) pour activer ou mettre à jour la configuration de diagnostics sur un service cloud qui est déjà en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a0965-124">You can use the [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to enable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="a0965-125">Obtenir la configuration actuelle de l’extension de diagnostics</span><span class="sxs-lookup"><span data-stu-id="a0965-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="a0965-126">Pour obtenir la configuration de diagnostics actuelle pour un service cloud, utilisez l’applet de commande [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) :</span><span class="sxs-lookup"><span data-stu-id="a0965-126">Use the [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to get the current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="a0965-127">Supprimer l’extension de diagnostics</span><span class="sxs-lookup"><span data-stu-id="a0965-127">Remove diagnostics extension</span></span>
<span data-ttu-id="a0965-128">Pour désactiver les diagnostics sur un service cloud, vous pouvez utiliser l’applet de commande [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="a0965-128">To turn off diagnostics on a cloud service you can use the [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="a0965-129">Si vous avez activé l’extension de diagnostics à l’aide de *Set-AzureServiceDiagnosticsExtension* ou *New-AzureServiceDiagnosticsExtensionConfig* sans le paramètre *Role*, vous pouvez supprimer l’extension à l’aide de *Remove-AzureServiceDiagnosticsExtension* sans le paramètre *Role*.</span><span class="sxs-lookup"><span data-stu-id="a0965-129">If you enabled the diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or the *New-AzureServiceDiagnosticsExtensionConfig* without the *Role* parameter then you can remove the extension using *Remove-AzureServiceDiagnosticsExtension* without the *Role* parameter.</span></span> <span data-ttu-id="a0965-130">Si le paramètre *Role* a été utilisé lors de l’activation de l’extension, il doit également être utilisé lors de la suppression de l’extension.</span><span class="sxs-lookup"><span data-stu-id="a0965-130">If the *Role* parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="a0965-131">Pour supprimer l’extension de diagnostics de chaque rôle individuel :</span><span class="sxs-lookup"><span data-stu-id="a0965-131">To remove the diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="a0965-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0965-132">Next Steps</span></span>
* <span data-ttu-id="a0965-133">Pour obtenir une aide supplémentaire sur l’utilisation des diagnostics Azure et d’autres techniques pour résoudre les problèmes, consultez la page [Activation de Diagnostics dans Azure Cloud Services et Azure Virtual Machines](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="a0965-133">For additional guidance on using Azure diagnostics and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="a0965-134">Le [schéma de configuration des diagnostics](https://msdn.microsoft.com/library/azure/dn782207.aspx) explique les différentes options de configuration xml pour l’extension de diagnostics.</span><span class="sxs-lookup"><span data-stu-id="a0965-134">The [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains the various xml configurations options for the diagnostics extension.</span></span>
* <span data-ttu-id="a0965-135">Pour savoir comment activer l’extension de diagnostics pour les machines virtuelles, consultez [Créer une machine virtuelle Windows avec la surveillance et les diagnostics à l’aide d’un modèle Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="a0965-135">To learn how to enable the diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
