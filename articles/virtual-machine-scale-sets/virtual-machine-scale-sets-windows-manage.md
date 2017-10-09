---
title: "aaaManage machines virtuelles dans un ensemble d’échelle de machines virtuelles | Documents Microsoft"
description: "Gérez des machines virtuelles dans un jeu de mise à l’échelle de machine virtuelle à l'aide d'Azure PowerShell."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d35fa77a-de96-4ccd-a332-eb181d1f4273
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 7d848729c0fc708bd596b61feb528cf4bf4bafd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a>Gérer des machines virtuelles dans un groupe de machines virtuelles identiques
Utilisez les tâches hello dans cet article toomanage les ordinateurs virtuels dans votre ensemble d’échelle de machine virtuelle.

La plupart des tâches hello qui impliquent la gestion d’une machine virtuelle dans un ensemble d’échelle requièrent que vous connaissez l’ID de l’instance de machine hello que vous souhaitez toomanage hello. Vous pouvez utiliser [Explorateur de ressources Azure](https://resources.azure.com) toofind hello des ID d’instance d’un ordinateur virtuel dans un ensemble d’échelle. Vous utilisez également l’Explorateur de ressources tooverify hello d’état hello tâches que vous avez terminé.

Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation hello dernière version de Azure PowerShell, en sélectionnant votre abonnement et l’ouverture de session tooyour compte.

## <a name="display-information-about-a-scale-set"></a>Affichage des informations relatives à un groupe identique
Vous pouvez obtenir des informations générales sur un ensemble d’échelle, qui est également référencé tooas hello-vue d’instance. Ou bien, vous pouvez obtenir des informations plus spécifiques, telles que des informations sur les ressources dans l’ensemble d’échelle hello hello.

Remplacez hello entre guillemets les valeurs avec le nom de hello ou votre groupe de ressources et l’échelle définie et puis exécutez la commande hello :

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

Le résultat suivant doit s’afficher :

    Id                                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/myvmss1
    Name                                        : myvmss1
    Type                                        : Microsoft.Compute/virtualMachineScaleSets
    Location                                    : centralus
    Sku                                         :
      Name                                      : Standard_A0
      Tier                                      : Standard
      Capacity                                  : 3
    UpgradePolicy                               :
      Mode                                      : Manual
    VirtualMachineProfile                       :
      OsProfile                                 :
        ComputerNamePrefix                      : vmss1
        AdminUsername                           : admin1
        WindowsConfiguration                    :
          ProvisionVMAgent                      : True
          EnableAutomaticUpdates                : True
    StorageProfile                              :
      ImageReference                            :
        Publisher                               : MicrosoftWindowsServer
        Offer                                   : WindowsServer
        Sku                                     : 2012-R2-Datacenter
        Version                                 : latest
      OsDisk                                    :
        Name                                    : vmssosdisk
        Caching                                 : ReadOnly
        CreateOption                            : FromImage
        VhdContainers[0]                        : https://astore.blob.core.windows.net/vmss
        VhdContainers[1]                        : https://gstore.blob.core.windows.net/vmss
        VhdContainers[2]                        : https://mstore.blob.core.windows.net/vmss
        VhdContainers[3]                        : https://sstore.blob.core.windows.net/vmss
        VhdContainers[4]                        : https://ystore.blob.core.windows.net/vmss
    NetworkProfile                              :
      NetworkInterfaceConfigurations[0]         :
        Name                                    : mync1
        Primary                                 : True
        IpConfigurations[0]                     :
          Name                                  : ip1
          Subnet                                :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/virtualNetworks/myvn1/subnets/mysn1
          LoadBalancerBackendAddressPools[0]    :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/backendAddressPools/bepool1
        LoadBalancerInboundNatPools[0]          :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/inboundNatPools/natpool1
    ExtensionProfile                            :
      Extensions[0]                             :
        Name                                    : Microsoft.Insights.VMDiagnosticsSettings
        Publisher                               : Microsoft.Azure.Diagnostics
        Type                                    : IaaSDiagnostics
        TypeHandlerVersion                      : 1.5
        AutoUpgradeMinorVersion                 : True
        Settings                                : {"xmlCfg":"...","storageAccount":"astore"}
    ProvisioningState                           : Succeeded

Remplacez hello entre guillemets les valeurs de nom hello de votre jeu de groupe et l’échelle des ressources. Remplacez  *#*  avec l’identificateur hello instance hello virtuels que vous souhaitez obtenir des informations tooget et exécutez :

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Un résultat de ce type est renvoyé :

    Id                            : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/
                                    virtualMachineScaleSets/myvmss1/virtualMachines/0
    Name                          : myvmss1_0
    Type                          : Microsoft.Compute/virtualMachineScaleSets/virtualMachines
    Location                      : centralus
    InstanceId                    : 0
    Sku                           :
      Name                        : Standard_A0
      Tier                        : Standard
    LatestModelApplied            : True
    StorageProfile                :
      ImageReference              :
        Publisher                 : MicrosoftWindowsServer
        Offer                     : WindowsServer
        Sku                       : 2012-R2-Datacenter
        Version                   : 4.0.20160617
      OsDisk                      :
        OsType                    : Windows
        Name                      : vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8
        Vhd                       :
          Uri                     : https://astore.blob.core.windows.net/vmss/vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8.vhd
        Caching                   : ReadOnly
        CreateOption              : FromImage
    OsProfile                     :
      ComputerName                : myvmss1-0
      AdminUsername               : admin1
      WindowsConfiguration        :
        ProvisionVMAgent          : True
        EnableAutomaticUpdates    : True
    NetworkProfile                :
      NetworkInterfaces[0]        :
        Id                        : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/
                                    myvmss1/virtualMachines/0/networkInterfaces/mync1
    ProvisioningState             : Succeeded
    Resources[0]                  :
      Id                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachines/
                                    myvmss1_0/extensions/Microsoft.Insights.VMDiagnosticsSettings
      Name                        : Microsoft.Insights.VMDiagnosticsSettings
      Type                        : Microsoft.Compute/virtualMachines/extensions
      Location                    : centralus
      Publisher                   : Microsoft.Azure.Diagnostics
      VirtualMachineExtensionType : IaaSDiagnostics
      TypeHandlerVersion          : 1.5
      AutoUpgradeMinorVersion     : True
      Settings                    : {"xmlCfg":"...","storageAccount":"astore"}
      ProvisioningState           : Succeeded

## <a name="start-a-virtual-machine-in-a-scale-set"></a>Démarrer une machine virtuelle dans un jeu de mise à l’échelle
Remplacez hello entre guillemets les valeurs de nom hello de votre jeu de groupe et l’échelle des ressources. Remplacez  *#*  avec l’identificateur hello hello virtuels que vous souhaitez toostart et exécutez :

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Dans l’Explorateur de ressources, nous constatons qu’état hello d’instance de hello est **en cours d’exécution**:

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T02:10:08.0730839+00:00"
      },
      {
        "code": "PowerState/running",
        "level": "Info",
        "displayStatus": "VM running"
      }
    ]

