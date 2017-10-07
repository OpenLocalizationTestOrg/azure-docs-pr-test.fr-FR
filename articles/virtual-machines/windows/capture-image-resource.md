---
title: "aaaCreate une image managée dans Azure | Documents Microsoft"
description: "Créer une image managée d’une machine virtuelle ou d’un disque dur virtuel généralisé(e) dans Azure. Les images peut être utilisé toocreate plusieurs machines virtuelles qui utilisent des disques gérés."
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
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a>Créer une image managée d’une machine virtuelle généralisée dans Azure

Une ressource d’image managée peut être créée à partir d’une machine virtuelle généralisée stockée comme un disque géré ou non géré dans un compte de stockage. Hello image peut ensuite être utilisé toocreate plusieurs machines virtuelles. 


## <a name="generalize-hello-windows-vm-using-sysprep"></a>Généraliser hello virtuelle Windows à l’aide de Sysprep

Sysprep supprime toutes vos informations de compte personnel, entre autres choses et prépare hello machine toobe est utilisé en tant qu’image. Pour plus d’informations sur Sysprep, consultez [comment tooUse Sysprep : Introduction](http://technet.microsoft.com/library/bb457073.aspx).

Assurez-vous que les rôles de serveur hello en cours d’exécution sur l’ordinateur de hello sont pris en charge par Sysprep. Pour plus d’informations, consultez [Prise en charge de Sysprep pour les rôles serveur](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Si vous exécutez Sysprep avant de télécharger votre tooAzure de disque dur virtuel pour hello première fois, vérifiez que vous disposez [préparé votre machine virtuelle](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avant d’exécuter Sysprep. 
> 
> 

1. Se connecter toohello machine virtuelle Windows.
2. Ouvrez la fenêtre d’invite de commandes hello en tant qu’administrateur. Basculez hello trop**%windir%\system32\sysprep**, puis exécutez `sysprep.exe`.
3. Bonjour **outil de préparation système** boîte de dialogue, sélectionnez **entrer le système Out-of-Box Experience (OOBE)**et assurez-vous que hello **Generalize** case à cocher est activée.
4. Dans **Options d’arrêt**, sélectionnez **Arrêter**.
5. Cliquez sur **OK**.
   
    ![Démarrer Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. Quand Sysprep se termine, il arrête de machine virtuelle de hello. Ne redémarrez pas hello machine virtuelle.


## <a name="create-a-managed-image-in-hello-portal"></a>Créer une image managée dans le portail de hello 

1. Ouvrez hello [portal](https://portal.azure.com).
2. Cliquez sur hello signe toocreate une nouvelle ressource.
3. Dans la recherche de filtre hello, tapez **Image**.
4. Sélectionnez **Image** à partir des résultats de hello.
5. Bonjour **Image** panneau, cliquez sur **créer**.
6. Dans **nom**, tapez un nom pour l’image de hello.
7. Si vous avez plusieurs abonnements, sélectionnez hello un correct à partir de hello **abonnement** liste déroulante.
7. Dans **groupe de ressources** sélectionnez **nouvel** et tapez un nom ou sélectionnez **partir d’un** et sélectionnez un toouse de groupe de ressources à partir de la liste déroulante de hello.
8. Dans **emplacement**, choisissez l’emplacement hello de votre groupe de ressources.
9. Dans **type de système d’exploitation** sélectionner type hello du système d’exploitation, Windows ou Linux.
11. Dans **objet blob de stockage**, cliquez sur **Parcourir** toolook pour hello disque dur virtuel dans le stockage Azure.
12. Dans **Type de compte**, choisissez Standard_LRS ou Premium_LRS. Le type Standard utilise des disques durs et Premium, des disques SSD. Les deux utilisent le stockage localement redondant.
13. Dans **mise en cache disque** sélectionnez hello option mise en cache de disque approprié. options de Hello sont **aucun**, **en lecture seule** et **en lecture-écriture**.
14. Facultatif : Vous pouvez également ajouter une image de toohello de disque de données existante en cliquant sur **+ disque de données ajouter**.  
15. Une fois les sélections terminées, cliquez sur **Créer**.
16. Après la création d’image de hello, vous verrez comme un **Image** ressource dans la liste hello de ressources dans le groupe de ressources hello choisis.



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a>Créer une image managée d’une machine virtuelle à l’aide de Powershell

Création d’une image directement à partir de hello que VM garantit cette image hello inclut tous les disques hello associés hello machine virtuelle, y compris hello disque de système d’exploitation et les disques de données.


Avant de commencer, assurez-vous d’avoir hello dernière version du module PowerShell de AzureRM.Compute de hello. Exécutez hello après la commande tooinstall il.

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Pour plus d’informations, consultez la page relative au [contrôle de version d’Azure PowerShell](/powershell/azure/overview).


1. Définissez des variables.

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. Vérifiez que hello que machine virtuelle a été libérée.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Définir le statut de hello de machine virtuelle de hello trop**généralisé**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. Obtenir un ordinateur virtuel de hello. 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. Créer la configuration de l’image hello.

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. Créer l’image de hello.

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a>Créer une image managée d’un disque dur virtuel à l’aide de Powershell

Créez une image managée à l’aide de votre disque dur virtuel généralisé de système d’exploitation.


1.  Tout d’abord, définissez les paramètres communs hello :

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. Hello Step\deallocate machine virtuelle.

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. Marquer hello machine virtuelle comme généralisé.

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  Créer l’image de hello à l’aide de votre disque dur virtuel du système d’exploitation généralisé.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a>Créer une image managée à partir d’une capture instantanée à l’aide de Powershell

Vous pouvez également créer une image managée à partir d’un instantané de disque dur virtuel à partir d’une machine virtuelle généralisée de hello.

    
1. Définissez des variables. 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. Obtenir un instantané de hello.

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. Créer la configuration de l’image hello.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. Créer l’image de hello.

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a>Étapes suivantes
- Vous pouvez à présent [créer une machine virtuelle à partir de l’image managée de hello généralisé](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).    

