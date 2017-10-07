---
title: "aaaUse une résolution des problèmes de la machine virtuelle avec Azure PowerShell Windows | Documents Microsoft"
description: "Découvrez comment tootroubleshoot machine virtuelle Windows problèmes dans Azure en vous connectant à la restauration tooa disque hello du système d’exploitation machine virtuelle à l’aide d’Azure PowerShell"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a>Résoudre les problèmes d’une machine virtuelle Windows en attachant la restauration tooa disque hello du système d’exploitation machine virtuelle à l’aide d’Azure PowerShell
Si votre machine virtuelle de Windows (VM) dans Azure rencontre une erreur de démarrage ou de disque, vous devrez peut-être tooperform étapes de dépannage sur le disque dur virtuel hello lui-même. Un exemple courant est une mise à jour de l’application qui a échoué empêche hello machine virtuelle en mesure de tooboot avec succès. Cet article détails comment toouse Azure PowerShell tooconnect votre toofix de machine virtuelle Windows tooanother disque dur virtuel toutes les erreurs, puis la recréer votre machine virtuelle d’origine.


## <a name="recovery-process-overview"></a>Vue d’ensemble du processus de récupération
Hello, résolution des problèmes de processus est la suivante :

1. Supprimer hello VM fait de rencontrer des problèmes, en conservant les disques durs virtuels hello.
2. Attacher et monter un disque dur virtuel de hello tooanother machine virtuelle Windows à des fins de dépannage.
3. Se connecter toohello résolution des problèmes de la machine virtuelle. Modifier des fichiers ou d’exécuter des outils toofix problèmes sur les disque dur virtuel d’origine hello.
4. Démontez et détacher le disque dur virtuel de hello de hello, résolution des problèmes de la machine virtuelle.
5. Créer une machine virtuelle à l’aide de hello d’origine disque dur.

Assurez-vous que vous avez [hello la dernière version d’Azure PowerShell](/powershell/azure/overview) installé et enregistré dans tooyour abonnement :

```powershell
Login-AzureRMAccount
```

Bonjour les exemples suivants, remplacez les noms de paramètres par vos propres valeurs. Exemples de noms de paramètre : `myResourceGroup`, `mystorageaccount` et `myVM`.


## <a name="determine-boot-issues"></a>Identifier les problèmes de démarrage
Vous pouvez afficher une capture d’écran de votre machine virtuelle dans Azure toohelp résoudre les problèmes de démarrage. Cette capture d’écran peut aider à identifier la cause d’une machine virtuelle échoue tooboot. Hello exemple suivant obtient hello capture d’écran de hello VM Windows nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

Passez en revue les toodetermine de capture d’écran hello pourquoi hello VM échoue tooboot. Notez les messages d’erreur ou les codes d’erreur spécifiques fournis.


## <a name="view-existing-virtual-hard-disk-details"></a>Afficher les détails du disque dur virtuel existant
Avant de pouvoir joindre votre tooanother de disque dur virtuel machine virtuelle, vous devez nom de hello tooidentify de hello les disque dur virtuel (VHD).

Hello exemple suivant obtient les informations pour hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Recherchez `Vhd URI` dans hello `StorageProfile` section à partir de la sortie de hello Hello précédant la commande. Hello tronquée exemple de sortie suivant affiche hello `Vhd URI` vers fin hello hello du bloc de code :

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a>Supprimer une machine virtuelle existante
Les disques durs virtuels et les machines virtuelles sont deux ressources distinctes dans Azure. Un disque dur virtuel consiste à stocker des hello système d’exploitation, des applications et des configurations. Hello machine virtuelle proprement dite est simplement des métadonnées qui définit la taille de hello ou l’emplacement et fait référence à des ressources, tel qu’un disque dur virtuel ou d’une carte réseau virtuelle (NIC). Chaque disque dur virtuel a un bail attribué lorsqu’il est attaché tooa machine virtuelle. Bien que les disques de données peuvent être attachées et détachées même pendant l’exécution de la machine virtuelle de hello, les disques du système d’exploitation hello ne peut pas être détachée tant que hello ressource d’ordinateur virtuel est supprimé. bail de Hello continue disque hello du système d’exploitation de tooassociate avec une machine virtuelle, même lorsque l’ordinateur virtuel est dans un état arrêté et est libéré.

Hello première étape toorecover votre machine virtuelle est la ressource d’ordinateur virtuel hello toodelete lui-même. Suppression hello VM laisse hello des disques durs virtuels dans votre compte de stockage. Après hello que machine virtuelle est supprimée, vous attachez hello disque dur virtuel tooanother VM tootroubleshoot et résolvez les erreurs de hello.

Hello suivant supprime de l’exemple hello ordinateur virtuel nommé `myVM` du groupe de ressources hello nommé `myResourceGroup`:

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

