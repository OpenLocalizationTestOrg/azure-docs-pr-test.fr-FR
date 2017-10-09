---
title: aaaAbout disques et les disques durs virtuels pour les machines virtuelles Windows de Microsoft Azure | Documents Microsoft
description: "Découvrez les principes de base hello des disques et des machines virtuelles disques durs virtuels pour Windows Azure."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 1b0d6bf05237bb3d1497b2c60f79a0159b730108
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a>À propos des disques et des VHD pour les machines virtuelles Azure Windows
Comme tout autre ordinateur, machines virtuelles dans Azure utilisent des disques comme un toostore place un système d’exploitation, des applications et des données. Toutes les machines virtuelles Azure possèdent au moins deux disques : un disque de système d’exploitation Windows et un disque temporaire. disque de système d’exploitation Hello est créé à partir d’une image et disque de système d’exploitation hello et image de hello sont des disques durs virtuels (VHD) stockées dans un compte de stockage Azure. Les machines virtuelles peuvent également disposer d’un ou plusieurs disques de données, également stockés sur les VHD. 

Dans cet article, nous parlons de différentes utilisations de hello pour les disques de hello et puis discuter hello différents types de disques, vous pouvez créer et utiliser. Cet article est également disponible pour les [machines virtuelles Linux](about-disks-and-vhds.md).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>Disques utilisés par les machines virtuelles

Jetons un œil sur l’utilisation des disques de hello par hello machines virtuelles.

### <a name="operating-system-disk"></a>Disque de système d’exploitation
Chaque machine virtuelle dispose d’un disque de système d’exploitation attaché. Il a enregistré en tant que lecteur SATA et étiqueté en tant que lecteur C: de hello par défaut. Ce disque a une capacité maximale de 2048 gigaoctets (Go). 

### <a name="temporary-disk"></a>Disque temporaire
Chaque machine virtuelle contient un disque temporaire. disque temporaire de Hello fournit le stockage à court terme pour les applications et les processus et données du magasin prévue tooonly tels que des fichiers d’échange. Données sur le disque temporaire de hello peuvent être perdues pendant un [événement de maintenance](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) ou lorsque vous [redéployer une machine virtuelle](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Lors du redémarrage de hello machine virtuelle standard données hello sur lecteur temporaire de hello doivent rendre persistant.

disque temporaire de Hello porte hello lecteur D: par défaut et il est utilisé pour stocker le fichier pagefile.sys. tooremap cette lettre de lecteur différente tooa de disque, consultez [modifier la lettre de lecteur hello du disque temporaire de Windows hello](change-drive-letter.md). taille de Hello du disque temporaire de hello varie selon la taille hello de machine virtuelle de hello. Pour plus d’informations, voir [Tailles des machines virtuelles Windows](sizes.md).

Pour plus d’informations sur la façon dont Azure utilise le disque temporaire de hello, consultez [présentation lecteur temporaire de hello sur des Machines virtuelles Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)


### <a name="data-disk"></a>Disque de données
Un disque de données est un disque dur virtuel est les données d’application toostore tooa attaché machine virtuelle ou d’autres données que vous devez tookeep. Les disques de données sont enregistrés en tant que disques SCSI et sont nommés avec la lettre de votre choix. Chaque disque de données offre une capacité maximale de 4095 Go. taille de machine virtuelle de hello Hello détermine le nombre de disques données vous pouvez associer un type tooit et hello de stockage, vous pouvez utiliser des disques toohost hello.

> [!NOTE]
> Pour plus d’informations sur les capacités des machines virtuelles, consultez [Tailles des machines virtuelles Windows](sizes.md).
> 

Lorsque vous créez une machine virtuelle à partir d’une image, Azure crée un disque de système d’exploitation. Si vous utilisez une image qui inclut des disques de données, Azure crée également hello disques de données lorsqu’il crée la machine virtuelle de hello. Sinon, vous ajoutez des disques de données après avoir créé l’ordinateur virtuel de hello.

Vous pouvez ajouter par machine virtuelle de données disques tooa à tout moment, **attachement** hello toohello de disque virtuels. Vous pouvez utiliser un disque dur virtuel que vous avez téléchargé ou copié le compte de stockage tooyour ou une qu’Azure crée pour vous. Attachement d’un disque de données associe fichier de disque dur virtuel hello hello machine virtuelle en plaçant un « bail » sur le disque dur virtuel de hello afin qu’il ne peut pas être supprimé du stockage s’il est toujours attaché.


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a>Une dernière recommandation : utilisez TRIM avec des disques standard non gérés 

Si vous utilisez les disques standard non gérés (disque dur), vous devez activer TRIM. La fonction TRIM ignore les blocs inutilisés sur le disque de hello afin de vous êtes facturé uniquement pour le stockage que vous utilisez réellement. Vous pouvez ainsi faire des économies si vous créez des fichiers volumineux, puis les supprimez. 

Vous pouvez exécuter ce paramètre de découpage hello commande toocheck. Ouvrez une invite de commandes sur votre machine virtuelle Windows et saisissez :


```
fsutil behavior query DisableDeleteNotify
```

Si la commande hello retourne 0, la fonction TRIM est activée correctement. Si elle retourne 1, exécutez hello suivant commande tooenable d’ajustement :

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> Remarque : Prise en charge Trim démarre avec Windows Server 2012 / Windows 8 et versions ultérieures, consultez Voir [nouvelle API permet aux applications media de toostorage indicateurs « TRIM et annuler le mappage de » toosend](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints).
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a>Étapes suivantes
* [Attacher un disque](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooadd de stockage supplémentaire pour votre machine virtuelle.
* [Modifier la lettre de lecteur hello du disque temporaire de Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) pour votre application peut utiliser le lecteur D: de hello pour les données.

