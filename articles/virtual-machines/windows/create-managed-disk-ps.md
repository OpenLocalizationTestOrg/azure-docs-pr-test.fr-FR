---
title: "aaaCreate un disque géré à partir d’un disque dur virtuel dans Azure | Documents Microsoft"
description: "Créer un disque géré à partir d’un disque dur virtuel est en cours d’un compte de stockage Azure à l’aide du modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: 77adaac5419186ff85039fe2c4752f021aa5e448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a>Créer des disques gérés à partir de disques non gérés dans un compte de stockage

Un disque géré peut être créé à partir d’un disque de données ou d’un disque du système d’exploitation existant hébergé dans un compte de stockage Azure. Vous pouvez également créer un disque vide utilisable comme nouveau disque de données pour une machine virtuelle. 

## <a name="before-you-begin"></a>Avant de commencer
Si vous utilisez PowerShell, assurez-vous d’avoir hello dernière version du module PowerShell de AzureRM.Compute de hello. Exécutez hello après la commande tooinstall il.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a>Créer un disque géré à partir d’un disque dur virtuel dans un compte de stockage Azure

Dans l’exemple hello nous créer un disque à partir d’un disque dur virtuel en tant que disque géré et affectez-le toohello paramètre **$disque1** toouse plus tard. 

Hello disque géré sera créé dans hello **ouest des États-Unis** emplacement, dans un groupe de ressources nommé **myResourceGroup**. disque de Hello sera nommé **myDisk** et il sera créé à partir d’un fichier de disque dur virtuel nommé **myDisk.vhd** nous téléchargé précédemment tooa compte de stockage nommé **mystorageaccount**. disque géré de Hello sera créé dans le stockage de premium localement redondant (LRS). StandardLRS et PremiumLRS sont hello uniquement **- AccountType** options disponibles pour des disques gérés. 

1.  Définir les paramètres requis

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. Créer un disque de données hello. 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a>Créez un disque de données vide comme disque géré

Dans l’exemple hello nous créer un disque de données vide en tant que disque géré et affectez-le toohello paramètre **dataDisk2 $** toouse plus tard. Un disque de données vide devez toobe initialisé la connexion toohello machine virtuelle et à l’aide de diskmgmt.msc ou [à distance via WinRM et un script](attach-disk-ps.md#initialize-the-disk), une fois qu’il est attaché tooa machine virtuelle en cours d’exécution.

disque de données vide Hello sera créé dans hello **ouest des États-Unis** emplacement, dans un groupe de ressources nommé **myResourceGroup**. disque de Hello sera nommé **myEmptyDataDisk**. un disque vide Hello sera créé dans le stockage de premium localement redondant (LRS). StandardLRS et PremiumLRS sont hello uniquement **- AccountType** options disponibles pour des disques gérés.

taille du disque Hello dans cet exemple est de 128 Go, mais vous devez choisir une taille qui répond aux besoins de hello de toutes les applications en cours d’exécution sur votre machine virtuelle.

1.  Définir les paramètres requis

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. Créer un disque de données hello.
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a>Étapes suivantes   
- Si vous disposez déjà d’une machine virtuelle, vous pouvez y [attacher un disque de données](attach-disk-portal.md).
