---
title: "Utilisation d’Azure PowerShell pour activer les diagnostics sur une machine virtuelle Windows | Microsoft Docs"
services: virtual-machines-windows
documentationcenter: 
description: "Utilisation de PowerShell pour activer Azure Diagnostics sur une machine virtuelle exécutant Windows"
author: sbtron
manager: timlt
editor: 
ms.assetid: 2e6d88f2-1980-4a24-827e-a81616a0d247
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: saurabh
ms.openlocfilehash: d0be4a712657edfc516c5f32e66519f5d9486728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-enable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="f372b-103">Utiliser PowerShell pour activer Azure Diagnostics sur une machine virtuelle exécutant Windows</span><span class="sxs-lookup"><span data-stu-id="f372b-103">Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="f372b-104">Azure Diagnostics est la fonctionnalité Azure qui active la collecte de données de diagnostic dans une application déployée.</span><span class="sxs-lookup"><span data-stu-id="f372b-104">Azure Diagnostics is the capability within Azure that enables the collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="f372b-105">Vous pouvez utiliser l'extension de diagnostics pour collecter des données de diagnostic telles que les journaux des applications ou les compteurs de performances à partir d'une machine virtuelle Azure exécutant Windows.</span><span class="sxs-lookup"><span data-stu-id="f372b-105">You can use the diagnostics extension to collect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="f372b-106">Cet article décrit comment utiliser Windows PowerShell activer l’extension de diagnostics pour une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f372b-106">This article describes how to use Windows PowerShell to enable the diagnostics extension for a VM.</span></span> <span data-ttu-id="f372b-107">Consultez [Installer et configurer Azure PowerShell Azure](/powershell/azure/overview) pour connaître les conditions requises pour cet article.</span><span class="sxs-lookup"><span data-stu-id="f372b-107">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-the-diagnostics-extension-if-you-use-the-resource-manager-deployment-model"></a><span data-ttu-id="f372b-108">Activer l'extension de diagnostics si vous utilisez le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f372b-108">Enable the diagnostics extension if you use the Resource Manager deployment model</span></span>
<span data-ttu-id="f372b-109">Vous pouvez activer l'extension de diagnostics lors de la création d'une machine virtuelle Windows avec le modèle de déploiement Azure Resource Manager en ajoutant la configuration de l'extension au modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f372b-109">You can enable the diagnostics extension while you create a Windows VM through the Azure Resource Manager deployment model by adding the extension configuration to the Resource Manager template.</span></span> <span data-ttu-id="f372b-110">Consultez [Créer une machine virtuelle Windows avec des fonctionnalités de surveillance et de diagnostics à l’aide d’un modèle Azure Resource Manager](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f372b-110">See [Create a Windows virtual machine with monitoring and diagnostics by using the Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="f372b-111">Pour activer l'extension de diagnostics sur une machine virtuelle existante qui a été créée avec le modèle de déploiement Resource Manager, vous pouvez utiliser l'applet de commande PowerShell [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f372b-111">To enable the diagnostics extension on an existing VM that was created through the Resource Manager deployment model, you can use the [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="f372b-112">*$diagnosticsconfig_path* est le chemin d'accès au fichier contenant la configuration des diagnostics dans XML, comme décrit dans l'[exemple](#sample-diagnostics-configuration) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f372b-112">*$diagnosticsconfig_path* is the path to the file that contains the diagnostics configuration in XML, as described in the [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="f372b-113">Si le fichier de configuration des diagnostics spécifie un élément **StorageAccount** avec un nom de compte de stockage, le script *Set-AzureRMVMDiagnosticsExtension* définit automatiquement l'extension de diagnostics pour envoyer des données de diagnostic à ce compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f372b-113">If the diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then the *Set-AzureRMVMDiagnosticsExtension* script will automatically set the diagnostics extension to send diagnostic data to that storage account.</span></span> <span data-ttu-id="f372b-114">Pour que cela fonctionne, le compte de stockage doit appartenir au même abonnement que la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f372b-114">For this to work, the storage account needs to be in the same subscription as the VM.</span></span>

