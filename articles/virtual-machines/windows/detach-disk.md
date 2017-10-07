---
title: "aaaDetach un disque de données à partir d’une machine virtuelle Windows - Azure | Documents Microsoft"
description: "En savoir plus toodetach un disque de données à partir d’une machine virtuelle dans Azure à l’aide du modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: f3f581d3f33329db2ecb7d25a68bc59af7361aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-windows-virtual-machine"></a>Toodetach données de disque à partir d’une machine virtuelle Windows
Lorsque vous n’avez plus besoin un disque de données est attachée tooa virtual machine, vous pouvez facilement la détacher. Cela supprime le disque de hello à partir de l’ordinateur virtuel de hello, mais ne le supprime pas de stockage.

> [!WARNING]
> Si vous détachez un disque, il n’est pas supprimé automatiquement. Si vous êtes abonné tooPremium stockage, vous continuerez tooincur des frais de stockage pour le disque de hello. Pour plus d’informations, consultez trop[tarification et facturation lors de l’utilisation du stockage Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).
>
>

Si vous souhaitez toouse hello données existantes hello disque à nouveau, vous pouvez rattacher il toohello même ordinateur virtuel ou un autre.

## <a name="detach-a-data-disk-using-hello-portal"></a>Détacher un disque de données à l’aide du portail de hello
1. Dans le concentrateur de portail hello, sélectionnez **virtuels**.
2. Sélectionnez la machine virtuelle hello qui possède le disque de données hello toodetach et cliquez sur **arrêter** toodeallocate hello machine virtuelle.
3. Dans le panneau de la machine virtuelle hello, sélectionnez **disques**.
4. En haut de hello Hello **disques** panneau, sélectionnez **modifier**.
5. Bonjour **disques** panneau, toohello plus à droite hello du disque de données que vous aimeriez toodetach, cliquez sur hello ![détacher l’image du bouton](./media/detach-disk/detach.png) bouton détacher.
5. Après la suppression de disque de hello, cliquez sur Enregistrer en haut de hello du Panneau de hello.
6. Dans le panneau de la machine virtuelle hello, cliquez sur **vue d’ensemble** puis cliquez sur hello **Démarrer** bouton haut hello hello toorestart de panneau hello machine virtuelle.



disque de Hello reste dans le stockage, mais n’est plus attaché tooa virtual machine.

## <a name="detach-a-data-disk-using-powershell"></a>Détacher un disque de données avec PowerShell
Dans cet exemple, hello la première commande obtient hello ordinateur virtuel nommé **MyVM07** Bonjour **RG11** groupe de ressources à l’aide d’applet de commande Get-AzureRmVM de hello. Hello commande magasins hello machine virtuelle dans hello **$VirtualMachine** variable.

commande deuxième Hello supprime le disque de données hello nommé DataDisk3 à partir de l’ordinateur virtuel de hello.

commande finale Hello met à jour l’état hello du processus de hello toocomplete hello machine virtuelle de la suppression de disque de données hello.

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

Pour plus d’informations, consultez [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk).

## <a name="next-steps"></a>Étapes suivantes
Si vous souhaitez que le disque de données hello tooreuse, vous pouvez juste [attachez-le tooanother machine virtuelle](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

