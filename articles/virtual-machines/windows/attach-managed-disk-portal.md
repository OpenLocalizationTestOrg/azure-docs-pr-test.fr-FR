---
title: "aaaAttach un tooa disque données managées machine virtuelle Windows - Azure | Documents Microsoft"
description: "La méthode de tooattach nouvelle gestion des données disque tooa virtuelle Windows dans le portail Azure à l’aide de hello hello modèle de déploiement de gestionnaire de ressources."
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
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>Tooattach une données managées de disque tooa machine virtuelle Windows dans hello portail Azure

Cet article explique de tooattach une nouvelle données managées de disque virtuels tooWindows via hello portail Azure. Avant cela, passez en revue les conseils suivants :

* taille de Hello de machine virtuelle de hello détermine le nombre que vous pouvez attacher des disques de données. Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](sizes.md).
* Pour un nouveau disque, vous n’avez pas besoin toocreate il premier, car Azure crée lorsque vous l’attachez.

Vous pouvez également [attacher un disque de données à l’aide de PowerShell](attach-disk-ps.md).



## <a name="add-a-data-disk"></a>Ajouter un disque de données
1. Dans le menu hello hello gauche, cliquez sur **virtuels**.
2. Sélectionnez hello virtuels à partir de la liste de hello.
3. Dans le panneau de la machine virtuelle hello, cliquez sur **disques**.
   4. Sur hello **disques** panneau, cliquez sur **+ disque de données ajouter**.
5. Bonjour pour le nouveau disque de hello liste déroulante, sélectionnez **créer vide**.
6. Bonjour **disque géré de créer** panneau, tapez un nom pour le disque de hello et ajustez hello autres paramètres si nécessaire. Lorsque vous avez terminé, cliquez sur **Créer**.
7. Bonjour **disques** panneau, cliquez sur Enregistrer toosave hello nouvelle configuration de disque pour hello machine virtuelle.
6. Une fois Azure crée le disque de hello et attache la machine virtuelle de toohello, nouveau disque de hello est répertorié dans les paramètres de disque de l’ordinateur virtuel de hello sous **des disques de données**.


## <a name="initialize-a-new-data-disk"></a>Initialisation d’un nouveau disque de données

1. Se connecter toohello machine virtuelle.
1. Cliquez sur le menu Démarrer hello hello machine virtuelle et le type **diskmgmt.msc** puis appuyez sur **entrée**. Ceci démarrera hello composant logiciel enfichable Gestion des disques.
2. Gestion des disques reconnaît que vous disposez d’un nouveau disque sans être initialisé et hello initialiser le disque fenêtre s’affiche.
3. Assurez-vous que le nouveau disque de hello est sélectionné et cliquez sur **OK** tooinitialize il.
4. nouveau disque de Hello sera **non alloué**. Avec le bouton droit n’importe où sur le disque de hello et sélectionnez **nouveau volume simple**. Hello **Assistant de nouveau Volume Simple** démarre.
5. Passez en revue l’Assistant hello, conserve toutes les valeurs par défaut de hello, lorsque vous avez terminé de sélectionner **Terminer**.
6. Fermez Gestion des disques.
7. Vous obtenez un menu contextuel que vous avez besoin de nouveau disque de tooformat hello avant que vous puissiez l’utiliser. Cliquez sur **Formater le disque**.
8. Bonjour **nouveau disque de Format** boîte de dialogue, vérifiez les paramètres hello et puis cliquez sur **Démarrer**.
9. Vous serez averti que formatage des disques de hello supprimera toutes les données de hello, cliquez sur **OK**.
10. Lorsque le format de hello est terminée, cliquez sur **OK**.

## <a name="use-trim-with-standard-storage"></a>Utilisation de TRIM avec le stockage standard

Si vous utilisez le stockage standard (disque dur), vous devez activer la fonction TRIM. La fonction TRIM ignore les blocs inutilisés sur le disque de hello afin de vous êtes facturé uniquement pour le stockage que vous utilisez réellement. Vous pouvez ainsi faire des économies si vous créez des fichiers volumineux, puis les supprimez. 

Vous pouvez exécuter ce paramètre de découpage hello commande toocheck. Ouvrez une invite de commandes sur votre machine virtuelle Windows et saisissez :

```
fsutil behavior query DisableDeleteNotify
```

Si la commande hello retourne 0, la fonction TRIM est activée correctement. Si elle retourne 1, exécutez hello suivant commande tooenable d’ajustement :
```
fsutil behavior set DisableDeleteNotify 0
```

Après la suppression des données à partir de votre disque, vous pouvez garantir la défragmentation des opérations de découpage hello vidage correctement en exécutant avec la fonction TRIM :

```
defrag.exe <volume:> -l
```

Vous pouvez également vérifier la totalité du volume hello est tronqué en mettant en forme de volume de hello.

## <a name="next-steps"></a>Étapes suivantes
Si votre application a besoin de données toostore toouse hello D:, vous pouvez [modifier la lettre du lecteur de disque temporaire de Windows hello hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