<span data-ttu-id="f372b-115">Si aucun **StorageAccount** n’a été spécifié dans la configuration des diagnostics, vous devez transmettre le paramètre *StorageAccountName* à l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f372b-115">If no **StorageAccount** was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="f372b-116">Si le paramètre *StorageAccountName* est spécifié, l’applet de commande utilise toujours le compte de stockage spécifié dans le paramètre et non celui spécifié dans le fichier de configuration des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="f372b-116">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="f372b-117">Si le compte de stockage de diagnostics appartient à un autre abonnement que celui de la machine virtuelle, vous devez transmettre explicitement les paramètres *StorageAccountName* et *StorageAccountKey* à l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f372b-117">If the diagnostics storage account is in a different subscription from the VM, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="f372b-118">Le paramètre *StorageAccountKey* n’est pas nécessaire lorsque le compte de stockage de diagnostics appartient au même abonnement si l’applet de commande peut interroger et définir automatiquement la valeur clé lors de l’activation de l’extension de diagnostics.</span><span class="sxs-lookup"><span data-stu-id="f372b-118">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="f372b-119">Toutefois, si le compte de stockage de diagnostics appartient à un autre abonnement, l’applet de commande n’est peut-être pas en mesure d’obtenir automatiquement la clé, et vous devez explicitement spécifier celle-ci par le biais du paramètre *StorageAccountKey* .</span><span class="sxs-lookup"><span data-stu-id="f372b-119">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="f372b-120">Une fois que l'extension de diagnostics est activée sur une machine virtuelle, vous pouvez obtenir les paramètres actuels à l'aide de l'applet de commande [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) .</span><span class="sxs-lookup"><span data-stu-id="f372b-120">Once the diagnostics extension is enabled on a VM, you can get the current settings by using the [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="f372b-121">L'applet de commande renvoie *PublicSettings*, qui contient la configuration des diagnostics.</span><span class="sxs-lookup"><span data-stu-id="f372b-121">The cmdlet returns *PublicSettings*, which contains the diagnostics configuration.</span></span> <span data-ttu-id="f372b-122">Deux types de configuration sont prises en charge, WadCfg et xmlCfg.</span><span class="sxs-lookup"><span data-stu-id="f372b-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="f372b-123">WadCfg est une configuration JSON et xmlCfg est une configuration XML dans un format codé en base64.</span><span class="sxs-lookup"><span data-stu-id="f372b-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="f372b-124">Pour lire le code CXML, vous devez le décoder.</span><span class="sxs-lookup"><span data-stu-id="f372b-124">To read the XML, you need to decode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="f372b-125">L’applet de commande [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) peut être utilisé pour supprimer l’extension de diagnostics à partir de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f372b-125">The [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used to remove the diagnostics extension from the VM.</span></span>  

