---
title: "aaaDetach un disque de données à partir d’un VM Linux - Azure | Documents Microsoft"
description: "En savoir plus toodetach un disque de données à partir d’une machine virtuelle dans Azure à l’aide de CLI 2.0 ou hello portail Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a>Toodetach données de disque à partir d’une machine virtuelle Linux

Lorsque vous n’avez plus besoin un disque de données est attachée tooa virtual machine, vous pouvez facilement la détacher. Cela supprime le disque de hello à partir de l’ordinateur virtuel de hello, mais ne le supprime pas de stockage. 

> [!WARNING]
> Si vous détachez un disque, il n’est pas supprimé automatiquement. Si vous êtes abonné tooPremium stockage, vous continuerez tooincur des frais de stockage pour le disque de hello. Pour plus d’informations, consultez trop[tarification et facturation lors de l’utilisation du stockage Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing). 
> 
> 

Si vous souhaitez toouse hello données existantes hello disque à nouveau, vous pouvez rattacher il toohello même ordinateur virtuel ou un autre.  

## <a name="detach-a-data-disk-using-cli-20"></a>Détacher un disque de données à l’aide de CLI 2.0

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

disque de Hello reste dans le stockage, mais n’est plus attaché tooa virtual machine.


## <a name="detach-a-data-disk-using-hello-portal"></a>Détacher un disque de données à l’aide du portail de hello
1. Dans le concentrateur de portail hello, sélectionnez **virtuels**.
2. Sélectionnez la machine virtuelle hello qui possède le disque de données hello toodetach et cliquez sur **arrêter** toodeallocate hello machine virtuelle.
3. Dans le panneau de la machine virtuelle hello, sélectionnez **disques**.
4. En haut de hello Hello **disques** panneau, sélectionnez **modifier**.
5. Bonjour **disques** panneau, toohello plus à droite hello du disque de données que vous aimeriez toodetach, cliquez sur hello ![détacher l’image du bouton](./media/detach-disk/detach.png) bouton détacher.
5. Après la suppression de disque de hello, cliquez sur Enregistrer en haut de hello du Panneau de hello.
6. Dans le panneau de la machine virtuelle hello, cliquez sur **vue d’ensemble** puis cliquez sur hello **Démarrer** bouton haut hello hello toorestart de panneau hello machine virtuelle.

disque de Hello reste dans le stockage, mais n’est plus attaché tooa virtual machine.








## <a name="next-steps"></a>Étapes suivantes
Si vous souhaitez que le disque de données hello tooreuse, vous pouvez juste [attachez-le tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

