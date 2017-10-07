---
title: "aaaCreate une copie d’un disque géré de Azure pour sauvegarder | Documents Microsoft"
description: "Découvrez comment toocreate émet une copie d’un toouse des disques gérés Azure précédent ou de résolution des problèmes de disque."
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Créer une copie d’un disque dur virtuel stocké en tant que disque Azure géré à l’aide de captures instantanées gérées
Prendre un instantané d’un disque géré pour la sauvegarde ou créer un disque gérés à partir de la capture instantanée de hello et attachez-le tootroubleshoot de machine virtuelle de test tooa. Une capture instantanée gérée est une copie complète d’un disque géré de machine virtuelle à un moment donné. Elle crée une copie en lecture seule de votre disque dur virtuel et, par défaut, le stocke sous la forme d’un disque géré Standard. Pour plus d’informations sur les disques gérés, consultez [Vue d’ensemble d’Azure Managed Disks](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

Pour plus d’informations sur la tarification, consultez la page [Tarification Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/). 

## <a name="before-you-begin"></a>Avant de commencer
Si vous utilisez PowerShell, assurez-vous d’avoir hello dernière version du module PowerShell de AzureRM.Compute de hello. Exécutez hello après la commande tooinstall il.

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).

## <a name="copy-hello-vhd-with-a-snapshot"></a>Copiez hello disque dur virtuel avec un instantané
Utiliser PowerShell tootake un instantané de hello géré disque ou hello portail Azure.

### <a name="use-azure-portal-tootake-a-snapshot"></a>Utilisez tootake portail Azure un instantané 

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Désormais, dans le coin supérieur gauche de hello, cliquez sur **nouveau** et recherchez **instantané**.
3. Dans le panneau de la capture instantanée hello, cliquez sur **créer**.
4. Entrez un **nom** pour la capture instantanée de hello.
5. Sélectionnez un existant [groupe de ressources](../../azure-resource-manager/resource-group-overview.md#resource-groups) ou nom du type hello pour un nouveau. 
6. Sélectionnez un emplacement de centre de données Azure.  
7. Pour **disque Source**, sélectionnez hello toosnapshot de disques gérés.
8. Sélectionnez hello **type de compte** instantané d’hello toouse toostore. Nous vous recommandons d’utiliser le type **Standard_LRS**, sauf si vous avez besoin de la stocker sur un disque hautes performances.
9. Cliquez sur **Créer**.

### <a name="use-powershell-tootake-a-snapshot"></a>Utilisez PowerShell tootake un instantané
Hello suit afficher vous tooget hello disque dur virtuel de disque toobe copié, créer des configurations de capture instantanée hello et prenez un instantané du disque de hello en utilisant l’applet de commande New-AzureRmSnapshot de hello<!--Add link toocmdlet when available-->. 

1. Définissez certains paramètres. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  Remplacez les valeurs de paramètre hello :
  -  « myResourceGroup » avec le groupe de ressources de la machine virtuelle hello.
  -  « southeastasia » avec hello zone géographique où vous souhaitez votre instantané gérés stockées. <!---How do you look these up? -->
  -  « ContosoMD_datadisk1 » avec le nom de hello du disque du disque dur virtuel hello que vous souhaitez toocopy.
  -  « ContosoMD_datadisk1_snapshot1 » avec hello nom que vous souhaitez toouse du nouvel instantané hello.

2. Obtenir toobe de disque hello disque dur virtuel copié.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. Créer des configurations de capture instantanée hello. 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. Prendre un instantané hello.

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
Toouse hello instantané toocreate un disque géré et d’attacher une machine virtuelle qui doit effectuer haute toobe, utilisez le paramètre hello `-AccountType Premium_LRS` avec la commande hello AzureRmSnapshot de nouveau. paramètre Hello crée l’instantané d’hello afin qu’il est stocké comme disque Premium gérés. Les disques gérés Premium sont plus chers que les disques gérés Standard. Vérifiez qu’il vous faut vraiment le niveau Premium avant d’utiliser ce paramètre.


