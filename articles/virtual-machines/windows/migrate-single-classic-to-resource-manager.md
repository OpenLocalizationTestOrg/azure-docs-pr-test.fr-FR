---
title: "aaaMigrate un tooan VM classique ARM gérés disque VM | Documents Microsoft"
description: "Migrer des machines virtuelles Azure à partir de déploiement classique de hello tooManaged des disques dans le modèle de déploiement du Gestionnaire de ressources hello de modèle."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a>Migrer manuellement un tooa VM classique ARM gérés disque machine virtuelle à partir de hello disque dur virtuel 


Cette section vous aide à vous toomigrate vos machines virtuelles Azure existantes à partir du modèle de déploiement classique hello trop[disques gérés](managed-disks-overview.md) dans le modèle de déploiement du Gestionnaire de ressources hello.


## <a name="plan-for-hello-migration-toomanaged-disks"></a>Planifier la migration de hello de tooManaged disques

Cette section vous aide à toomake hello meilleure décision sur les types de machine virtuelle et le disque.


### <a name="location"></a>Lieu

Choisissez un emplacement où Azure Managed Disks est disponible. Si vous migrez des disques gérés tooPremium, vérifiez également que le stockage Premium est disponible dans la région de hello lorsque vous prévoyez de toomigrate à. Pour obtenir des informations à jour sur les emplacements disponibles, consultez [Services Azure par région](https://azure.microsoft.com/regions/#services).

### <a name="vm-sizes"></a>Tailles de machine virtuelle

Si vous effectuez une migration tooPremium des disques gérés, vous tooupdate hello taille êtes de hello VM tooPremium taille capable de stockage disponible dans la région de hello où se trouve la machine virtuelle. Passez en revue les tailles de machine virtuelle hello qui sont capables de stockage Premium. spécifications de taille de machine virtuelle Azure Hello sont répertoriées dans [tailles des machines virtuelles](sizes.md).
Passez en revue les caractéristiques de performances hello d’ordinateurs virtuels qui fonctionnent avec un stockage Premium et choisissez hello plus approprié taille de machine virtuelle qui convient le mieux à votre charge de travail. Assurez-vous qu’il y suffisamment de bande passante disponible sur votre trafic de disque de machine virtuelle toodrive hello.

### <a name="disk-sizes"></a>Tailles du disque

**Disques gérés Premium**

Il existe sept types de disques gérés Premium qui peuvent être utilisés avec votre machine virtuelle, chacun d’eux présentant des limites d’E/S par seconde et de débit spécifiques. Prendre en compte ces limites lorsque vous choisissez hello le type de disque Premium pour votre machine virtuelle en fonction des besoins de hello de votre application en termes de capacité, les performances, l’évolutivité, et des pics.

| Type de disque Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Taille du disque           | 128 Go| 512 Go| 128 Go| 512 Go            | 1024 Go (1 To)    | 2 048 Go (2 To)    | 4 095 Go (4 To)    | 
| IOPS par disque       | 120   | 240   | 500   | 2 300              | 5 000              | 7500              | 7500              | 
| Débit par disque | 25 Mo par seconde  | 50 Mo par seconde  | 100 Mo par seconde | 150 Mo par seconde | 200 Mo par seconde | 250 Mo par seconde | 250 Mo par seconde | 

**Disques gérés Standard**

Il existe sept types de disques gérés Standard qui peuvent être utilisés avec votre machine virtuelle. Chacun d’eux dispose d’une capacité différente, mais ils partagent les mêmes limites d’E/S par seconde et de débit. Choisissez le type hello de disques gérés Standard selon les besoins en capacité hello de votre application.

| Type de disque Standard  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Taille du disque           | 30 Go            | 64 Go            | 128 Go           | 512 Go           | 1024 Go (1 To)   | 2 048 Go (2 To)    | 4 095 Go (4 To)   | 
| IOPS par disque       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Débit par disque | 60 Mo par seconde | 60 Mo par seconde | 60 Mo par seconde | 60 Mo par seconde | 60 Mo par seconde | 60 Mo par seconde | 60 Mo par seconde | 


### <a name="disk-caching-policy"></a>Stratégie de mise en cache du disque 

**Disques gérés Premium**

Par défaut, la mise en cache de stratégie est *en lecture seule* pour tous les hello disques de données Premium, et *en lecture-écriture* hello Premium système d’exploitation attaché toohello machine virtuelle. Ce paramètre de configuration est recommandé tooachieve hello des performances optimales IOs de votre application. Pour les disques de données en écriture seule ou avec d'importantes opérations d'écriture (par ex., les fichiers journaux de SQL Server), désactivez la mise en cache du disque pour de meilleures performances de l'application.

### <a name="pricing"></a>Tarification

Hello de révision [prix des disques gérés](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Tarification de disques gérés de Premium est identique hello les disques Premium non managé. En revanche, la tarification des disques gérés Standard est différente de celle des disques non gérés Standard.


## <a name="checklist"></a>Liste de contrôle

1.  Si vous migrez des disques gérés tooPremium, assurez-vous qu’il est disponible dans la région de hello que vous effectuez la migration.

2.  Décidez nouvelle série VM hello, que vous allez utiliser. Il doit être un stockage Premium compatibles si vous migrez des disques gérés tooPremium.

3.  Décidez hello exacte taille de machine virtuelle que vous utiliserez qui sont disponibles dans la région de hello que vous effectuez la migration. Taille de machine virtuelle doit toobe toosupport suffisamment grand hello différents disques de données que vous avez. Par exemple, si vous avez quatre disques de données, hello machine virtuelle doit avoir deux ou plusieurs noyaux. Prenez également en considération les besoins en puissance, mémoire et bande passante réseau.

4.  Des informations VM hello en cours pratiques, y compris les listes de hello des disques et des objets BLOB de disque dur virtuel correspondant.

Préparez votre application pour les interruptions de service. toodo une nouvelle migration, vous avez toostop tout traitement hello dans le système actuel de hello. Alors seulement vous pouvez l’obtenir état tooconsistent dont vous pouvez migrer toohello nouvelle plateforme. Temps d’arrêt dépend de la quantité de hello de données dans toomigrate de disques hello.


## <a name="migrate-hello-vm"></a>Migrer hello machine virtuelle

Préparez votre application pour les interruptions de service. toodo une nouvelle migration, vous avez toostop tout traitement hello dans le système actuel de hello. Alors seulement vous pouvez l’obtenir état tooconsistent dont vous pouvez migrer toohello nouvelle plateforme. Temps d’arrêt dépend de quantité hello d’hello disques toomigrate.


1.  Tout d’abord, définissez les paramètres communs hello :

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  Créer un disque du système d’exploitation géré à l’aide de hello disque dur virtuel à partir de hello VM classique.

    Assurez-vous d’avoir fourni hello compléter URI Hello paramètre toohello $osVhdUri de disque dur virtuel du système d’exploitation. De plus, dans **Type de compte**, indiquez **PremiumLRS** ou **StandardLRS** selon le type de disque (Premium ou Standard) vers lequel vous effectuez la migration.

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  Attacher hello du système d’exploitation disque toohello nouvelle machine virtuelle.

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  Créer un disque de données managées à partir du fichier de disque dur virtuel de données hello et l’ajouter toohello nouvelle machine virtuelle.

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  Créer hello du nouvel ordinateur virtuel par définition publique IP, réseau virtuel et carte réseau.

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
>Il peut y avoir toosupport nécessaire des étapes supplémentaires votre application est ne pas couvert par ce guide.
>
>

## <a name="next-steps"></a>Étapes suivantes

- Connecter l’ordinateur virtuel de toohello. Pour obtenir des instructions, consultez [comment tooconnect et ouverture de session tooan Azure virtual machine exécutant Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

