---
title: aaaAttach un tooa disque classique Azure VM | Documents Microsoft
description: "Attacher une machine virtuelle données disque tooa Windows créée avec le modèle de déploiement classique hello et son initialisation."
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Attacher une machine virtuelle données disque tooa Windows créée avec le modèle de déploiement classique de hello
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

Cet article vous explique comment tooattach les disques nouveaux et existants créés avec hello classique déploiement modèle tooa machine virtuelle Windows à l’aide de hello portail Azure.

Vous pouvez également [attacher un tooa de disque de données Linux VM Bonjour Azure portal](../../linux/attach-disk-portal.md).

Avant d’attacher un disque, lisez les conseils suivants :

* taille de Hello de machine virtuelle de hello détermine le nombre que vous pouvez attacher des disques de données. Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* toouse stockage Premium, vous devez un ordinateur virtuel de la série DS ou GS-series. Vous pouvez utiliser des disques de comptes de stockage Premium et Standard avec ces machines virtuelles. Le stockage Premium est disponible dans certaines régions. Pour plus d’informations, voir l’article [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

* Pour un nouveau disque, vous n’avez pas besoin toocreate il premier, car Azure crée lorsque vous l’attachez.

Vous pouvez également [attacher un disque de données à l’aide de PowerShell](../../virtual-machines-windows-attach-disk-ps.md).

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).

## <a name="find-hello-virtual-machine"></a>Trouver l’ordinateur virtuel de hello
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Machine virtuelle de hello SELECT à partir de la ressource hello répertorié dans le tableau de bord hello.
3. Dans le volet gauche, hello sous **paramètres**, cliquez sur **disques**.

    ![Ouverture des paramètres d’un disque](./media/attach-disk/virtualmachinedisks.png)

Continuez en suivant les instructions pour attacher un [nouveau disque](#option-1-attach-a-new-disk) ou un [disque existant](#option-2-attach-an-existing-disk).

## <a name="option-1-attach-and-initialize-a-new-disk"></a>Option 1 : attacher et initialiser un nouveau disque

1. Sur hello **disques** panneau, cliquez sur **attacher nouvelle**.
2. Passez en revue les paramètres par défaut de hello, mettre à jour si nécessaire, puis cliquez sur **OK**.

   ![Examen des paramètres d’un disque](./media/attach-disk/attach-new.png)

3. Une fois Azure crée le disque de hello et attache la machine virtuelle de toohello, nouveau disque de hello est répertorié dans les paramètres de disque de l’ordinateur virtuel de hello sous **des disques de données**.

### <a name="initialize-a-new-data-disk"></a>Initialisation d’un nouveau disque de données

1. Connecter l’ordinateur virtuel de toohello. Pour obtenir des instructions, consultez [comment tooconnect et ouverture de session tooan Azure virtual machine exécutant Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Une fois que vous ouvrez une session sur l’ordinateur virtuel de toohello, ouvrez **le Gestionnaire de serveur**. Dans le volet gauche de hello, sélectionnez **File and Storage Services**.

    ![Ouvrir le gestionnaire de serveur](../media/attach-disk-portal/fileandstorageservices.png)

3. Sélectionnez **Disques**.
4. Hello **disques** section répertorie les disques hello. En règle générale, une machine virtuelle contient le disque 0, le disque 1 et le disque 2. Le disque 0 est le disque du système d’exploitation hello, disque 1 est le disque temporaire de hello et le disque 2 est le disque de données hello nouvellement attachés toohello virtual machine. listes de disque de données Hello hello Partition en tant que **inconnu**.

 Cliquez sur le disque de hello et sélectionnez **initialiser**.

5. Vous êtes averti que toutes les données seront effacées lors de l’initialisation de disque de hello. Cliquez sur **Oui** disque hello tooacknowledge hello avertissement et d’initialisation. Une fois terminé, partition de hello est répertoriée comme **GPT**. Avec le bouton droit à nouveau de disque de hello et sélectionnez **nouveau Volume**.

6. Exécutez l’Assistant hello à l’aide des valeurs par défaut de hello. Une fois terminé, Assistant de hello hello **Volumes** section répertorie le nouveau volume de hello. Hello disque est maintenant en ligne et prêt toostore données.

    ![Volume correctement initialisé](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a>Option 2 : attacher un disque existant
1. Sur hello **disques** panneau, cliquez sur **attacher existant**.
2. Sous **Attacher un disque existant**, cliquez sur **Emplacement**.

   ![Attachement d’un disque existant](./media/attach-disk/attachexistingdisksettings.png)
3. Sous **comptes de stockage**, sélectionnez le compte de hello et conteneur qui contient le fichier .vhd de hello.

   ![Recherche d’emplacement VHD](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. Sélectionnez le fichier .vhd de hello.
5. Sous **attachement du disque existant**, fichier hello vous venez de sélectionner est répertorié sous **fichier de disque dur virtuel**. Cliquez sur **OK**.
6. Une fois Azure attache hello disque toohello virtual machine, il est répertorié dans les paramètres de disque de l’ordinateur virtuel de hello sous **des disques de données**.

## <a name="use-trim-with-standard-storage"></a>Utilisation de TRIM avec le stockage standard

Si vous utilisez le stockage standard (disque dur), vous devez activer la fonction TRIM. La fonction TRIM ignore les blocs inutilisés sur le disque de hello afin de vous êtes facturé uniquement pour le stockage que vous utilisez réellement. La fonction TRIM peut réduire les coûts, notamment les blocs inutilisés qui résultent de la suppression de fichiers volumineux.

Vous pouvez exécuter ce paramètre de découpage hello commande toocheck. Ouvrez une invite de commandes sur votre machine virtuelle Windows et saisissez :

```
fsutil behavior query DisableDeleteNotify
```

Si la commande hello retourne 0, la fonction TRIM est activée correctement. Si elle retourne 1, exécutez hello suivant commande tooenable d’ajustement :
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a>Étapes suivantes
Si votre application a besoin de données toostore toouse hello D:, vous pouvez [modifier la lettre du lecteur de disque temporaire de Windows hello hello](../../virtual-machines-windows-change-drive-letter.md).

## <a name="additional-resources"></a>Ressources supplémentaires
[À propos des disques et VHD pour machines virtuelles](../../virtual-machines-linux-about-disks-vhds.md)
