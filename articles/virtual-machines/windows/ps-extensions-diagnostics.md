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
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a>Utilisez les Diagnostics de Azure PowerShell tooenable dans une machine virtuelle exécutant Windows
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Les Diagnostics Azure sont fonction hello dans Azure qui active la collecte de hello de données de diagnostic sur une application déployée. Vous pouvez utiliser hello diagnostics extension toocollect données de diagnostic tels que les journaux des applications ou des compteurs de performance à partir d’une machine virtuelle Azure (VM) qui exécute Windows. Cet article décrit comment toouse Windows PowerShell tooenable hello extension diagnostics pour une machine virtuelle. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour hello requis pour cet article.

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a>Activer l’extension de diagnostics hello si vous utilisez le modèle de déploiement du Gestionnaire de ressources hello
Vous pouvez activer les extension de diagnostics hello lorsque vous créez une machine virtuelle de Windows via le modèle de déploiement du Gestionnaire de ressources Azure hello en ajoutant hello extension configuration toohello Gestionnaire de ressources du modèle. Consultez [créer une machine virtuelle Windows avec l’analyse et de diagnostics à l’aide du modèle de gestionnaire de ressources Azure hello](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

extension des diagnostics hello tooenable sur un ordinateur virtuel existant qui a été créé via le modèle de déploiement du Gestionnaire de ressources hello, vous pouvez utiliser hello [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) applet de commande PowerShell comme indiqué ci-dessous.

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


*$diagnosticsconfig_path* est hello chemin d’accès toohello fichier qui contient la configuration des diagnostics hello dans XML, comme décrit dans hello [exemple](#sample-diagnostics-configuration) ci-dessous.  

Si le fichier de configuration de diagnostics hello spécifie un **StorageAccount** élément avec un nom de compte de stockage, puis hello *Set-AzureRMVMDiagnosticsExtension* script définit automatiquement hello Diagnostics extension toosend des données de diagnostic toothat compte de stockage. Pour que cette toowork, compte de stockage hello doit toobe dans hello même abonnement que hello de machine virtuelle.

Si aucun **StorageAccount** a été spécifié dans la configuration des diagnostics hello, vous devez toopass Bonjour *StorageAccountName* paramètre toohello applet de commande. Si hello *StorageAccountName* paramètre est spécifié, puis applet de commande hello sera toujours utiliser le compte de stockage hello est spécifié dans le paramètre hello et pas hello qui est spécifié dans le fichier de configuration des diagnostics hello.

Si les diagnostics hello compte de stockage est dans un autre abonnement hello machine virtuelle, vous devez tooexplicitly passez hello *StorageAccountName* et *StorageAccountKey* paramètres toohello applet de commande. Hello *StorageAccountKey* paramètre n’est pas nécessaire lorsque les diagnostics hello compte de stockage est dans hello même abonnement, car l’applet de commande hello peut automatiquement de requête et définir la valeur de clé hello lors de l’activation de l’extension de diagnostics hello. Toutefois, si hello compte de stockage de diagnostics est dans un autre abonnement, puis hello applet de commande peuvent ne pas être automatiquement clé de hello tooget en mesure, vous devez tooexplicitly spécifiez clé hello via hello *StorageAccountKey* paramètre.  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

Une fois que l’extension de diagnostics hello est activée sur une machine virtuelle, vous pouvez obtenir les paramètres actuels de hello à l’aide de hello [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) applet de commande.

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

Hello applet de commande renvoie *PublicSettings*, qui contient la configuration des diagnostics hello. Deux types de configuration sont prises en charge, WadCfg et xmlCfg. WadCfg est une configuration JSON et xmlCfg est une configuration XML dans un format codé en base64. tooread hello XML, vous devez toodecode il.

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

Hello [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) applet de commande peut être utilisé tooremove hello extension des diagnostics à partir de la machine virtuelle de hello.  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a>Activer l’extension de diagnostics hello si vous utilisez le modèle de déploiement classique de hello
Vous pouvez utiliser hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) tooenable de l’applet de commande une extension de diagnostics sur une machine virtuelle que vous créez via un modèle de déploiement classique hello. Hello exemple suivant montre comment toocreate une nouvelle machine virtuelle via le modèle de déploiement classique hello avec l’extension de diagnostics hello activé.

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

extension de diagnostics hello tooenable sur un ordinateur virtuel existant qui a été créé via le modèle de déploiement classique de hello, première utilisation hello [Get-AzureVM](/powershell/module/azure/get-azurevm) configuration d’ordinateur virtuel d’applet de commande tooget hello. Puis mettez à jour l’extension des diagnostics configuration tooinclude hello hello machine virtuelle à l’aide de hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) applet de commande. Enfin, appliquez hello mis à jour configuration toohello machine virtuelle à l’aide de [Update-AzureVM](/powershell/module/azure/update-azurevm).

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a>Effectuer un échantillon de configuration de diagnostics
Hello que code XML suivant peut être utilisé pour la configuration des diagnostics hello public avec hello au-dessus de scripts. Cet exemple de configuration des diagnostics de hello transférera différents performances compteurs toohello diagnostics compte de stockage, ainsi que des erreurs de l’application hello, la sécurité et les canaux de système dans les journaux des événements Windows hello et toutes les erreurs journaux d’infrastructure.

configuration de Hello doit suivant de hello toobe tooinclude mis à jour :

* Hello *resourceID* attribut Hello **métriques** élément doit toobe mis à jour avec l’ID de ressource hello pour hello machine virtuelle.
  
  * Hello ID peut être construit à l’aide de hello suivant le modèle de ressource : « / subscriptions / {*ID d’abonnement pour l’abonnement hello avec hello VM*} /resourceGroups/ {*nom du groupe de ressources hello pour hello VM*} / providers/Microsoft.Compute/virtualMachines/ {*hello nom d’ordinateur virtuel*} ».
  * Par exemple, si hello ID d’abonnement pour l’abonnement hello où hello machine virtuelle est en cours d’exécution est **11111111-1111-1111-1111-111111111111**, nom du groupe de ressources pour le groupe de ressources hello hello est **MyResourceGroup**, et hello nom de la machine virtuelle est **MyWindowsVM**, puis hello valeur pour *resourceID* serait :
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * Pour plus d’informations sur la façon dont les mesures sont les compteurs de performance hello selon généré et configuration des métriques, consultez [table des métriques dans le stockage Azure Diagnostics](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).
* Hello **StorageAccount** toobe mis à jour avec le nom hello hello diagnostics du compte de stockage a besoin d’élément.
  
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

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur l’utilisation de la fonctionnalité des Diagnostics Windows Azure hello et autres problèmes de tootroubleshoot techniques, consultez [activation des Diagnostics dans Azure Cloud Services et Machines virtuelles](../../cloud-services/cloud-services-dotnet-diagnostics.md).
* [Schéma des configurations de diagnostics](https://msdn.microsoft.com/library/azure/mt634524.aspx) explique hello diverses configurations XML options pour l’extension de diagnostics hello.

