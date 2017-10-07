---
title: aaaUse diagnostics tooenable de Azure PowerShell sur une machine virtuelle Windows | Documents Microsoft
services: virtual-machines-windows
documentationcenter: 
description: "Découvrez comment toouse PowerShell tooenable Diagnostics Azure dans une machine virtuelle exécutant Windows"
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
ms.openlocfilehash: e945f0de154b5ba600f845f0d577b48e2254573b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="f9c60-103">Utilisez les Diagnostics de Azure PowerShell tooenable dans une machine virtuelle exécutant Windows</span><span class="sxs-lookup"><span data-stu-id="f9c60-103">Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="f9c60-104">Les Diagnostics Azure sont fonction hello dans Azure qui active la collecte de hello de données de diagnostic sur une application déployée.</span><span class="sxs-lookup"><span data-stu-id="f9c60-104">Azure Diagnostics is hello capability within Azure that enables hello collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="f9c60-105">Vous pouvez utiliser hello diagnostics extension toocollect données de diagnostic tels que les journaux des applications ou des compteurs de performance à partir d’une machine virtuelle Azure (VM) qui exécute Windows.</span><span class="sxs-lookup"><span data-stu-id="f9c60-105">You can use hello diagnostics extension toocollect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="f9c60-106">Cet article décrit comment toouse Windows PowerShell tooenable hello extension diagnostics pour une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f9c60-106">This article describes how toouse Windows PowerShell tooenable hello diagnostics extension for a VM.</span></span> <span data-ttu-id="f9c60-107">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour hello requis pour cet article.</span><span class="sxs-lookup"><span data-stu-id="f9c60-107">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a><span data-ttu-id="f9c60-108">Activer l’extension de diagnostics hello si vous utilisez le modèle de déploiement du Gestionnaire de ressources hello</span><span class="sxs-lookup"><span data-stu-id="f9c60-108">Enable hello diagnostics extension if you use hello Resource Manager deployment model</span></span>
<span data-ttu-id="f9c60-109">Vous pouvez activer les extension de diagnostics hello lorsque vous créez une machine virtuelle de Windows via le modèle de déploiement du Gestionnaire de ressources Azure hello en ajoutant hello extension configuration toohello Gestionnaire de ressources du modèle.</span><span class="sxs-lookup"><span data-stu-id="f9c60-109">You can enable hello diagnostics extension while you create a Windows VM through hello Azure Resource Manager deployment model by adding hello extension configuration toohello Resource Manager template.</span></span> <span data-ttu-id="f9c60-110">Consultez [créer une machine virtuelle Windows avec l’analyse et de diagnostics à l’aide du modèle de gestionnaire de ressources Azure hello](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f9c60-110">See [Create a Windows virtual machine with monitoring and diagnostics by using hello Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="f9c60-111">extension des diagnostics hello tooenable sur un ordinateur virtuel existant qui a été créé via le modèle de déploiement du Gestionnaire de ressources hello, vous pouvez utiliser hello [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) applet de commande PowerShell comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f9c60-111">tooenable hello diagnostics extension on an existing VM that was created through hello Resource Manager deployment model, you can use hello [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="f9c60-112">*$diagnosticsconfig_path* est hello chemin d’accès toohello fichier qui contient la configuration des diagnostics hello dans XML, comme décrit dans hello [exemple](#sample-diagnostics-configuration) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f9c60-112">*$diagnosticsconfig_path* is hello path toohello file that contains hello diagnostics configuration in XML, as described in hello [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="f9c60-113">Si le fichier de configuration de diagnostics hello spécifie un **StorageAccount** élément avec un nom de compte de stockage, puis hello *Set-AzureRMVMDiagnosticsExtension* script définit automatiquement hello Diagnostics extension toosend des données de diagnostic toothat compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f9c60-113">If hello diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then hello *Set-AzureRMVMDiagnosticsExtension* script will automatically set hello diagnostics extension toosend diagnostic data toothat storage account.</span></span> <span data-ttu-id="f9c60-114">Pour que cette toowork, compte de stockage hello doit toobe dans hello même abonnement que hello de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f9c60-114">For this toowork, hello storage account needs toobe in hello same subscription as hello VM.</span></span>

<span data-ttu-id="f9c60-115">Si aucun **StorageAccount** a été spécifié dans la configuration des diagnostics hello, vous devez toopass Bonjour *StorageAccountName* paramètre toohello applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f9c60-115">If no **StorageAccount** was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="f9c60-116">Si hello *StorageAccountName* paramètre est spécifié, puis applet de commande hello sera toujours utiliser le compte de stockage hello est spécifié dans le paramètre hello et pas hello qui est spécifié dans le fichier de configuration des diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="f9c60-116">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="f9c60-117">Si les diagnostics hello compte de stockage est dans un autre abonnement hello machine virtuelle, vous devez tooexplicitly passez hello *StorageAccountName* et *StorageAccountKey* paramètres toohello applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f9c60-117">If hello diagnostics storage account is in a different subscription from hello VM, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="f9c60-118">Hello *StorageAccountKey* paramètre n’est pas nécessaire lorsque les diagnostics hello compte de stockage est dans hello même abonnement, car l’applet de commande hello peut automatiquement de requête et définir la valeur de clé hello lors de l’activation de l’extension de diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="f9c60-118">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="f9c60-119">Toutefois, si hello compte de stockage de diagnostics est dans un autre abonnement, puis hello applet de commande peuvent ne pas être automatiquement clé de hello tooget en mesure, vous devez tooexplicitly spécifiez clé hello via hello *StorageAccountKey* paramètre.</span><span class="sxs-lookup"><span data-stu-id="f9c60-119">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="f9c60-120">Une fois que l’extension de diagnostics hello est activée sur une machine virtuelle, vous pouvez obtenir les paramètres actuels de hello à l’aide de hello [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f9c60-120">Once hello diagnostics extension is enabled on a VM, you can get hello current settings by using hello [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="f9c60-121">Hello applet de commande renvoie *PublicSettings*, qui contient la configuration des diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="f9c60-121">hello cmdlet returns *PublicSettings*, which contains hello diagnostics configuration.</span></span> <span data-ttu-id="f9c60-122">Deux types de configuration sont prises en charge, WadCfg et xmlCfg.</span><span class="sxs-lookup"><span data-stu-id="f9c60-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="f9c60-123">WadCfg est une configuration JSON et xmlCfg est une configuration XML dans un format codé en base64.</span><span class="sxs-lookup"><span data-stu-id="f9c60-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="f9c60-124">tooread hello XML, vous devez toodecode il.</span><span class="sxs-lookup"><span data-stu-id="f9c60-124">tooread hello XML, you need toodecode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="f9c60-125">Hello [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) applet de commande peut être utilisé tooremove hello extension des diagnostics à partir de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="f9c60-125">hello [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used tooremove hello diagnostics extension from hello VM.</span></span>  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a><span data-ttu-id="f9c60-126">Activer l’extension de diagnostics hello si vous utilisez le modèle de déploiement classique de hello</span><span class="sxs-lookup"><span data-stu-id="f9c60-126">Enable hello diagnostics extension if you use hello classic deployment model</span></span>
<span data-ttu-id="f9c60-127">Vous pouvez utiliser hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) tooenable de l’applet de commande une extension de diagnostics sur une machine virtuelle que vous créez via un modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="f9c60-127">You can use hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable a diagnostics extension on a VM that you create through hello classic deployment model.</span></span> <span data-ttu-id="f9c60-128">Hello exemple suivant montre comment toocreate une nouvelle machine virtuelle via le modèle de déploiement classique hello avec l’extension de diagnostics hello activé.</span><span class="sxs-lookup"><span data-stu-id="f9c60-128">hello following example shows how toocreate a new VM through hello classic deployment model with hello diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="f9c60-129">extension de diagnostics hello tooenable sur un ordinateur virtuel existant qui a été créé via le modèle de déploiement classique de hello, première utilisation hello [Get-AzureVM](/powershell/module/azure/get-azurevm) configuration d’ordinateur virtuel d’applet de commande tooget hello.</span><span class="sxs-lookup"><span data-stu-id="f9c60-129">tooenable hello diagnostics extension on an existing VM that was created through hello classic deployment model, first use hello [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet tooget hello VM configuration.</span></span> <span data-ttu-id="f9c60-130">Puis mettez à jour l’extension des diagnostics configuration tooinclude hello hello machine virtuelle à l’aide de hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f9c60-130">Then update hello VM configuration tooinclude hello diagnostics extension by using hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="f9c60-131">Enfin, appliquez hello mis à jour configuration toohello machine virtuelle à l’aide de [Update-AzureVM](/powershell/module/azure/update-azurevm).</span><span class="sxs-lookup"><span data-stu-id="f9c60-131">Finally, apply hello updated configuration toohello VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="f9c60-132">Effectuer un échantillon de configuration de diagnostics</span><span class="sxs-lookup"><span data-stu-id="f9c60-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="f9c60-133">Hello que code XML suivant peut être utilisé pour la configuration des diagnostics hello public avec hello au-dessus de scripts.</span><span class="sxs-lookup"><span data-stu-id="f9c60-133">hello following XML can be used for hello diagnostics public configuration with hello above scripts.</span></span> <span data-ttu-id="f9c60-134">Cet exemple de configuration des diagnostics de hello transférera différents performances compteurs toohello diagnostics compte de stockage, ainsi que des erreurs de l’application hello, la sécurité et les canaux de système dans les journaux des événements Windows hello et toutes les erreurs journaux d’infrastructure.</span><span class="sxs-lookup"><span data-stu-id="f9c60-134">This sample configuration will transfer various performance counters toohello diagnostics storage account, along with errors from hello application, security, and system channels in hello Windows event logs and any errors from hello diagnostics infrastructure logs.</span></span>

<span data-ttu-id="f9c60-135">configuration de Hello doit suivant de hello toobe tooinclude mis à jour :</span><span class="sxs-lookup"><span data-stu-id="f9c60-135">hello configuration needs toobe updated tooinclude hello following:</span></span>

* <span data-ttu-id="f9c60-136">Hello *resourceID* attribut Hello **métriques** élément doit toobe mis à jour avec l’ID de ressource hello pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f9c60-136">hello *resourceID* attribute of hello **Metrics** element needs toobe updated with hello resource ID for hello VM.</span></span>
  
  * <span data-ttu-id="f9c60-137">Hello ID peut être construit à l’aide de hello suivant le modèle de ressource : « / subscriptions / {*ID d’abonnement pour l’abonnement hello avec hello VM*} /resourceGroups/ {*nom du groupe de ressources hello pour hello VM*} / providers/Microsoft.Compute/virtualMachines/ {*hello nom d’ordinateur virtuel*} ».</span><span class="sxs-lookup"><span data-stu-id="f9c60-137">hello resource ID can be constructed by using hello following pattern: "/subscriptions/{*subscription ID for hello subscription with hello VM*}/resourceGroups/{*hello resourcegroup name for hello VM*}/providers/Microsoft.Compute/virtualMachines/{*hello VM Name*}".</span></span>
  * <span data-ttu-id="f9c60-138">Par exemple, si hello ID d’abonnement pour l’abonnement hello où hello machine virtuelle est en cours d’exécution est **11111111-1111-1111-1111-111111111111**, nom du groupe de ressources pour le groupe de ressources hello hello est **MyResourceGroup**, et hello nom de la machine virtuelle est **MyWindowsVM**, puis hello valeur pour *resourceID* serait :</span><span class="sxs-lookup"><span data-stu-id="f9c60-138">For example, if hello subscription ID for hello subscription where hello VM is running is **11111111-1111-1111-1111-111111111111**, hello resource group name for hello resource group is **MyResourceGroup**, and hello VM Name is **MyWindowsVM**, then hello value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="f9c60-139">Pour plus d’informations sur la façon dont les mesures sont les compteurs de performance hello selon généré et configuration des métriques, consultez [table des métriques dans le stockage Azure Diagnostics](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span><span class="sxs-lookup"><span data-stu-id="f9c60-139">For more information on how metrics are generated based on hello performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="f9c60-140">Hello **StorageAccount** toobe mis à jour avec le nom hello hello diagnostics du compte de stockage a besoin d’élément.</span><span class="sxs-lookup"><span data-stu-id="f9c60-140">hello **StorageAccount** element needs toobe updated with hello name of hello diagnostics storage account.</span></span>
  
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
        <Metrics resourceId="(Update with resource ID for hello VM)" >
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

## <a name="next-steps"></a><span data-ttu-id="f9c60-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9c60-141">Next steps</span></span>
* <span data-ttu-id="f9c60-142">Pour plus d’informations sur l’utilisation de la fonctionnalité des Diagnostics Windows Azure hello et autres problèmes de tootroubleshoot techniques, consultez [activation des Diagnostics dans Azure Cloud Services et Machines virtuelles](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="f9c60-142">For additional guidance on using hello Azure Diagnostics capability and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="f9c60-143">[Schéma des configurations de diagnostics](https://msdn.microsoft.com/library/azure/mt634524.aspx) explique hello diverses configurations XML options pour l’extension de diagnostics hello.</span><span class="sxs-lookup"><span data-stu-id="f9c60-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains hello various XML configurations options for hello diagnostics extension.</span></span>