Vous pouvez démarrer tous les ordinateurs virtuels hello dans hello en puissance en n’utilisant ne pas de paramètre de hello - InstanceId.

## <a name="stop-a-virtual-machine-in-a-scale-set"></a>Arrêter une machine virtuelle dans un jeu de mise à l’échelle
Remplacez hello entre guillemets les valeurs de nom hello de votre jeu de groupe et l’échelle des ressources. Remplacez  *#*  avec l’identificateur hello hello virtuels que vous souhaitez toostop et exécutez :

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Dans l’Explorateur de ressources, nous constatons qu’état hello d’instance de hello est **désalloué**:

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T01:25:17.8792929+00:00"
      },
      {
        "code": "PowerState/deallocated",
        "level": "Info",
        "displayStatus": "VM deallocated"
      }
    ]

toostop une machine virtuelle et pas désallouer, utilisez hello - StayProvisioned paramètre. Vous pouvez arrêter toutes les machines virtuelles hello hello définie en n’utilisant ne pas de paramètre de hello - InstanceId.

## <a name="restart-a-virtual-machine-in-a-scale-set"></a>Redémarrer une machine virtuelle dans un jeu de mise à l’échelle
Remplacez hello entre guillemets les valeurs de nom hello de votre ensemble d’échelle hello et de groupe de ressources. Remplacez  *#*  avec l’identificateur hello hello virtuels que vous souhaitez toorestart et exécutez :

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Vous pouvez redémarrer tous les ordinateurs virtuels hello Bonjour définie en n’utilisant ne pas de paramètre de hello - InstanceId.

## <a name="remove-a-virtual-machine-from-a-scale-set"></a>Supprimer une machine virtuelle d’un jeu de mise à l’échelle
Remplacez hello entre guillemets les valeurs de nom hello de votre ensemble d’échelle hello et de groupe de ressources. Remplacez  *#*  avec l’identificateur hello hello virtuels que vous souhaitez tooremove et exécutez :  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

Vous pouvez supprimer hello machines virtuelles identiques à la fois en n’utilisant ne pas de paramètre de hello - InstanceId.

## <a name="change-hello-capacity-of-a-scale-set"></a>Capacité de hello de modification d’un ensemble d’échelle
Vous pouvez ajouter ou supprimer des machines virtuelles par modification de la capacité de hello du jeu de hello. Obtenir le jeu de mise à l’échelle hello toochange, jeu hello capacité toowhat vous le souhaitez toobe et ensuite mettre à jour un ensemble d’échelle hello nouvelle capacité de hello souhaitées. Dans ces commandes, remplacez hello entre guillemets les valeurs de nom hello de votre ensemble d’échelle hello et de groupe de ressources.

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

Si vous supprimez des ordinateurs virtuels à partir d’un ensemble d’échelle hello, machines virtuelles de hello avec ID le plus élevés de hello sont supprimées en premier.