Attendez la fin hello VM suppression avant de joindre tooanother de disque dur virtuel hello machine virtuelle. bail Hello sur le disque dur virtuel hello qui associe hello machine virtuelle doit toobe publié avant de pouvoir joindre tooanother de disque dur virtuel hello machine virtuelle.


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>Attacher tooanother de disque dur virtuel existant machine virtuelle
Pour hello en suivant quelques étapes, vous utilisez un autre ordinateur virtuel à des fins de dépannage. Vous attachez hello toothis de disque dur virtuel existant dépannage toobrowse de machine virtuelle et que vous modifiez le contenu du disque hello. Ce processus vous permet de toocorrect toutes les erreurs de configuration ou examiner des applications supplémentaires ou de système de fichiers journaux, par exemple. Choisissez ou créez une autre machine virtuelle toouse, à des fins de dépannage.

Lorsque vous attachez le disque dur virtuel existant hello, spécifier le disque de toohello URL hello obtenu Bonjour précédent `Get-AzureRmVM` commande. exemple Hello attache un toohello disque dur virtuel existant, résolution des problèmes d’ordinateur virtuel nommé `myVMRecovery` dans le groupe de ressources hello nommé `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> Ajout d’un disque nécessite de taille de hello toospecify du disque de hello. Comme nous attacher un disque existant, hello `-DiskSizeInGB` est spécifié en tant que `$null`. Cette valeur permet de disque de données hello est correctement attaché, et sans hello devez toodetermine hello taille réelle du disque de données.


## <a name="mount-hello-attached-data-disk"></a>Monter le disque de données attaché hello

1. RDP tooyour de résolution des problèmes de la machine virtuelle en utilisant les informations d’identification appropriées hello. fichier de connexion RDP hello pour hello ordinateur virtuel nommé télécharge Hello exemple suivant `myVMRecovery` dans le groupe de ressources hello nommé `myResourceGroup`et le télécharge trop`C:\Users\ops\Documents`»

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. disque de données Hello est automatiquement détecté et attaché. Affichez la liste hello de lettre de lecteur de volumes attachés toodetermine hello comme suit :

    ```powershell
    Get-Disk
    ```

    Hello suivant l’exemple de sortie montre hello un disque dur virtuel connecté à un disque **2**. (Vous pouvez également utiliser `Get-Volume` lettre de lecteur tooview hello) :

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a>Résoudre des problèmes sur le disque dur virtuel d’origine
Avec hello disque dur virtuel existant monté, vous pouvez désormais effectuer une maintenance et dépannage en fonction des besoins. Une fois que vous avez corrige les problèmes de hello, poursuivez hello comme suit.


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>Démonter et dissocier le disque dur virtuel d’origine
Une fois les erreurs résolues, vous démontez et détachez un disque dur virtuel existant hello à partir de votre machine virtuelle de résolution des problèmes. Vous ne pouvez pas utiliser votre disque dur virtuel avec n’importe quel autre machine virtuelle jusqu'à ce que le bail hello attachement toohello de disque dur virtuel hello résolution des problèmes de la machine virtuelle est libéré.

1. À partir de votre session RDP, démontez disque de données hello sur votre ordinateur virtuel de récupération. Vous devez le numéro du disque à partir de hello hello précédente `Get-Disk` applet de commande. Ensuite, utilisez `Set-Disk` disque de hello tooset comme étant hors connexion :

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    Vérifiez le disque de hello est désormais défini à l’aide hors connexion `Get-Disk` à nouveau. Hello exemple de sortie suivant affiche hello disque est désormais défini comme étant hors connexion :

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. Quittez la session Bureau à distance. À partir de votre session Azure PowerShell, supprimez le disque dur virtuel de hello hello résolution des problèmes de la machine virtuelle.

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a>Créer une machine virtuelle à partir du disque dur d’origine
utilisation d’une machine virtuelle à partir de votre disque dur virtuel d’origine, toocreate [ce modèle Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet). modèle JSON réel Hello est à hello lien :

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json

modèle de Hello déploie une machine virtuelle dans un réseau virtuel existant, à l’aide de hello URL de disque dur virtuel à partir de hello commande précédemment. exemple Hello déploie groupe de ressources hello modèle toohello nommé `myResourceGroup`:

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

Hello de réponse demande modèle hello comme nom d’ordinateur virtuel, le type de système d’exploitation et taille de machine virtuelle. Hello `osDiskVhdUri` est hello même que celui précédemment utilisé lors de l’attachement toohello disque dur virtuel existant de hello, résolution des problèmes de la machine virtuelle.


## <a name="re-enable-boot-diagnostics"></a>Réactiver les diagnostics de démarrage

Lorsque vous créez votre machine virtuelle à partir du disque dur virtuel existant hello, les diagnostics de démarrage ne peut pas être automatiquement activés. Hello exemple suivant permet d’extension de diagnostic hello sur hello ordinateur virtuel nommé `myVMDeployed` dans le groupe de ressources hello nommé `myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a>Étapes suivantes
Si vous rencontrez des problèmes de connexion tooyour machine virtuelle, consultez [tooan des connexions RDP de résoudre les problèmes Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Pour résoudre les problèmes liés à l’accès aux applications exécutées sur votre machine virtuelle, consultez [Résoudre les problèmes de connectivité des applications sur une machine virtuelle Windows](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Pour plus d’informations sur l’utilisation de Resource Manager, consultez la page [Présentation d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