## <a name="enable-the-diagnostics-extension-if-you-use-the-classic-deployment-model"></a><span data-ttu-id="f372b-126">Activer l'extension de diagnostics si vous utilisez le modèle de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="f372b-126">Enable the diagnostics extension if you use the classic deployment model</span></span>
<span data-ttu-id="f372b-127">Vous pouvez utiliser l'applet de commande [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) pour activer une extension de diagnostics sur une machine virtuelle créée à l'aide du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="f372b-127">You can use the [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet to enable a diagnostics extension on a VM that you create through the classic deployment model.</span></span> <span data-ttu-id="f372b-128">L'exemple suivant indique comment créer une machine virtuelle à l'aide du modèle de déploiement classique avec l'extension de diagnostics activée.</span><span class="sxs-lookup"><span data-stu-id="f372b-128">The following example shows how to create a new VM through the classic deployment model with the diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="f372b-129">Pour activer l'extension de diagnostics sur une machine virtuelle existante créée avec le modèle de déploiement classique, utilisez d'abord l'applet de commande [Get-AzureVM](/powershell/module/azure/get-azurevm) pour obtenir la configuration de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f372b-129">To enable the diagnostics extension on an existing VM that was created through the classic deployment model, first use the [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet to get the VM configuration.</span></span> <span data-ttu-id="f372b-130">Mettez ensuite à jour la configuration de la machine virtuelle afin d'inclure l'extension de diagnostics à l'aide de l'applet de commande [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) .</span><span class="sxs-lookup"><span data-stu-id="f372b-130">Then update the VM configuration to include the diagnostics extension by using the [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="f372b-131">Pour finir, appliquez la configuration mise à jour à la machine virtuelle à l'aide de [Update-AzureVM](/powershell/module/azure/update-azurevm).</span><span class="sxs-lookup"><span data-stu-id="f372b-131">Finally, apply the updated configuration to the VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="f372b-132">Effectuer un échantillon de configuration de diagnostics</span><span class="sxs-lookup"><span data-stu-id="f372b-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="f372b-133">Le code XML suivant peut être utilisé pour la configuration publique de diagnostics avec les scripts ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f372b-133">The following XML can be used for the diagnostics public configuration with the above scripts.</span></span> <span data-ttu-id="f372b-134">Cet exemple de configuration transférera les différents compteurs de performance pour le compte de stockage de diagnostics, ainsi que les erreurs d'application, de sécurité et de canaux de système dans les journaux d'événement Windows, ainsi que toutes les erreurs dans les journaux d'infrastructure de diagnostics.</span><span class="sxs-lookup"><span data-stu-id="f372b-134">This sample configuration will transfer various performance counters to the diagnostics storage account, along with errors from the application, security, and system channels in the Windows event logs and any errors from the diagnostics infrastructure logs.</span></span>

<span data-ttu-id="f372b-135">La configuration doit être mise à jour pour inclure les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f372b-135">The configuration needs to be updated to include the following:</span></span>

* <span data-ttu-id="f372b-136">L'attribut *resourceID* de l'élément **Mesures** doit être mis à jour avec l'ID de ressource pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f372b-136">The *resourceID* attribute of the **Metrics** element needs to be updated with the resource ID for the VM.</span></span>
  
  * <span data-ttu-id="f372b-137">L’ID de ressource peut être construit à l’aide du modèle suivant : « /subscriptions/{*ID d’abonnement pour l’abonnement avec la machine virtuelle*}/resourceGroups/{*Nom du groupe de ressources pour la machine virtuelle*}/providers/Microsoft.Compute/virtualMachines/{*Nom de la machine virtuelle*} ».</span><span class="sxs-lookup"><span data-stu-id="f372b-137">The resource ID can be constructed by using the following pattern: "/subscriptions/{*subscription ID for the subscription with the VM*}/resourceGroups/{*The resourcegroup name for the VM*}/providers/Microsoft.Compute/virtualMachines/{*The VM Name*}".</span></span>
  * <span data-ttu-id="f372b-138">Par exemple, si l’ID d’abonnement pour l’abonnement dans lequel la machine virtuelle est en cours d’exécution est **11111111-1111-1111-1111-111111111111**, le nom du groupe de ressources pour le groupe de ressources est **MyResourceGroup** et le nom de la machine virtuelle est **MyWindowsVM**. La valeur pour *resourceID* serait alors :</span><span class="sxs-lookup"><span data-stu-id="f372b-138">For example, if the subscription ID for the subscription where the VM is running is **11111111-1111-1111-1111-111111111111**, the resource group name for the resource group is **MyResourceGroup**, and the VM Name is **MyWindowsVM**, then the value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="f372b-139">Pour plus d’informations sur la façon dont les mesures sont générées en fonction de la configuration des compteurs de performances et des mesures, consultez [Table des mesures Diagnostics Azure pour le stockage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span><span class="sxs-lookup"><span data-stu-id="f372b-139">For more information on how metrics are generated based on the performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="f372b-140">L’élément **StorageAccount** doit être mis à jour avec le nom du compte de stockage de diagnostics.</span><span class="sxs-lookup"><span data-stu-id="f372b-140">The **StorageAccount** element needs to be updated with the name of the diagnostics storage account.</span></span>
  
    ```
    <?xml version="1.0" encoding="utf-8"?>
    <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
        <WadCfg>
          <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
            <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error"/>
            <PerformanceCounters scheduledTransferPeriod="PT1M">
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU utilization" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Privileged Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU privileged time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% User Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU user time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor Information(_Total)\Processor Frequency" sampleRate="PT15S" unit="Count">
            <annotation displayName="CPU frequency" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\System\Processes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Processes" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Thread Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Threads" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Handle Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Handles" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\% Committed Bytes In Use" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Memory usage" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory available" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory committed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Commit Limit" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory commit limit" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Paged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Nonpaged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory non-paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Read Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active read time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Write Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active write time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Transfers/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Reads/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk read operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Writes/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk write operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Read Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk read speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Write Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk write speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Read Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average read queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Write Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average write queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\% Free Space" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk free space (percentage)" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\Free Megabytes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk free space (MB)" locale="en-us"/>
          </PerformanceCounterConfiguration>
        </PerformanceCounters>
        <Metrics resourceId="(Update with resource ID for the VM)" >
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*[System[(Level = 1 or Level = 2)]]"/>
          <DataSource name="Security!*[System[(Level = 1 or Level = 2)]"/>
          <DataSource name="System!*[System[(Level = 1 or Level = 2)]]"/>
        </WindowsEventLog>
          </DiagnosticMonitorConfiguration>
        </WadCfg>
        <StorageAccount>(Update with diagnostics storage account name)</StorageAccount>
    </PublicConfig>
    ```

## <a name="next-steps"></a><span data-ttu-id="f372b-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f372b-141">Next steps</span></span>
* <span data-ttu-id="f372b-142">Pour obtenir une aide supplémentaire sur l’utilisation de la fonction Diagnostics Azure et d’autres techniques pour résoudre les problèmes, consultez la page [Activation de Diagnostics dans Azure Cloud Services et Azure Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="f372b-142">For additional guidance on using the Azure Diagnostics capability and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="f372b-143">[schéma de configuration des diagnostics](https://msdn.microsoft.com/library/azure/mt634524.aspx) explique les différentes options de configuration XML pour l'extension de diagnostics.</span><span class="sxs-lookup"><span data-stu-id="f372b-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains the various XML configurations options for the diagnostics extension.</span></span>

